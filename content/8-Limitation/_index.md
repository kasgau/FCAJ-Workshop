---
title : "Limitations and Future Developments"
date : 2026-07-30
weight: 8
chapter: false
pre: " <b> 8. </b> "
---


Although the system architecture was successfully deployed to fulfill the workshop objectives, the current setup still exhibits specific technical limitations due to AWS Free Tier constraints and cost optimization boundaries.

## 1. Current Limitations

* **AWS Free Tier Account Constraints:**
  * **Custom Domain & SSL/TLS:** Due to restricted privileges under the Free Tier account, **Amazon Route 53** could not be fully utilized to assign a custom domain name or configure free SSL/TLS certificates via **AWS Certificate Manager (ACM)** for HTTPS (port `443`) termination.
  * **Database High Availability:** **Amazon RDS** is strictly limited to a Single-AZ deployment. The **Multi-AZ** deployment mode (synchronous replication across multiple Availability Zones) is unavailable under basic tier settings, leaving the database tier without automated failover capabilities.

* **Database Query Bottlenecks (RDS Pressure):**
  * As the MonaPerfume e-commerce store relies exclusively on Amazon RDS for all data operations, repetitive user browsing actions (e.g., loading product catalogs and item details) trigger continuous `SELECT` queries. Under high traffic volume, this direct query pattern significantly increases query latency and drives up overall RDS operational costs.

---

## 2. Mitigation Strategies & Future Roadmap

* **Account Upgrade & Security Hardening:**
  * Transition to a standard Pay-As-You-Go AWS account to unlock advanced features.
  * Integrate **Amazon Route 53** with **AWS ACM** to bind a custom domain and terminate HTTPS traffic safely at the Application Load Balancer (ALB).
  * Enable **Multi-AZ** deployment for Amazon RDS to guarantee high availability and seamless automated failover.

* **Implement a Caching Layer using Amazon ElastiCache:**
  * Deploy **Amazon ElastiCache (Redis/Memcached)** as an in-memory caching layer in front of the primary database.
  * Leverage ElastiCache to offload:
    * **User Session State:** Maintain seamless user sessions across auto-scaled EC2 instances.
    * **Temporary Shopping Carts:** Store active cart items in memory before final checkout.
    * **Frequently Accessed Catalogs:** Serve popular product details directly from memory, significantly decreasing RDS query workloads, cutting infrastructure costs, and accelerating user response times.