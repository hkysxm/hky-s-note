 > 遇到的AIX特有指令，日后进行分类


`entstat`：Shows Ethernet device driver and device statistics.

`chdev`：Changes the characteristics of a device.

 - **Syntax**：`chdev -l Name [  -a Attribute=Value ... ] [  -f File ] [ -h ] [  -p ParentName ] [  -P | -T ] [  -U ][  -q ] [  -w ConnectionLocation ] [ -g ]`

`lspath`：Displays information about paths to an MultiPath I/O (MPIO) capable device.

 - **Syntax**：`lspath [ -F Format | –t ] [ -H ] [ -l Name ] [ -p Parent ] [ -s Status ] [ -w Connection ] [ -i PathID ]`

   `lspath -A -l Name -p Parent [ -w Connection ] [ -i PathID ] {-D [ -O ] | -E [ -O ] | -F Format [ -Z character ] } [ -a Attribute ] ...[ -f File ] [ -H ]`

    `lspath -A -l Name -p Parent [ -w Connection ] [ -i PathID ]-R -a Attribute [ -f File ] [ -H ]`

`chpath`：Changes the operational status of paths to an MultiPath I/O (MPIO) capable device, or changes an attribute associated with a path to an MPIO capable device.

 - **Syntax**：`chpath -l Name -s OpStatus [ -p Parent ] [ -w Connection ] [ -i PathID ]`

   `chpath -l Name -p Parent [ -w Connection ] [ -P ] -a Attribute=Value [ -a Attribute=Value ... ] [ -g ]`

   `chpath -l Name -i PathID [ -P ] -a Attribute=Value [ -a Attribute=Value ... ]`

   `chpath -h`


`bosboot`：Creates boot image.

 - **Syntax**：For General Use:

   `bosboot -Action [ -d Device ] [ -Options ... ]`

   To Create a Device Boot Image:

   `bosboot {-a -v} [-d Device] [-p Proto] [-k Kernel] [-I|-D] [-l LVdev] [ -L] [-M { primary| standby|both }] [ -T Type] [ -b FileName ] [ -q]`

`smit`：Performs system management.

 - **Syntax**：`smit [ -C | -M ] [ -D ] [ -f ] [ -h ] [ -l File ] [ -o PathName ] [ -p Entity/ValueString ] [ -r RunMode ] [ -s File ] [ -t ] [ -v ] [ [ -m | -n | -d ] FastPath ] [ -X ] [ -x ]`


`lsvg`: Displays information about volume groups.

 - **Syntax**: `lsvg [ -L ] [ -o ] | [ -n descriptorphysicalvolume ] | [ -i ] [ -l | -M | -p ] [ -m ] [ -P ] volumegroup ...`

`lslv`: Displays information about a logical volume.

 - **Syntax**:
  To Display Logical Volume Information

  `lslv [ -L ] [ -l| -m ] [ -n PhysicalVolume ] LogicalVolume`

  To Display Logical Volume Allocation Map

  `lslv [ -L ] [ -n PhysicalVolume ] -p PhysicalVolume [ LogicalVolume ]`

 
`smitty` (`smit -C`): Provides a Curses-based text interface to perform system management.

  - **Syntax**
  `smitty [ -C ] [ -D ] [ -f ] [ -h ] [ -l File ] [ -o PathName ] [ -s File ] [ -t ] [ -v ] [ [ -m | -n | -d ] FastPath ] [ -X ] [ -x ]`


-------
`ps -ef | gpep sync` 查看同步
`df -g` 查看文件大小
`chfs -a size=5G`    修改文件大小
创建LV `smitty mklv`  /`smitty rmlv` 删除LV
`migratepv -l` lv的名字  迁移LV的数据

`lsvg rootvg`  查看PP SIZE:    1024 megabyte(s) 为了建立LV的时候计算

如何创建文件系统 `smitty crfs`   /  `smitty rmfs` 删除文件系统 

如果删不掉 要查看这个LV是否有文件系统挂在 如果有 那需要`umount /nimama`  反之当需要LV和文件系统都创建好以后 就需要把文件系统mount起来


-------

### Device commands

### Installation commands

### IBM　Systems Director agent commands

### IBM Tivoli Montioring agent commands

### IBM Tivoli Storage agent commands

### IBM Tivoli Usage and Accounting Manager agent commands

### IBM TotalStorage Productivity Center agent commands

### Integrated Virtualization Manager commands

### Logical volume commands

### Maintenance commands

### Network commands

### Physical volume commands

### Runtime Expert commands

###Security commands

### Shared storage pool commands

### Standard shell commands

### Storage pool commands

### User ID commands

### Virtual media repository commands

### Virtual terminals commands

### Volume group commands

### Workload manager commands

