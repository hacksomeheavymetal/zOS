## The complete list of z/OS acronyms
- http://www.ibm.com/systems/z/os/zos/bkserv/lookat/
- https://walton.uark.edu/enterprise/IBM/systemZ/downloads/module0/zglossary.pdf (the original [source #1](https://www.ibm.com/support/knowledgecenter/en/zosbasics/com.ibm.zglossary.doc/zglossary.html) and [source #2](https://www.ibm.com/software/globalization/) were removed)

## Basic acronyms and terms
- ACP (Access Control Product) - products such as RACF, ACF2 and TSS.
- APF (Authorized Program Facility) - checks if a given program is authorised to access system sensitive functions, e.g. SVCs or SVC paths.
- BCP (Base Control Program) - z/OS kernel is part of it.
- CICS (Customer Information Control System) - a transaction server (think rollbacks). Used to be able to do internal CICS security, now uses ESM RACF, ACF2 or TSS.
- DASD (Direct Access Storage Device) - device in which the access time is effectively independent of the location of the data.
- DFDSS (Data Facility Data Set Services) - used to copy, move, dump, and restore data sets and volumes.
- DFSMS (Data Facility Storage Management Subsystem) - provides storage, data, program, and device management functions, i.e. disk utility.
- DITTO (Data Interfile Transfer Testing and Operations) - storage media and data maintenance utility.
- DSMON (Data Security Monitor) - produces a set of reports that provide information about the current status of the data security environment.
- Dataset - "file" on a mainframe; logical records (length) instead of bytes, no newlines (there are partitioned, sequential and VSAM datasets).
- EBCDIC (Extended Binary Coded Decimal Interchange Code) - alternative character set to ASCII (https://en.wikipedia.org/wiki/IBM_3270#3270_character_set).
- ESM (External Security Manager) - one of RACF, ACF2 or TSS (see SAF below)(?).
- HFS (Hierarchical File System) - z/OS file system.
- HLQ (High Level Qualifier) - allows to associate an app's configuration dataset with a job name or TSO's userid, or permits to use the default configuration dataset for the app.
- ICSF (Integrated Cryptographic Service Facility) - hardware crypto acceleration, provides the APIs by which applications request the cryptographic services.
- IDTS - `TODO` LDAP for z/os.
- ISHELL (ISPF Shell) - MVS/norton like shell where commands are entered using tabs/panels.
- ISPF (Interactive System Productivity Facility) - norton like dialog manager for interactive applications.
- JCL (Job Control Language) - is a meta-language/virtualization for a lower level programs e.g. asm, c, cobol etc. can be also a program on it's own. Defines how program's input/output/storage etc. will be handled in a very detailed way. it is passed to JES for execution.
- JES (Job Entry Subsystem) - v2 or v3, manages input/execution/output job queues and data, e.g. RJE, NJE and JCL. Feed it with code to be executed e.g. via FTP. The output goes to e.g. printer, tape, dataset etc.  Uses data sets for spooling (in/out).
- LPA (Link Pack Area) - is a virtual storage that contains reenterable routines that are loaded at IPL and can be used concurrently by all tasks in the system.
- LPAR (Logical Partition) - but not in the tradinional meaning. Each LAPR is a separate mainframe and can run different IBM OS (e.g. z/os, s/390, linux).
- NJE (Network Job Entry) - is a protocol to send jobs to other nodes.
- OCSF (Open Cryptographic Service Facility) - `TODO`.
- OMVS - stands for z/OS UNIX System Services, basically a POSIX unix environment on the mainframe that coexists with z/os.
- RACF (Resource Access Control Facility) - default z/OS facility for authentication, RBAC, ACLs, auditing etc.
- ACF2 (Access Control Facitlity) - alternative facility for authentication, RBAC, ACLs, auditing etc.
- RJE (Remote Job Entry) - allows RJE workstations to use JES for job execution.
- SAF (System Access Facility) - similar to PAM (Pluggable Authentication Modules) framework. Delegates requests to the RACF db and/or other ESMs.
- SDSF (System Display and Search Facility) - allows users and administrators to view and control various aspects of the mainframe's operation and system resources. Think ps, kill jobs, syslog etc.
- SVC (Supervisor Call) - is a hardware instruction used to cause an interrupt to request a service from the operating system. SVC is a specific implementation of a system call.
- TSO (Time Sharing Option) is like login sessions on linux.
- TSS (Top Secret System) - alternative facility for authentication, RBAC, ACLs, auditing etc.
- UACC (Universal Access Authority) - is the default access authority that RACF gives to users and groups that are not defined in the profile's access list.
- USS (Unix Services Security) - basically a POSIX unix environment on the mainframe that coexists with z/os.
- USS file - dataset emulated to a byte oriented (no records and no blocks) regular file.
- zFS - z/OS file system.

## Operating Systems for Z architecture
- z/os (zero-downtime os): https://en.wikipedia.org/wiki/Z/OS
- z/vm  (virtual machine): https://en.wikipedia.org/wiki/Z/VM
- z/tpf (transaction processing facility): https://en.wikipedia.org/wiki/Transaction_Processing_Facility
- z/vse (virtual storage extended): https://en.wikipedia.org/wiki/VSE_%28operating_system%29
- Linux on system z: https://en.wikipedia.org/wiki/Linux_on_z_Systems

## Virtualization
- lpar - type one hypervisor (cpu, io channels, !mem virt, can host 1-5 OSs)
- z/vm - type two hypervisor (mem virt, can host 100-1000s of OSs)

## OSs communication
The hypersockets and vswitch - network communication between OSs within the mainframe with near zero net delay.
    
## Syntax of system messages
All messages can be searched for at: http://www.ibm.com/systems/z/os/zos/bkserv/lookat/

  ```
  CCCSnnns    // syntax:
              // C - component
              // S - subcomponent
              // n - msg number
              // s - typ code (a - action, e - error, i - information,
              //    w - warning)
  ```
  
IKJ**** - TSO component messages
  
## The hardware controls (sandboxing/virtual cages)
- Supervisor State Switch - restricts when a program can execute privileged hardware instructions.
- Protect Keys - restrict what memory a program can update or read.
- Address Spaces - restrict processes by running them within dedicated address spaces managed by the kernel (like in other unices). 

## Security sensitive datasets
- SYS1.UADS - if ACP is not used for whatever reason, then definitions in this dataset will be used to grant access to the system.
- SYS1.PARMLIB - contains control parameters for the whole system (similar function to /etc in other unices). The SVCs, Exits, APF-authorization, Program Properties Table, functional subsystems etc. reside in PARMLIB datasets.
- SYS1.NUCLEUS - contains the basic supervisor modules of the system. 
- SYS1.PROCLIB - contains the IBM-supplied JCL procedures used to perform certain system functions.
- SYS1.LINKLIB - contains many of the executable code, also known as modules, for z/OS components and utilities. By default, SYS1.LINKLIB is the first data set in the linklist, which is a collection of libraries containing system and user code. 
- SYS1.LPALIB - ???
- SYS1.SVCLIB - ???
- LPALIST - reenterable routines that are loaded at IPL. Contains SVCs.
  
