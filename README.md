# AWS Secure Private Architecture with SSM Session Manager

## Project Overview
This project provisions a secure, private AWS network infrastructure designed to host compute workloads without direct public exposure. Management and shell access are configured strictly via **AWS Systems Manager (SSM) Session Manager**, eliminating the need for public IP addresses, open SSH ports (TCP 22), or bastion hosts.

---

## Architecture Topology

```mermaid
flowchart TD
    subgraph VPC ["fawwaz-vpc (vpc-041a4abfd01e09e54)"]
        subgraph PublicSubnet ["Public Subnet"]
            IGW["Internet Gateway"]
            NAT["fawwaz-nat-gateway (nat-18c1693dbe94a9da3)"]
        end
        
        subgraph PrivateSubnet ["Private Subnet (subnet-00f9de28c2995ee41)"]
            EC2["private-test-server (i-01451e1e2846157a0)"]
        end
    end

    EC2 -- Outbound Port 443 --> NAT
    NAT --> IGW
    IGW --> SSM["AWS Systems Manager Service"]
