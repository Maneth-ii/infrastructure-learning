## Benefits of Virtualization
* **Efficient resource use**: without virtualization each application server needs dedicated hardware for doing the work. companies must purchase new hardware for individual application. 

* **Easier management**: Companies can do automation tasks more seamlessly, and eliminates the time consuming and error prone process of manually configuring and setting up physical computers or servers.

* **Reduce Downtime**:
    - High Availability: If one physical server fails, virtual machines can automatically run on another server in the cluster
    - Live Migration: VMs can be moved from one physical server to another without shutting them down, so maintenance causes no downtime
    - Snapshots: Administrators can save a VM's current state and quickly restore it if something goes wrong. It is like a save point in a video game.

* **Cost Effectiveness**: Virtualization delivers substantial cost savings across multiple areas, such as hardware consolidation, where multiple VMs run on one physical server instead of dedicated hardware for each workload.
This also leads to reduced energy costs with fewer physical servers, lowering electricity consumption for both power and cooling. And correspondingly, fewer physical components mean less hardware to maintain, replace, and support.

## What is a Hypervisor
A hypervisor is software that pools computing resources such as processing, memory, and storage and distributes them across multiple virtual machines running on a single physical host

How It Works: The hypervisor allocates and schedules physical hardware execution for guest VMs. It relies on core OS level components such as memory managers, process schedulers, I/O stacks, device drivers to isolate and run multiple operating systems simultaneously on shared hardware

Type 1 (Bare Metal): Runs directly on physical hardware without a host OS. It offers higher efficiency and is common in enterprise data centers

Examples: KVM, Microsoft Hyper-V, and VMware vSphere.

Type 2 (Hosted): Runs as an application layer on top of a conventional host operating system. It is best suited for personal computers.

Examples: VMware Workstation, Oracle VirtualBox.

Security: Guest VMs are isolated from each other so a compromised VM won't affect the host. However, if the hypervisor itself is compromised, all guest VMs managed by it become vulnerable.

## VM files and Live Storage

persistent files stored on disk that define the virtual machine's configuration and storage

#### VM files
- configuration files: stores VM's virtual hardware specifications (Ram, Cpu , adapter types) , strictly required to boot the VM

- The Virtual Disk Files such as VMDK or VHDX acts as the hard drive containing the guest operating system, applications, and user data

#### Live State
dynamic, temporary state of an active, running virtual machine

- includes the contents of the VM’s Memory, CPU registers, and active network or storage I/O traffic

- Exists only while the VM is powered on or saved in a suspended state

## CPU Virtualization
CPU Virtualization dividing its processing power into virtual CPUs (vCPUs) assigned to Virtual Machines
Hypervisor sits between the physical CPU and the virtual machines, managing access through time sharing and scheduling

### Key Components and Mechanisms
##### vCPUs vs Physical Cores:
A vCPU is not a physical piece of hardware; it is a slice of physical CPU execution time assigned to a VM. A host with 8 physical cores (or 16 threads with hyperthreading) can allocate multiple vCPUs across dozens of VMs.

##### The Role of the Hypervisor:
The hypervisor acts as a traffic controller using a CPU Scheduler. It dynamically allocates time slots on physical CPU cores to execute instructions requested by each VM's vCPU.

##### Hardware-Assisted Virtualization:
Modern processors include dedicated instruction sets (Intel VT-x and AMD-V) designed specifically to handle virtualization. This allows the hypervisor to execute guest OS instructions directly on the physical CPU safely without heavy software emulation overhead

##### CPU Oversubscription:
Because VMs rarely demand 100% CPU capacity simultaneously, hypervisors allow assigning more total vCPUs to VMs than there are physical cores on the host.

##### Common Use Cases & Benefits
- Resource Efficiency: Maximizes hardware utilization by preventing single OS deployments from leaving physical CPU cores idle.

- Workload Isolation: Prevents a CPU-heavy process or crash in one VM from crashing other VMs running on the same host.

- Flexibility: Allows increasing or decreasing a server's processing power (adding or removing vCPUs) with software settings rather than opening up server hardware

## Memory Virtualization
Memory Virtualization is the process where a Virtual Machine thinks it has its own physical memory, but the hypervisor actually manages and allocates the real physical memory of the host computer 

### Why Memory Virtualization is Needed

- Allows multiple VMs to share the same RAM

- Provides isolation between VMs

- Improves resource utilization

- Enables features like VM migration and snapshots