[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/0JZKkp5C)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, March 1st, Friday

---

### Name: Xu Zizhao
### Student Id: 20969874
### Email: zxudh@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > The tool is Phoronix Test Suite. I did not config (i.e., just installed, used its default configuration parameters). For CPU measurement, the task is pts/compress-7zip, which means let it execute 7-zip compression; the value is MIPS, meaning Million Instructions Per Second, represents the CPU processing speed. For Memory measurement, the task is pts/ramspeed, there’re some different options and I chose to let it execute copy integer task; the value is MB/s, meaning Million Bytes per Second, represents the memory processing speed.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?
    >  Yes, the performance of EC2 instances increase commensurate roughly with the increase of the number of vCPUs and memory resource, because:
For t2.micro, it has 1vCPU and 1GiB memory; For t2.medium and c5d.large, both have 2vCPU and 4GiB memory. We can see that t2.micro’s performance is significantly weaker than t2.medium and c5d.large, and, t2.medium and c5d.large’s performances are close.

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |        3793         |          10965.11          |
    | `t2.medium`  |      8390           |        17077.64            |
    | `c5d.large` |       8033          |         14419.03           |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

   >  Same type performance: For t3.medium, the TCP bandwidth is relatively weak, but RTT is OK. For m5.large, the TCP bandwidth is relatively strong, but RTT is relatively weak. For c5n.large, the TCP bandwidth is relatively strong, and RTT is also strong. Different type performance: For t3.medium - c5n.large, both TCP bandwidth and RTT are stronger than two same type t3.medium and weaker than two same type c5n.large. For m5.large - c5n.large, both bandwidth and RTT are weaker than two same type m5.large and two same type c5n.large. For m5.large - t3.medium, both bandwidth and RTT are weaker than two same type m5.large and two same type t3.medium.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |    3.90Gbits/sec            |   0.287       |
    | `m5.large` - `m5.large`   |    9.53Gbits/sec            |   0.324       |
    | `c5n.large` - `c5n.large` |    9.53Gbits/sec            |   0.169       |
    | `t3.medium` - `c5n.large` |    4.34Gbits/sec            |   0.205       |
    | `m5.large` - `c5n.large`  |    2.43Gbits/sec            |   0.658       |
    | `m5.large` - `t3.medium`  |    2.09Gbits/sec            |   0.755       |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

3. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.
    
    >  When deployed in the same region, the performance is strong. But when deployed in different region, the performance of both TCP bandwidth and RTT are significantly far weaker than in the same region.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |     26.6Mbits/sec           |   61.094       |
    | N. Virginia - N. Virginia |     4.66Gbits/sec           |   0.300       |
    | Oregon - Oregon           |     4.78Gbits/sec           |   0.159       |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
