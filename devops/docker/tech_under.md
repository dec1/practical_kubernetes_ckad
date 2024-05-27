## Underlying Tech
3 features of linux are essential for containers/images

### 1). Union Filesystem: 
-   Efficiently layers filesystems for container images (e.g. OverlayFS).

### 2). Process Isolation
Cgroups and namespaces, allow you to put a process into different (independent) sets
- A single process can be in at most 1 of each (5) namespace sets, and one (of each of many) cgroup sets
- The sets may coincide, which is  whats done to create the "illusion" of containers


- #### a). Namespaces:
    -  **whats visible** for a process 
        - Partitions various system resources (for processes
            - allowing sets of processes to operate with their own isolated view of the system
        #####
        - Stops one process in one set causing trouble for this in aother another by:
            - using too much cpu, memory, storage, network
            - corrupting memory or files of another process
            - sending another process bad data or too many requests
    
        ##
        -  Isolates 5 linux system **Aspects** (ie namespace **types**/sets),
            -  so processes in each ns have independent version of given aspect, from processes in any other ns
                
                ####
                - 1). **pid**  
                    - process **identifiers** (of running processes) in any ns are indep of those in any other ns
                    - process can be created in specific namespace 


                ##### 
                -  2). ***net***   
                    - network **stack** (interfaces, routing table, firewall)
                    - only processes in given ns can use network stack of that ns
                        - and thus communicate directly with each other via tcp/localhost
                    - processes in different network namespaces require additional configuration to communicate
                        - e.g. [virtual ethernet devices](../../network/interafce.md) 
                ##### 
                -  3). **mnt**   
                    - processes in the same mount namespace see the same mounted **file systems** at the same mount points

                ##### 
                -  4). **ipc**   
                    - only processes in same ns can communicate with each other via ipc (eg shared memory) 
                

                #####             
                -  5). **uts**   
                    - allow a process in given ns to see
                        - **host** - (host name and domain **name**) as different from what processes in other ns do

- #### b). Cgroups (Control Groups)
    - **how much** process  **can use**
    - Limits and manages resource usage  of containers.
    - Each process can be assigned a cgroup controller of given type:
        - CPU
        - Memory

