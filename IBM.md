IBM z13 server

## 一些简称

 - **FRU**: Field Replaced Unit
 - **CPC**: central processor complex

### 存储连接

 - **FICON**: IBM Fibre Connection
 - **FC**: Fibre Channel
 - **FCP**: FIbre Channel Protocol
 
###　网络连接

 - **OSA-Express**



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