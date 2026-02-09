# 🛡️ Ingress Shielded API 
> **Securing Kubernetes at the Edge with NGINX Rate Limiting**

![Architecture Diagram](./your-image-lin<img width="2752" height="1536" alt="unnamed" src="https://github.com/user-attachments/assets/5ded09a5-1fa5-4dac-8744-4ced3e1ced8b" />
k.png)

## 🚀 Overview
Filtering malicious activity at the entry point is more efficient than handling it in your code. This project implements an **NGINX Ingress Controller** as a protective gateway for a 3-replica Python API.

### Key Features
*   **Rate Limiting:** Identified and restricts excessive traffic.
*   **Burst Management:** Allows handled traffic spikes before enforcing caps.
*   **High Availability:** 3-replica backend deployment.

---

## 🏗️ Architecture
| Component | Responsibility |
| :--- | :--- |
| **NGINX Ingress** | The "Shield" - Handles Rate Limiting (L7) |
| **K8s Service** | The "Internal Router" |
| **Python API** | The "Backend" - 3 Replicas for stability |

---

## 🛠️ Quick Start

1. **Deploy the API & Service**
   ```bash
   kubectl apply -f advanced-app.yaml
