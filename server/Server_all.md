# lec1

- Key features of win server 2016 edition
  - essentials
    - no virtual machines, no cloud services, cannot join a domain
  - standard
    - two type of containers:
      - Hyper-V containers
      - windows server containers
    - defender
  - datacenter
    - clustering up to 64 computers
- Hardware requirements for win server 2016
- Client systems that can be used with win server 2016
- Important general features of win server 2016
- Win server 2016 networking model
- Network protocols used by win server 2016

# AD and Account Management

## AD

> houses information about all network resources (servers, printers, user account, groups of user accounts, security policies)

- replicate **individual properties** instead of entire accounts

### Schema

- defines the objects and the information pertaining(属于) to those objects that can be  stored in AD

- like a small **database** of information associated with that object

- schema information for objects in a domain is **replicated** on every DC

- User account: one class of object in AD that is defined through schema elements unique to that class

  ![image-20191127214138459](D:\Note\server\all.assets\image-20191127214138459.png)

### Global catalog

- stores information about every object within a forest
- the first DC configured in a forest becomes the global catalog server (you can configure another DC to be a global catalog server or designating指定 multiple DCs as global catalog servers)
  - store a full replica of every object within its **own domain**
  - store a **partial replica** of each object within **every domain in the forest** (重要的部分)
  - enables forest-wide searches of data
- purposes
  - serving as the central storehouse of key object information in a forest that has multiple domains
  - providing lookup and access to **all resources** in **all domains**
  - providing replication of key AD elements
  - keeping a copy of the most used attributes for each object for quick access

### DNS

- AD uses Domain Name System(DNS)
  - 网络中至少有一台AD能访问的DNS服务器(通过 **name resolution** 这个方法把 computer and domain host names 转成 dotted decimal addresses)

### Namespace

- a logical area on a network that contain directory services and named objects
- can perform **name resolution**
- AD employs采用 two kinds of namespace
  - contiguous连接的: 每个child object 都包含 parent objet的name
  - disjointed: child name does not resemble像 the name of its parent object

## Directory service

responsible for providing a central listing of resources and ways to quickly find and access specific resources and for providing a way to manage network resources?

## DC

> **servers** that have the AD DS server role installed
>
> contain writable copies of information in AD

- responds to security authentication request
- contains active directory & group policy

- Multi-master replication
  - each DC is equal to every other DC in that it contains the full range of information that composes AD
  - if information on one DC changes, it is replicated to all other DCs

## Member servers

> servers on a network managed by AD that do not have AD installed

## Domain

> Container that holds information about all network resources that are grouped within it
>
> every resource is called an **object**

## Containers in AD

- AD has a treelike structure

- 结构包含: forest, tree, domain, Organization Units(OUs), sites

  ![figure4-9](D:\Note\server\all.assets\image-20191128181323218.png)

### Forest

? AD 包含Forest吗

- 包含一个或多个有相同关系的AD trees
- characteristics
  - tree 可以使用 disjointed namespace
  - 所有tree使用相同的schema
  - 所有tree使用相同的global catalog
  - •Domains enable administration of commonly associated objects, such as accounts and other resources, within a forest?
  - 在同个forest中不同domain之间two-way transitive trusts(双向传递信任) 是自动配置好的
- 

### Tree

### Domain

### OU

store AD objects such as Domain Admins, Domain Users

### Site

## Security groups

## User profiles



