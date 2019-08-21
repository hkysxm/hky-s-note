IBM z13 server

## 一些简称

 - **FRU**: Field Replaced Unit
 - **CPC**: central processor complex
 - **OSC**：Oscillator cards
 - **PPS**：pulse per second
 - **SNTP**：Simple Network Time Protocol
 - **STP**：Server Time Protocol
 - **NTP**：Network Time Protocol
 - **ETS**：External Time Source
 - **SCM**：Single chip module
 - **SC**：storage control
 - **RAS**: Reliability, Availability and Serviceability
 - **IFL**: Integrated Facility for Linux
 - **ICF**：internal coupling facility
 - **zIIP**:System z Integrated Information Processor
 - **CBU**：Capacity Backup
 - **MCU**: memory controller units
 - **SMT**: Simultaneous multithreading
 - **SMID**: Single-instruction multiple-data

### 存储连接

 - **FICON**: IBM Fibre Connection
 - **FC**: Fibre Channel
 - **FCP**: FIbre Channel Protocol
 
###　网络连接

 - **OSA-Express**

### 其他链接

 - **FSP**：Flexible Service Processor

## Frames & drawers

### A Frame  A柜

 - Two Support Element（SE）servers
    In previous z System servers, the SEs were notebooks in the Z Frame. For z13 servers, the SEs are replaced with the 1U servers, which are mounted at the top of the 42U EIA frame. 

 - Two optional intergrated battery features (IBFS)
    Provice the function of a local uninterrupted power source.

 - One PCIe I/O drawer
    Presence of it depends on the server's I/O configuration.

 - Two System Control Hubs (SCHS)
    Replacement of the Bulk Power Hubs that were used in previous z Systems servers.

 - Up to four CPC drawers
    Depends on the model number of the z13 server. Additional ones are filled up from the bottom to the top. 

 - Cooling units
     > We use water-cooling

    Two Water Conditioning Units (WCUs) are installed. The WCUs are connected to a customer-operated (data-center) chilled water supply. 


### Z Frame  Z柜

 - Two or four optional IBFs
    Depends on the number of bulk power regulators that are installed. Always installed in pairs.

 - Bulk powerregulators (BPRs)
    Number of BPRs varied depending on the configuration of the z13 server. 

 - Keyboard and Display tray
    In front of the I/O drawer slots, contains the keyboards and the displays thay ae connected to the SEs(Support Elements).

 - Up to four drawers
    Can be any combination of up to two I/O drawers & up to four PCIe I/O drawers:
     - PCIe I/O drawer is used for all new installations or can be carried forward through miscellaneous equipment specification (MES).
     - The I/O drawer itself can be carried forward only with an MES from z196 or zEC12. 

 - An optional overhead power cable
    When this feature is ordered, it is present on the Z frae. The top I/O exit cabling feature must also be installed in this case. 

### I/O drawer & PCIe I/O drawer
Each CPC drawer has 10 PCIe Generation3 fanout slots & four InfiniBand fanout slots to support two types of I/O infrastructure for data transfer:

 - PCIe I/O infrastructure: 16 GBps
 - InfiniBand I/O infrastructure: 6 GBps

### PCIe I/O infrastructure
Use the PCIe fanout to connect to the PCIe I/O drawer, which can contain the following features:

 - FICON Express16S
 - FICON Express8S
  - OSA-Express5S 10 Gb Ethernet
  - OSA-Express5S Gb Ethernet
  - OSA-Express5S 1000BASE-T Ethernet
 - OSA-Express4S features
  - OSA-Express4S 10 Gb Ethernet
  - OSA-Express4S Gb Ethernet
  - OSA-Express4S 1000BASE-T Ethernet
 - Crypto Express5S feature
    Each feature holds one PCIe cryptographic adapter. Each adapter can be configured by the installaton as a Secure IBM Common Cryptographic Architecture (CCA) coprocessor, as a Secure IBM Enterprise Public Key Cryptography Standards (PKCS) #11 (EP11) coprocessor, or as an accelerator.
 - Flash Express
    Each Flash Express feature occupies two I/O slots, but does not have a CHPID type. Logical partitions (LPARs) in all channel subsystems (CSSs) have access to the features.
 - 10 GbE Remote Direct Memory Access (RDMA) over Converged Ethernet (RoCE) Express
  Has a 2-port card, and up to 31 LPARS can share a physical adapter.
 - zEnterprise Data Compression (zEDC) Express
 The Enterprise Data Compression Express feature occupies one I/O slot, but it does not have a CHPID type. Up to 15 partitions can share the feature concurrently.

## CPC drawer

 - **in the **A frame**
 - One CPC drawers contains:
   - 8 single chip modules(SCMS)
   - memory
   - symmetric multiprocessor (SMP) connectivity
   - connectors to support PCIe I/O drawers (through PCIe fanout hbs)
   - I/O drawers through InfiniBand features
   - coupling links to other CPCs.
 - CPC drawer is divided in to 2 nodes. Each node contains:
   - Three 8-core processor unit (PU) SCMS with *6/7/8 active cores (depending on the machine model)*
   - One storage controller SCM, with a 480 MB L4 cache.
   - Five DDR3 dual inline memory module (DIMM) slots per memory controller, for a total of up to 10 or 15 per node.
 - Each CPC drawer contains two nodes, which altogether consist of the following components: 
   - Six 8-core PU SCMs, with 39 or 42 active PUs, depending on the model
   - Two Storage Controller SCMs, with 960 MB L4 cache total.
   - DIMMs plugged in to 20 or 25 DIMM slots, providing 320 - 3,200 GB of physical memory and 256 - 2,560 GB of addressable memory.
   - Ten PCIe Generation 3 (PCIe Gen3) slots for PCIe I/O drawer fanouts or PCIe coupling links fanouts.
   - Four GX++ slots for IFB fanouts or InfiniBand coupling fanouts
   - Two flexible service processor (FSP) cards for system control.
   - Two DC converter assemblies (DCAs) that provide power to the CPC drawer. Loss of one DCA leaves enough power to satisfy the drawer’s power requirements (n+1 redundancy). The DCAs can be concurrently removed and replaced (one at a time).
   - Water-cooling manifold for PU chips.

### Oscillator

 - 2 oscillator cards (OSCs): One primary & one backup
 - Primary OSC fails =>secondary
   - secondary detect the failure
   - take over transparently
   - continue to provide the clock signal to the CPC
 - 2 Oscillator have Neill-Concelman (BNC) connectors that provide pulse per second signal (PPS) synchronization to an external time source with PPS output
 - The SEs provide the Simple Network Time Protocol (SNTP) client function. 


### System control 

 - Various system elements are managed through the FSPs.
 - Each FSP card has: two ports to connect to two internal Ethernet LANs, through system control hubs (SCH1 and SCH2)
 - FSPs communicate with the SEs and provide a subsystem interface (SSI) for controlling components

### CPC drawer power
 - Each CPC drawer gets its power from two DCAs
 - DCAs provide the required power for the drawer in an n+1 configuration
 - Loss of one DCA leaves enough power to meet power requirements for the entire drawer
 - DCAs can be concurrently serviced, and are accessed from the rear of the frame A

