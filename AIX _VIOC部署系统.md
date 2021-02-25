需要的：正常运行的 VIOS、已经建立好的 VIO Client、nim master、mksysb 备份、服务器已连接上交换机

## 在 nim 部署并下发系统

### 配置 Resource
1. /etc/hosts 添加准备部署的分区
```
...
...


test01 10.3.1.1
test02 10.3.1.2
```

2. nim 添加 mksysb 资源

   以下几步都在 `smit nim` 里进行，推荐一次性做完

   `smit nim`  -> Perform NIM Administration Tasks -> Manage resources -> Define a resource -> mksysb

3. nim 定义 machine

   `smit nim`  -> Perform NIM Administration Tasks -> Manage machines -> Define a machine

4. 使用 mksysb 生成 spot文件

   原本以为可以直接开始了，发现安装系统时还需要 spot 文件，可以使用 mksysb 生成

   `smit nim`

   Perform NIM Administration Tasks -> Manage resources -> Define a resource -> spot

   Resource name：生成的 spot 文件名

   Server of Resource：master

   Source of Install Image：在 list 中找到 mksysb

   Location of install image ：生成 spot 的位置

   使用此方法生成后，会自动定义 spot

3. 检查

   `lsnim -l  `  查看所有定义的nim资源



### 配置存储映射

单位的习惯为分区 rootvg 使用 VSCSI，datavg 数据盘使用 NPIV。



- VSCSI

  1. 查看物理光纤卡的 WWN 并提供给存储、交换机。

     ```shell
      # VIOS中操作，多 VIOS 需要收集每个 VIOS 的信息。
      $ oem_setup_env 
      lscfg -vpl fcs2|grep Address
      # 返回中，Network Address 即为 WWN
      Network Address.................1000000000000FADFSDFASF
     ```

   2. 安装所需的 MPIO 驱动

      VSCSI 需要在建立映射的 VIOS 安装 MPIO 驱动。

      使用的存储为 NetApp，**NetApp必须安装** NetApp Host Utilities 中的 MPIO 驱动（推荐把 ToolKit 也安装上，方便管理），系统自带的多路径无法识别 NetApp 的磁盘，默认会将单块磁盘识别为多个 Other FC SCSI Disk Drive，影响使用，此时解决方法：`rmdev -Rdl hdisk100`。
      
   3. VIOS 识别磁盘

      存储划分完成后，在 VIOS 中 `cfgmgr`，`lsdev -Cc disk` 查看。NetApp 安装 SAN_ToolKit后可以使用`sanlun lun show`  查看状态，可能还需要调整相关属性。

      ```shell
      # lsdev|grep disk
      ...
      ...
      hdisk100 　　　　Available 111-T1-01 　　　　MPIO NetApp FCP Default PCM Disk
      ```

   4. VIOS配置映射：

      ```shell
      $mkvdev -vdev hdisk26 -vadapter vhost37 -dev -rg0_lpar40
      $mkvdev -vdev hdisk27 -vadapter vhost37 -dev -rg1_lpar40
      # 返回
      rg0_lpar40 Available
      rg1_lpar40 Available
      ```

      没有指定 vhost 设备的话，可以从 HMC 进行添加（修改 profile 或者在有 RMC 连接的情况下动态添加均可）

      验证：`$lsmap -all`，可以看到 vhost 下分配的对应磁盘
      
      建错了删除：`$rmvdev -vtd rg0_lpar40`

  

- NPIV

  1. 收集 WWN。NPIV 存储、交换机端不需要 VIOS 的光纤卡信息，仅需要虚拟光纤卡的信息。

     可以在 HMC 的分区 profile 中查看 VIOC 虚拟光纤卡的 WWN。每张虚拟光纤卡有两个 WWPN，第二个为 LPM 使用，不需要可以不配置。

  2. VIOS配置映射：

     ```shell
     $vfcmap –vadapter vfchost0 –fcp fcs3 
     ```

  ​       验证：NPIV 在 VIOS 中无法看到映射的磁盘。使用`$lsmap -all -npiv`  查看对应 vfchost 下的工作状态，Status 配置正常则为 LOGGED_IN.

  接下来还需要在 VIOC 上安装多路径工具，不过目前系统未安装，稍后再进行操作。




### 安装系统

#### nim操作

1. `smit nim`  -> Perform NIM Software Installation and Maintenance Tasks -> Install and Update Software -> Install the Base Operating System on Standalone Clients

2. 选择定义好的 machine

3. TYPE 为 mksysb，再指定 spot
4. 修改以下选项，安装：
   - ACCEPT new license agreements: **yes**
   - Intitate reboot and installation now? : **no**
   - 下方另一个 ACCEPT new license agreements: **yes**

#### HMC操作

1. 修改分区名，需与 nim server 的 host 文件、 machine 名一致

2. 确认 profile 文件已经加上了所需虚拟适配器、资源足够

3. 使用正确的 profile 文件，以 **SMS 模式**  启动分区

#### 分区操作

1. 通过 HMC vtmenu 进入已经通过 SMS 模式启动的分区

2. 配置 IP 并测试
   - **Select Remote IPL** -> 选择网卡设备 -> ipv4 -> BOOTP 
   - 在 IP Parameters 配置 IP
   - 配置完成后，返回进行 Ping test，确保 ping 测试成功

3. 从网络引导

   重复 ESC 回到首页，选择  **Select Boot Options** -> Select Install/Boot Device -> Network -> 刚才的网卡设备 -> Normal Mode Boot -> Yes.

   稍等片刻后，就会显示已经在从 nim 服务器接受数据了。

4. 继续安装

   等待终端显示多语言界面，输入显示的数字，回车，再选择语言，继续进行安装。

   默认会安装在映射过来的 hdisk0 上，当然也可以通过 **Change/Show Installation Settings and Install** 配置安装选项，按 0 保存配置并准备安装。期间若有磁盘等不满足亦会显示。

   确认无误后，回车开始安装。模板的操作系统安装完成。

5. 安装完成后，配置存储 NPIV 映射

   系统安装完成后，登录系统，安装 MPIO 多路径驱动，和 VIOS 的安装验证方法相同。

   验证：

   `cfgmgr`，`lsdev -Cc disk`





