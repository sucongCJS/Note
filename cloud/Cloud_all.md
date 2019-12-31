# Cloud Computing

> set of systems connected **over Internet** to support a **dynamically scalable** infrastructure for **storage** of applications and data
>
> 
>
> storing and accessing data and programs over the Internet instead of your computer hard drive. 

## Advantage

- **reliability**
  - (cloud-based storage) automatically replicate data to another data repository
- **scalability**
  - scaling of resources on demand
  - **Resource Pooling**
    - 资源池共享，弹性，按需求、按功能分配 
    - sharing resources by large number of organisations can save cost for each organisation
  
- **cost** of hosting applications, storing data, processing and computing is decreased
- **security**
  - **specialists** who are experts in cloud security
  - immediate deployment of **software** **patches** by cloud provider
  - **timeliness of incident response**: cloud provider has expertise to quickly deal with security concerns
- make better use of hardware(virtualisation)
- **Outsourced server management**
  - do not have to maintain

## Disadvantage

- cloud provider has access to customer’s data

## Cloud Type

![image-20191203231707542](D:\Note\cloud\Cloud_all.assets\image-20191203231707542.png)

### Public

> for public, customer share same resources and same level of security

- example
  - Ali Cloud
- pay as you go

### Private

> for one organisation

- example
  - Henu Cloud
- greater control for security
- expensive

### Community

> for multiple organisations with common interest

- example
  - 中国高校云

### Hybrid

> public clouds mixed with private cloud

## Service Type

![saas-vs-paas-vs-iaas-breakdown](D:\Note\cloud\all.assets\saas-vs-paas-vs-iaas-breakdown.jpg)

### IaaS

> supply for data centre space, physical or virtual servers, storage system, network
>
> 
>
> virtual data centre in cloud

- 只提供虚拟主机(服务器集群)
- example
  - Amazon, Vultr

### PaaS

> supply of foundational hardware technology (server, DB, OS, runtime, network, middleware)

- benefits
  - customer: not concerned about hardware or OS upgrades but instead about own applications
  - provider: manage hardware, software
- example
  - LAMP, AWS

### SaaS

> only one instance of service run on cloud, which supports several end users

- benefits
  - customer: doesn’t need to upfront purchase servers of software
  - provider: **hosting** and **maintenance** of only one application
- example
  - salesforce

# Virtualisation

> the use of hardware and software to create the **perception** that one or more entities exist, which are **not physically present**

- using virtualisation, we can run multiple OS **simultaneous** in one  desktop computer

## Advantages

- increased **device** utilisation
- decreased device **footprint**
- decreased **power** consumption
- simplified OS and application **administration**
- ease of software **provisioning** and **patch releases**
- device and **storage** scalability
- increased user **access** to key resources
- increased flexibility in **supporting multiple OS** environments
- improved use and management of **software licenses**
- improved disaster **recovery** and business continuity

## Disadvantages

- not all applications are suited for virtualisation
- adds slight **overhead**, slow
- staff is required to understand virtualisation process

## Server Vtlst

> making one server appear as many

- each virtual server may run the same or different OS

- benefits
  - greater **CPU** utilisation
  - smaller equipment **footprint** (占用空间)
  - less **power** consumption
  - support for multiple **OS**

## Desktop Vtlst

> allow user to switch between multiple OS on the same computer. 

- guest OS, host OS


### virtual desktop

> a desktop computer that runs two or more OS

- advantage
  - a single desktop computer can simultaneously run multiple OS
  - reduced need for duplicate **hardware**
  - less **power** consumed

## VPN

> virtual networks
>
> virtual private network

- create the illusion that a user is connected directly to a company network and resources, although no such physical connection may exist

- let network administrators to **segment a network**, making different departments appear to have their own separate networks. 

## VLAN

> virtual local-area network

- use **special routers** to **segment** part of the physical network in such a way that the group appears to have its **own private network**

## Virtual Storage

> the pooling of physical storage from **multiple network storage devices** into what appears to be **single storage device** that is managed from a central console

- **Using abstract, or logical, disk drives or file systems, or a database interface** to provide users (and applications) with **access to scalable and redundant physical storage through**. 

## Not Suitable Situation

- applications with **unique hardware requirements**
- graphics-intensive application
  - virtual device drivers will slow down the I/O processing

## OTHER

### green computing

- power off devices when they are not in use
- power up energy-intensive devices(laser printers) when needed
- use notebooks instead of desktops
- use computer’s built-in **power management features**
- minimise printing
- dispose of e-waste in compliance with government regulations

