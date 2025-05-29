# ✅ Top 50 OS + Networking Interview Questions

## 🖥️ Operating System Questions

### 1. What is an operating system?
An operating system (OS) is system software that acts as an intermediary between computer hardware and the user. It manages hardware resources, provides a user interface, and offers common services for application software. Examples include Windows, Linux, and macOS.

### 2. What are the main functions of an OS?
- **Process management**: Creating, scheduling, and terminating processes.
- **Memory management**: Allocating and deallocating memory space as needed.
- **File system management**: Organizing, storing, retrieving, and managing data on storage devices.
- **Device management**: Controlling and managing input/output devices via drivers.
- **Security and access control**: Protecting data and resources from unauthorized access.
- **User interface**: Providing command-line or graphical interfaces for user interaction.

### 3. What is a process vs a thread?
- **Process**: An independent program in execution with its own memory space and system resources. For example, running a web browser is a process.
- **Thread**: A smaller unit of execution within a process that shares the same memory space. Multiple threads within a process can run concurrently, such as tabs in a browser.

### 4. What is multithreading?
Multithreading allows a single process to have multiple threads executing concurrently, improving performance by parallelizing tasks. For example, a web browser can load images, render text, and respond to user input simultaneously using multiple threads.

### 5. What is the difference between concurrency and parallelism?
- **Concurrency**: Multiple tasks progress by interleaving execution on a single CPU through context switching. For example, a single-core CPU running multiple applications by switching between them rapidly.
- **Parallelism**: Multiple tasks execute simultaneously on multiple CPUs or cores. For example, a quad-core processor running four threads at the same time.

### 6. What is a context switch?
A context switch is the process where the CPU saves the state of the currently running process or thread and loads the state of the next scheduled process or thread. This allows multiple processes to share a single CPU effectively.

### 7. What is a deadlock? How to prevent it?
A deadlock occurs when two or more processes are waiting indefinitely for resources held by each other, causing a standstill. Prevention techniques include:
- **Resource ordering**: Enforcing a strict order in which resources are requested.
- **Deadlock detection and recovery**: Detecting deadlocks and terminating or rolling back processes.
- **Banker's algorithm**: Allocating resources only if it leaves the system in a safe state.

### 8. What are the necessary conditions for a deadlock?
- **Mutual exclusion**: At least one resource must be held in a non-shareable mode.
- **Hold and wait**: Processes holding resources can request new ones.
- **No preemption**: Resources cannot be forcibly taken from a process.
- **Circular wait**: A circular chain of processes exists, each waiting for a resource held by the next.

### 9. What is virtual memory?
Virtual memory is a memory management technique that uses disk storage to extend the apparent amount of RAM, allowing programs to use more memory than physically available. It enables efficient multitasking and isolation between processes.

### 10. What is paging and segmentation?
- **Paging**: Divides memory into fixed-size blocks called pages. Pages can be mapped non-contiguously in physical memory, simplifying memory allocation and avoiding fragmentation.
- **Segmentation**: Divides memory into variable-sized segments based on logical divisions like code, data, and stack, providing more flexibility but potentially causing fragmentation.

### 11. What is a page fault?
A page fault occurs when a program tries to access a page that is not currently loaded into physical memory (RAM). The OS then loads the required page from disk into memory, allowing the program to continue execution. This mechanism supports virtual memory.

### 12. What is a system call?
A system call is a controlled entry point through which a program requests services from the operating system's kernel, such as file operations, process control, or communication.

### 13. What is a kernel? Difference between monolithic and microkernel?
- **Kernel**: The core part of the OS responsible for managing system resources and hardware communication.
- **Monolithic kernel**: All OS services (file system, device drivers, memory management) run in kernel space, providing high performance but less modularity.
- **Microkernel**: Only essential services run in kernel space; other services run in user space, improving modularity and stability but potentially reducing performance.

### 14. What is user mode vs kernel mode?
- **User mode**: Restricted mode where applications run with limited privileges to protect system stability.
- **Kernel mode**: Privileged mode where the OS kernel runs with full access to hardware and system resources.

### 15. What is process scheduling?
Process scheduling is the OS mechanism that decides which process runs on the CPU at any given time, optimizing CPU utilization and responsiveness.

### 16. What are different scheduling algorithms?
- **FCFS (First Come First Serve)**: Processes are scheduled in the order they arrive.
- **SJF (Shortest Job First)**: Processes with the shortest execution time are scheduled first.
- **Round Robin**: Each process gets a fixed time slice in a cyclic order.
- **Priority Scheduling**: Processes are scheduled based on priority levels.
- **Multilevel Queue Scheduling**: Processes are divided into queues based on priority or type, each with its own scheduling algorithm.

### 17. What is inter-process communication (IPC)?
IPC refers to mechanisms that allow processes to exchange data and synchronize actions, such as pipes, message queues, shared memory, and semaphores.

### 18. What is a semaphore? Binary vs counting
- **Semaphore**: A synchronization tool used to control access to shared resources.
- **Binary semaphore**: Takes values 0 or 1, used for mutual exclusion (mutex).
- **Counting semaphore**: Can take non-negative integer values, used to manage access to a resource pool.

