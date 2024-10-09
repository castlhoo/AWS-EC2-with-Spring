
# 🚀 AWS EC2 with Spring Boot, Docker & JMeter Stress Test

The combination of AWS EC2, Spring Boot, Docker, and JMeter Stress Testing is essential for ensuring that applications can handle real-world demands in cloud environments. AWS EC2 provides scalable, on-demand cloud infrastructure, allowing applications to handle spikes in traffic without downtime. Spring Boot is used to build microservices or standalone applications, making it ideal for creating modular services that can be independently scaled. Docker ensures consistent deployment across different environments, reducing the risk of environment-specific issues during production deployment. JMeter is employed to simulate high traffic loads and stress-test these applications, helping to identify bottlenecks, optimize performance, and ensure that the system can handle thousands of concurrent users, which is critical in real-world scenarios like high-traffic promotions or sales events. This combination allows organizations to deploy, monitor, and scale applications efficiently, ensuring performance and reliability under varying traffic loads.

## 🌐 1. Setting Up EC2 (Public)

### 1.1 Create a VPC
A Virtual Private Cloud (VPC) is required to isolate your EC2 instances and control network traffic.

![VPC](https://github.com/user-attachments/assets/8534b9c8-178c-4c02-8ed3-4927f62b61dc)

### 1.2 Create a Subnet
Subnets allow you to partition your VPC and assign resources for better traffic management.

![Subnet](https://github.com/user-attachments/assets/f05fd257-3779-42c1-8ad0-52e795e0cb3f)

### 1.3 Create a Route Table
A route table ensures that your subnet traffic can be routed properly.

![Route Table](https://github.com/user-attachments/assets/2aad6964-1715-41bf-949d-d844f8fba374)

Assign the subnet to the route table.

### 1.4 Create an Internet Gateway
This allows your EC2 instances to communicate with the internet.

![Internet Gateway](https://github.com/user-attachments/assets/fcc19ebb-3bc2-4ed5-8078-4ef622cb4336)

Attach it to the VPC.

### 1.5 Configure Route Table for Gateway
Update the route table with the new gateway to allow internet access.

![Route Table Gateway](https://github.com/user-attachments/assets/9f6ebf42-193f-4957-9974-03dc4ddbfabf)

### 1.6 Complete VPC Setup
You now have a fully configured VPC with an internet gateway.

![VPC](https://github.com/user-attachments/assets/9d76560f-0084-4a55-a15e-23e1e0ae8c90)

### 1.7 Create a Security Group
Create a security group that allows HTTP and SSH access. Ensure that the inbound rules are set to `0.0.0.0/0` for both protocols.

![Security Group](https://github.com/user-attachments/assets/4dabb054-59b3-486d-ad7c-969aa5e194f3)

### 1.8 Launch EC2 Instance
Select the appropriate OS (Ubuntu for this tutorial), and configure the instance.

![EC2](https://github.com/user-attachments/assets/767705f9-363f-4193-ad29-0107c96de80e)

### 1.9 Connect to EC2 via SSH
Use the public IP address to connect to your EC2 instance using an SSH client like MobaXTerm.

![MobaXTerm](https://github.com/user-attachments/assets/18b1265c-ad68-4a76-8964-72b47fea96a5)

---

## 🖥️ 2. EC2 Stress Test

### 2.1 CPU Stress Test
Use the `stress` tool to simulate a high CPU load on your EC2 instance.

```bash
stress --cpu 2 --timeout 60
```
This command stresses 2 CPU cores for 60 seconds.
![image](https://github.com/user-attachments/assets/c1c44dab-d152-40da-8c1f-999ef82d0d80)

### 2.2 Network Stress Test
Use `iperf3` to simulate network stress by creating multiple parallel streams.

```bash
iperf3 -c <IP Address> -t 60 -P 8
```
This test runs for 60 seconds with 8 parallel streams.
![image](https://github.com/user-attachments/assets/fff1c269-cf6c-4122-93f8-639b0c158bb5)

---

## 🚢 3. Docker Setup and JMeter Test

### 3.1 Pull Docker Image
Download the necessary Docker image on your EC2 instance.

![Docker](https://github.com/user-attachments/assets/d2420190-7fc2-40e2-9102-a0ddfbecc491)

### 3.2 Spring Boot Port Configuration
Add inbound rules for port 9090 in the security group to allow access to your Spring Boot application.

![Port 9090](https://github.com/user-attachments/assets/43257038-f0f5-414a-b663-eb6d93218c0f)
![Spring Boot](https://github.com/user-attachments/assets/4c2e4a4e-9016-4ba5-acb3-d479ec70b70f)

### 3.3 Run Spring Boot Application
Launch your Spring Boot application using Docker.

![image](https://github.com/user-attachments/assets/f3cf1694-c424-43cb-aca1-add4ae142041)

---

## 🧪 4. JMeter Test
### Test Scenario
> One company on Ancestor Love (a service matching platform for ancestral grave cleaning, lawn mowing, and garden maintenance) is running a special promotion for the Chuseok holiday. The promotion offers an 80% discount for the first 5 customers. As a result, approximately 1,0000 users are expected to visit the promotional post, causing a traffic surge.


### 4.1 Install JMeter
Install JMeter on your EC2 instance for stress testing.

![JMeter](https://github.com/user-attachments/assets/53e8781a-b141-4c18-8be4-7dfbe3e5953e)

### 4.2 Thread Group Configuration
Set up a thread group in JMeter to simulate 1,000 users over 30 seconds.

![Thread Group](https://github.com/user-attachments/assets/5b6f32de-8eb9-4aea-aba9-7d44609655b5)

### 4.3 HTTP Request Configuration
Configure the HTTP request to simulate users accessing the promotion page.

![HTTP Request](https://github.com/user-attachments/assets/5f99d210-0ecd-4404-9cc3-96d3898206b8)

### 4.4 Test Results

#### First Image
![image](https://github.com/user-attachments/assets/ea5aefb9-a2ba-494c-812e-d7c28c871724)
The green line shows failed requests, and the red line shows successful requests over time. As time progresses, the number of failed requests increases significantly, particularly between 17 and 19 seconds.

#### Second Image
![image](https://github.com/user-attachments/assets/b4193639-cd8e-4e13-b583-115bb8c5f4bb)
Key statistics:
- Total samples: 18,070
- Average response time: 2161 ms
- Error percentage: 30.83%
- Throughput: 977.9 requests/sec

#### Third Image
![image](https://github.com/user-attachments/assets/2e155619-682a-4a5e-b247-27bef011c52c)
Response time increases steadily as the test progresses, indicating performance degradation over time.

### Conclusion
The test results show that the server struggled to handle the load, leading to high error rates and increased response times. To resolve this, consider:

1. **Scaling the server** (CPU/Memory)
2. **Auto-scaling** based on traffic
3. **Load balancing** with AWS ELB
4. **Optimizing application and database performance**
5. **Caching and using CDN** for static content

---

## 🔧 Troubleshooting

### 1. Out of Memory Errors: HEAP Memory Reconfiguration
When facing out-of-memory errors, it's necessary to adjust the HEAP memory settings in JMeter.

![Memory Error](https://github.com/user-attachments/assets/9fb4dac6-feaa-4a1a-9830-78691a0f5a25)
![Heap Memory Reconfiguration](https://github.com/user-attachments/assets/ff634822-e7a0-44bb-8a8b-968f0a1924ae)

### 2. Successful Installation & Execution
After adjusting the HEAP memory settings, JMeter should be successfully installed and running.

![Successful Execution](https://github.com/user-attachments/assets/53e8781a-b141-4c18-8be4-7dfbe3e5953e)