### blade servers

- in the rack(挂物架) with many other servers
- reduces server’s physical **footprint**
- easier to cool
- reduces **power** consumption

# Cloud Data Storage

## SAN

> Storage Area Network
>
> 直接把存储设备接到主机上, 没有文件系统, 相当于一个硬盘(disk), 但不是一个硬盘

## NAS

> Network-attached storage
>
> 文件系统

- present cloud-based storage as mountable devices, which may replicated in the cloud to meet a company’s data redundancy needs

### advantages

- **reliability**
  - data striping across multiple volumes within the device, if one fail, the data striping would maintain the data and allow **reconstruction** of the file contents
- **performance**
  - NAS device does not run a complete OS, it is just a file system
- **compatibility**(兼容性)
  - support common file system
- ease of performing **backups**
  - for example, within a home, all devices can easily access and back up files to a NAS device

## Cloud-Based Storage

> 云端的NAS

- **accessible ways**
  - through a web **browser** interface
  - through a mounted **disk** drive
  - through a set of **API** calls

- example
  - 网盘

### Advantages

- **scalability**
  - scale storage capacity
  - pay for use
- **reliability**
  - provide automatic data replication to another cloud-based data repository
- **ease of access**
  - support web-based access to file from any place, at any time, using a variety of devices
- **ease of use**
  - let users map a drive letter to the remote file storage area and then access the file through the use of a logical drive

### Disadvantages

- performance
  - Network delay, not as fast as local drives
- security
  - some users…
- data orphans
  - users may abandon confidential data in cloud storage

## Cloud-Based Backups

### Advantage

- can **schedule** when backup operations are to occur

- backed up in an **encrypted** format
- retrieve backup files from the cloud

## Cloud-Based Database

### Advantage

- **scalability**
  - scale dynamically to meet customer needs
- **availability**
  - normally reside on redundant hardware
- reduced administration 
  - provider maintains the DB version updates and patches

### Disadvantage

- high data redundancy
  - replicate data in order to increase data availability
- security
- performance
  - not as fast as local DB

## Cloud-Based File System

### File System

- copy, delete, create, move files between folders, the file system is performing the work
- locally

### CFS

> cloud-based file system

- allow users or programs to manipulate files residing in the cloud

## OTHER

### data replication

- using cloud-based NAS(network-attached storage) devices and cloud-based DB, companies can replicate key data within the cloud

  ![image-20191204115742676](D:\Note\cloud\Cloud_all.assets\image-20191204115742676.png)

# IaaS

- provide: server, storage, network
  - IaaS provider provides computing hardware resources
  - customers manage the hardware and the software
- other thing that must be provided
  - access high-speed and redundant **Internet** service 
  - efficient **cooling** system
  - using **power** generator to provide UPS in the short and long term
  - **file** extinguishing system
  - administrative **staffing** to support hardware, networks, OS

## Advantage

- reduced **hardware** **cost**
- on-demand, pay-as-you-go **scalability**
- ease of hardware **scalability**
- reduction of IT **staff**
- suitable for ad hoc test environments
- allows complete system **administration** and **management** 

## Co-location

> creating a duplicate data centre at a remote location to reduce the risk of **single point of failure**

- one of the data centres fail, the other can immediately take over operations

### Advantage

- improves **performance** through a distributed workload
- make it difficult for the company to **downtime** due to power loss from a blackout or brownout
- make the company **less affected by fire**, natural disaster and terrorism. 

### Disadvantage

- increase the **costs**

## Load Balancing

> share requests across multiple servers

- use a server to **route traffic** to multiple servers which, in turn, share the **workload**. 

  ![image-20191204115139912](D:\Note\cloud\Cloud_all.assets\image-20191204115139912.png)

### Replicated DB

![image-20191207204233584](D:\Note\cloud\Cloud_all.assets\image-20191207204233584.png)

- load balanced system often replicate DB on multiple servers for data redundancy
- each DB sends data updates to the other to keep the data in sync between the servers

## Server Type

- **Physical server**
  - actual hardware is allocated for the customer’s dedicated(专用的) use
- **Dedicated Virtual server**
  - the customer is allocated a virtual server, which runs on a physical server that **may or may not have other virtual servers**. 
- **Shared Virtual server**
  - the customer can access a virtual server on a device that **may be shared with other customers**. 

# PaaS

