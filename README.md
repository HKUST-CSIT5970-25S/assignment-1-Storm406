[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: ARSHAD, Muhammad Hassan
### Student Id: 21080455
### Email: mharshad@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > Phoronix Test Suite was used to measure the computational power of CPU and RAM bandwidth of different instances types. The obtained results for CPU are in MIPS (Million Instruction per second) for both compression and decompression. And for RAM bandwidth, the results are in MB/s (Megabytes per second). 

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro`  | 3514 MIPS/3077 MIPS  | 10575.75 MB/s  |
    | `t2.medium` | 10177 MIPS/5973 MIPS | 20014.96 MB/s  |
    | `c5d.large` | 7450 MIPS/4890 MIPS  | 13682.89 MB/s  |

    > The results show an increase in performance from t2.micro to t2.medium but c5d.large results is lower than t2.medium which is an unexpected result. Maybe large instances are good for heavier or more intensive tasks.

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 3.91 Gbits/sec | 0.310 ms |
    | `m5.large` - `m5.large`   | 4.97 Gbits/sec | 0.247 ms |
    | `c5n.large` - `c5n.large` | 4.96 Gbits/sec | 0.159 ms |
    | `t3.medium` - `c5n.large` | 2.22 Gbits/sec | 0.754 ms |
    | `m5.large` - `c5n.large`  | 3.54 Gbits/sec | 0.455 ms |
    | `m5.large` - `t3.medium`  | 1.77 Gbits/sec | 0.899 ms |

    > When testing the network performance, we can see from above table that the best result is for c5n.large to c5n.large, other same instance type also have good result. But when it comes to different instance type the performance is not that great.

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 22.3 Mbits/sec | 77.294 ms|
    | N. Virginia - N. Virginia | 4.96 Gbits/sec | 0.140  ms|
    | Oregon - Oregon           | 4.93 Gbits/sec | 0.203 ms|

    > Network performance between different region uses public ip address, therefore it has significantly lower bandwidth and higher RTT. Same region were tested with private ip, although public ip did not have much difference.
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
