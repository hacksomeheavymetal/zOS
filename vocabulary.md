## The complete list of z/OS acronyms
- http://www-01.ibm.com/support/knowledgecenter/zosbasics/com.ibm.zglossary.doc/zglossary.html?cp=zosbasics%2F14&lang=en
- http://www.ibm.com/software/globalization/terminology
- http://www.ibm.com/systems/z/os/zos/bkserv/lookat/

## Basic acronyms and terms
- Dataset - "file" on a mainframe; logical records (length) instead of bytes, no newlines (there are partitioned, sequential and VSAM datasets).
- USS file - dataset emulated to a byte oriented (no records and no blocks) regular file.
- BCP - Basic Control Program (z/os kernel is part of it).
- HFS/zFS - z/os file systems.
- TSO - Time Sharing Option is like login sessions on linux.
- ISHELL - ISPF Shell MVS-like. Commands entered using tabs/panels (norton like).
- ISPF - Interactive System Productivity Facility (nortol like).
- ICSF - Integrated Cryptographic Service Facility (hardware acceleration).
- OCSF - Open Cryptographic Service Facility.
- IDTS - LDAP for z/os.
- EBCDIC - alternative character set to ASCII. https://en.wikipedia.org/wiki/IBM_3270#3270_character_set
- ACP - Access Control Product like RACF/ACF2/TSS.
- RACF/ACF2/TSS - Resource Access Control Facility/Access Control Facitlity/Top Secret. Authentication, RBAC, ACLs, auditing etc.
- SAF - System Access Facility (looks like PAM framework). Delegates reqs to RACF db.
- ESM - External Security Manager (looks like PAM module).
- CICS - Customer Information Control System is a transaction server (think rollbacks). Uses TransacHons that run programs and the programs access the data. Used to be able to do internal CICS security, now uses ESM RACF, ACF2 or TSS (Top Secret System).
- LPAR - Logical Partition but not in its tradinional meaning. Each LAPR is a separate mainframe and can run different IBM OS (e.g. z/os, s/390, linux).
- NJE - Network Job Entry is a protocol to send jobs to other nodes.
- RJE - Remote Job Entry allows RJE workstations to use JES for job execution.
- JCL - Job Control Language is a meta-language/virtualization for a lower level programs e.g. asm, c, cobol etc. can be also a program on it's own. Defines how program's input/output/storage etc. will be handled in a very detailed way. it is passed to JES for execution.
- JES - Job Entry Subsystem v2 or v3. manages input/execution/output job queues and data for e.g. RJE, NJE and JCL. you feed it with code to be executed e.g. via ftp. output goes to e.g. printer, tape, dataset etc.  Uses data sets for spooling (in/out).
- APF - Authorized Program Facility checks if a given program is authorized to access system sensitive functions (e.g. SVCs or SVC paths).
- SVC - Supervisor Call is a hardware instruction used to cause an interrupt to request a service from the operating system. SVC is a specific implementation of a system call.
- LPA - Link Pack Area is a virtual storage that contains reenterable routines that are loaded at IPL and can be used concurrently by all tasks in the system.
- HLQ - High Level Qualifier permits to associate an app's conf data set with job name or TSO user ID, or permits to use a default conf data set for the app.
- USS - Unix Services Security, basically a POSIX unix environment on the mainframe that coexists with z/os.
- OMVS - --//--
- DFDSS - IBM-licensed program used to copy, move, dump, and restore data sets and volumes.
- SDSF - System Display and Search Facility, allows users and administrators to view and control various aspects of the mainframe's operation and system resources. Think ps, kill jobs, syslog etc.
- DITTO - IBM's Data Interfile Transfer, Testing and Operations Utility 
- DFSMS - provides storage, data, program, and device management functions. disk (a.k.a. DASD) utility.
- UACC - Universal Access Authority is the default access authority that RACF gives to users and groups that are not defined in the profile's access list.
- DSMON - data security monitor produces a set of reports that provide information about the current status of the data security environment.

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
  