- provide: servers(virtual servers), OS, DB, developer tools, network support
- provide a collection of hardware and software resources that developers can use to **build and deploy applications** within cloud
  - platform provider manage hardware and software
  - developer focus on their applications

## Advantage

- developers don’t need to buy and maintain hardware or install OS, DB, just focus on the applications
- **scalability**
  - the computing resources can scale on demand
  - the company can pay for only resources it consumes
- developer can **quickly deploy** their web-based solutions
- lower **total cost of ownership**(总持有成本低)
  - don’t need to purchase and maintain expensive hardware for server, power, and data storage
- lower **administration** overhead(开销)
  - the employees of cloud provider will administrate the system software well
- more **security**, more current system software
  - the cloud administrator is responsible for maintaining software version and patch installations

## Disadvantage

- some developers and administrators **want finer control** over the underlying systems
- data **security**
- challenges to **integrating** cloud solution with legacy(遗留的) software
  - on-site solution and cloud-based solution
- risk of **breach**(违约) by the PaaS provider
  - if the company providing the PaaS service fail to meet agree-upon service levels, performance, security, and availability may be at risk, and moving the application may be difficult. 

# SaaS

> a solution model in which users use a web browser to access software, programs, and user data in the cloud

- provides a cloud-based foundation for software on demand
- users can access web-delivered content through a web browser
- the software can reside in any deployment-model clouds

## Advantage

- don’t need for an on-site data centre
- don’t need for application **administration**
- **scalability**
  - allow customers to pay on demand for software use
  - offer application, processor, data storage scalability
- **availability**
  - offer device-independent access to applications
- **reliability**
  - increase disaster recovery and business continuity

## Disadvantage 

- security
- difficult or expensive to **customise** the application

## OpenSaaS

- SaaS application created using an **open-source programming language** and designed to run on an **open-source OS and DB**
- if a solution is open source, it will be easier for them to move the data to a different application if the future if the current solution fails to meet their needs

## Mashups

>  A mashup is a technique by which a website or web application uses two or more Web services or public APIs to create a new service. 

## SOA

> Service-oriented architecture

- an application development methodology with which developers create solution by **integrating one or more web services**. 
- describes the major components that comprise a system, their relationship, and the information the components exchange

- 开发SaaS应用的一种模型, 开发理念

松耦合, 水平可扩展

## Web Services

> web service consists of one or more  functions that a program can call to **accomplish a specific task**, and **return a specific result** normally

- each function has a unique name and may receive zero or more **parameter** values

- developers refer to a set of web services as an **application program interface**(API)
- example
  - return the weather conditions for a specific zip code 
  - return real-time traffic conditions for a road or highway
- some developers refer to web  services as remote-procedure calls

### Operation

1. a program running on one computer calls a web service
2. a message, possibly containing parameter values, is sent across the network, using **http** protocol, to the computer housing the web service. 
3. that computer, performs its processing and normally returns a result to the caller

### Advantage

- **ease of code reuse**
  - distributed nature
  - saves development and testing time and ultimately reduces costs
- **interoperability**
  - 互操作性
  - they can be called from programs using a variety of programming languages
- **Black Boxes**
  - describes a module for which developers do not care how the processing is performed, but know that the code will produce predictable results when provided valid inputs
  - web service is a black box, the developer trust the web service will function consistently with valid input. 

### Disadvantage

- because web services require network operations, a web service will be considerable **slower** than a program’s call to a function that resides on the same computer

### & SOA

- within SOA, programs make **remote-procedure calls** to web services

### Scaling

- using **load-balancing** model, web service solution is **scalable**

### Coupling

> 耦合

- describe the degree of dependence between a calling program and the web service
- ideally, to use a web service, a program needs to know
  - the **location** of the web service(URL)
  - the **name** of the functions the web service provides
  - **parameters** the program can pass to the functions
- programs and web services are said to be loosely coupled
  - because of loosely coupled, it is possible for developer to update a web service with a newer version
  - because of loosely coupled, programs that use the service can use the new version immediately without any modifications

### WSDL

> web service description language

- the web service uses a WSDL file to describe  the web service and its methods
- programs that use the web service will use the WSDL file to determine the available function, parameter types





# AWS

5中服务

bucket: 存储桶

storage class: 

front

SMS: 自动邮件



DynamoDB



MapReduce



work flow rules



# History

## Mainframe Computers

- large capital investment for data-centre-based computers
- large, expensive disk and tape storage systems that often provided only limited storage capacity
- terminal
- limited computer-network inter connectivity

## Personal Computers

## LAN

## ISP