### 19. What is mutual exclusion?
Mutual exclusion ensures that only one process or thread accesses a critical section or shared resource at a time to prevent data inconsistency.

### 20. What is a race condition?
A race condition occurs when the system's behavior depends on the sequence or timing of uncontrollable events, leading to unpredictable results.

### 21. What are threads and how are they managed?
Threads are lightweight units of execution within a process. They can be managed at the user level by thread libraries or at the kernel level by the OS scheduler.

### 22. What is a daemon process?
A daemon is a background process that runs continuously, often providing system or network services without direct user interaction.

### 23. What is swapping?
Swapping is the process of moving entire processes between main memory and disk to free up RAM for other processes.

### 24. What is demand paging?
Demand paging loads pages into memory only when they are needed, reducing memory usage and improving efficiency.

### 25. What is a memory-mapped file?
A memory-mapped file is a file whose contents are mapped directly into the virtual memory space of a process, allowing file I/O to be treated as memory access.

## 🌐 Computer Networking Questions

### 1. What is the OSI model? Explain all 7 layers
The OSI (Open Systems Interconnection) model is a conceptual framework used to understand and implement network protocols in seven layers:
1. **Physical**: Transmits raw bits over a physical medium (e.g., cables, radio waves).
2. **Data Link**: Provides error detection and correction, and frames data for transmission (e.g., Ethernet).
3. **Network**: Handles routing and forwarding of packets (e.g., IP).
4. **Transport**: Ensures reliable data transfer and flow control (e.g., TCP, UDP).
5. **Session**: Manages sessions or connections between applications.
6. **Presentation**: Translates data formats, encryption, and compression.
7. **Application**: Provides network services directly to user applications (e.g., HTTP, FTP).

### 2. What is the TCP/IP model?
The TCP/IP model is a simplified networking model with four layers:
- **Application**: Combines OSI layers 5-7, handling high-level protocols.
- **Transport**: Provides end-to-end communication (TCP, UDP).
- **Internet**: Handles logical addressing and routing (IP).
- **Network Access**: Manages physical transmission and data link protocols.

### 3. What is the difference between TCP and UDP?
- **TCP (Transmission Control Protocol)**: Connection-oriented, reliable, ensures ordered delivery, and error-checked. Used for applications like web browsing and email.
- **UDP (User Datagram Protocol)**: Connectionless, unreliable, no guarantee of order or delivery, but faster and lightweight. Used for streaming and gaming.

### 4. What is IP addressing?
IP addressing assigns a unique numerical label to each device on a network, enabling identification and communication. IPv4 uses 32-bit addresses, while IPv6 uses 128-bit addresses.

### 5. What is subnetting?
Subnetting divides a larger network into smaller subnetworks to improve performance and security. It involves splitting the IP address space using subnet masks.

### 6. What is DNS and how does it work?
The Domain Name System (DNS) translates human-readable domain names (e.g., www.example.com) into IP addresses using a hierarchical distributed database, enabling users to access websites easily.

### 7. What is ARP (Address Resolution Protocol)?
ARP maps IP addresses to physical MAC addresses on a local network, allowing devices to communicate within the same subnet.

### 8. What is DHCP?
Dynamic Host Configuration Protocol (DHCP) automatically assigns IP addresses and other network configuration parameters to devices on a network, simplifying management.

### 9. What is NAT (Network Address Translation)?
NAT modifies IP address information in packet headers while in transit, allowing multiple devices on a private network to share a single public IP address, enhancing security and address conservation.

### 10. What is a socket?
A socket is an endpoint for communication between two machines, identified by an IP address and port number, enabling networked applications to send and receive data.

### 11. What is the difference between a switch, router, and hub?
- **Hub**: A basic device that broadcasts incoming data to all ports (Layer 1).
- **Switch**: Forwards data only to the specific device based on MAC addresses (Layer 2).
- **Router**: Routes data between different networks using IP addresses (Layer 3).

### 12. What is HTTP vs HTTPS?
- **HTTP (Hypertext Transfer Protocol)**: Unencrypted protocol for transferring web pages.
- **HTTPS**: HTTP secured with SSL/TLS encryption, providing confidentiality and integrity.

### 13. What is a 3-way TCP handshake?
The process to establish a TCP connection:
1. Client sends SYN (synchronize) to server.
2. Server responds with SYN-ACK (synchronize-acknowledge).
3. Client sends ACK (acknowledge), establishing the connection.

### 14. What is latency, bandwidth, and throughput?
- **Latency**: Time taken for data to travel from source to destination.
- **Bandwidth**: Maximum data transfer rate of a network.
- **Throughput**: Actual data transfer rate achieved.

### 15. What is a firewall?
A firewall is a network security system that monitors and controls incoming and outgoing traffic based on predetermined security rules, protecting networks from unauthorized access.

### 16. What is a VPN?
A Virtual Private Network (VPN) extends a private network across a public network, encrypting data and providing secure remote access.

### 17. What are common HTTP status codes?
- **200 OK**: Request succeeded.
- **301 Moved Permanently**: Resource has been permanently moved.
- **404 Not Found**: Resource not found.
- **500 Internal Server Error**: Server encountered an error.

