# The-Shielded-API-Ingrees-controller-
The next project is the "Secure &amp; Resilient Gateway." In this project, we will add Rate Limiting (to prevent spam) and Custom Error Pages (to make it professional). This is a real-world scenario where you protect your 3–5 node cluster from being overwhelmed.
Advanced Kubernetes Ingress with Rate Limiting & Traffic Control
📖 Overview
In a production-ready 3-5 node Kubernetes cluster, you cannot just open your doors to everyone. This project demonstrates how to build a Secure Gateway using the NGINX Ingress Controller.

Instead of letting "spam" or "attack traffic" hit our application and waste CPU/RAM, we use the Ingress Controller as a Shield. It identifies the visitor and limits their speed before the request even reaches our backend.

🏗️ Architecture
Infrastructure: Multi-node Kubernetes Cluster (Kind/Bare Metal/Cloud).

The Entry Point: NGINX Ingress Controller (The "Security Guard").

The Application: A 3-replica Python API (The "Valuable Asset").

The Shield Logic: Annotation-based Rate Limiting.

🚀 Key Features
Layer 7 Routing: Intelligent path-based routing (/api).

Rate Limiting: Protects the backend by limiting users to 1 request per second.

High Availability: Scaled across multiple nodes to ensure no single point of failure.

Burst Control: Allows a small "burst" of traffic (5 requests) before strictly enforcing the limit.

🛠️ Step-by-Step Implementation
1. Install the Ingress Controller
We first deploy the "brain" of our routing system.

Bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.2/deploy/static/provider/cloud/deploy.yaml
2. Deploy the Protected API
We create 3 copies (replicas) of our app to ensure that if one node fails, the app stays online.

Bash
kubectl apply -f advanced-app.yaml
3. Apply the Security Shield
This Ingress rule contains the "Pro" instructions for the controller.

Bash
kubectl apply -f secure-ingress.yaml
🧪 Testing the Shield
To see the rate limiter in action, we simulate a "mini-attack" by sending 10 requests as fast as possible.

Step 1: Open the tunnel

Bash
kubectl port-forward -n ingress-nginx service/ingress-nginx-controller 8080:80
Step 2: Run the attack script

Bash
for i in {1..10}; do curl -I http://localhost:8080/api; done
Step 3: Analyze results

The first few requests will show 200 OK.

Very quickly, you will see 503 Service Temporarily Unavailable or 429 Too Many Requests.

Conclusion: The Ingress successfully blocked the spam without crashing our app!

💡 What I Learned
Bypassing Kube-Proxy: How Ingress talks directly to Pod IPs for faster performance.

Annotations Power: How to configure complex NGINX features (Rate limiting, Timeouts) using simple YAML metadata.

Resource Protection: Why it's better to block traffic at the "Edge" (Ingress) than inside the Application code.