### 18. What is SSL/TLS?
Secure Sockets Layer (SSL) and Transport Layer Security (TLS) are cryptographic protocols that provide secure communication over a network by encrypting data.

### 19. What is a CDN?
A Content Delivery Network (CDN) distributes content geographically across multiple servers to reduce latency and improve load times.

### 20. What is DNS spoofing or cache poisoning?
An attack that corrupts DNS cache data, redirecting users to malicious sites instead of legitimate ones.

### 21. What is a MAC address?
A Media Access Control (MAC) address is a unique identifier assigned to network interfaces for communications on the physical network segment.

### 22. What is port forwarding?
Port forwarding redirects communication requests from one IP address and port number to another, often used to allow external access to services within a private network.

### 23. What is ICMP and how is it used (e.g., in ping)?
Internet Control Message Protocol (ICMP) is used for diagnostic and error-reporting purposes, such as the ping command which tests connectivity.

### 24. What is load balancing?
Load balancing distributes network or application traffic across multiple servers to optimize resource use, maximize throughput, and ensure reliability.

### 25. What is the difference between public and private IPs?
- **Public IPs**: Globally routable on the Internet, assigned by ISPs.
- **Private IPs**: Used within private networks (ranges like 10.x.x.x, 172.16.x.x - 172.31.x.x, 192.168.x.x), not routable on the Internet.

## 🧠 Top 20 OS + Networking Concepts/Topics

### 🖥️ Operating System

1. **Process vs Thread**  
A process is an independent program in execution with its own memory space, while a thread is a smaller unit of execution within a process that shares the same memory. Threads enable concurrent execution within a process, improving efficiency.

2. **Multithreading & Concurrency**  
Multithreading allows multiple threads to run concurrently within a process, improving performance. Concurrency refers to managing multiple tasks at the same time, which may or may not run in parallel depending on CPU cores.

3. **Scheduling Algorithms**  
Scheduling algorithms determine the order in which processes access the CPU. Common algorithms include First Come First Serve (FCFS), Shortest Job First (SJF), Round Robin, and Priority Scheduling, each with trade-offs in fairness and efficiency.

4. **Deadlocks and Prevention**  
Deadlocks occur when processes wait indefinitely for resources. Prevention involves ensuring at least one of the necessary conditions (mutual exclusion, hold and wait, no preemption, circular wait) does not hold, using techniques like resource ordering or deadlock detection.

5. **Memory Management (Paging, Segmentation)**  
Paging divides memory into fixed-size pages, simplifying allocation and avoiding fragmentation. Segmentation divides memory into variable-sized segments based on logical divisions like code and data, providing flexibility but potentially causing fragmentation.

6. **Virtual Memory**  
Virtual memory uses disk space to extend physical memory, allowing programs to use more memory than physically available. It provides process isolation and efficient multitasking.

7. **Swapping & Thrashing**  
Swapping moves entire processes between RAM and disk to free memory. Thrashing occurs when excessive swapping degrades system performance, often due to insufficient RAM.

8. **Kernel vs User Mode**  
User mode restricts application privileges to protect system stability, while kernel mode allows the OS full access to hardware and resources.

9. **System Calls**  
System calls provide a controlled interface for programs to request OS services like file operations, process control, and communication.

10. **Synchronization (Mutex, Semaphore)**  
Synchronization mechanisms like mutexes and semaphores prevent race conditions by controlling access to shared resources, ensuring data consistency.

### 🌐 Networking

1. **OSI & TCP/IP Models**  
The OSI model has seven layers describing network functions, while the TCP/IP model has four layers focusing on practical protocol implementation.

2. **TCP vs UDP**  
TCP is connection-oriented and reliable, ensuring ordered data delivery. UDP is connectionless and faster but does not guarantee delivery or order.

3. **IP Addressing & Subnetting**  
IP addressing assigns unique identifiers to devices. Subnetting divides networks into smaller segments to improve management and security.

4. **DNS & DHCP**  
DNS translates domain names to IP addresses. DHCP automatically assigns IP addresses and network configurations to devices.

5. **NAT & Port Forwarding**  
NAT allows multiple devices to share a public IP address by translating private IPs. Port forwarding redirects external traffic to specific devices within a private network.

6. **HTTP Lifecycle & Status Codes**  
The HTTP lifecycle involves request, response, and connection management. Status codes indicate the result of HTTP requests (e.g., 200 OK, 404 Not Found).

7. **Socket Programming**  
Sockets provide endpoints for network communication, enabling data exchange between devices over IP networks.

8. **TCP 3-Way Handshake**  
A process to establish a TCP connection involving SYN, SYN-ACK, and ACK messages between client and server.

9. **Firewalls & VPN**  
Firewalls control network traffic based on security rules. VPNs create secure, encrypted connections over public networks.

10. **Load Balancing & CDN**  
Load balancing distributes traffic across servers to optimize resource use. CDNs deliver content from geographically distributed servers to reduce latency.

11. **Proxy, Reverse Proxy**  
A proxy acts as an intermediary for client requests, while a reverse proxy forwards requests to backend servers, often used for load balancing and security.
