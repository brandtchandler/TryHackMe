# TryHackMe - AI System Reconnaissance

**Platform**: TryHackMe  
**Difficulty**: Medium  
**Category**:  AI Security Path
**Date**:  19 OCT 2026
**Time spent**:  2.5 hours (Including Write-up)
**Tags**: `#TryHackMe` `#AISecurity` 

---

## Summary

AI System Reconnaissance is a hands-on room that teaches how to discover and enumerate AI/ML infrastructure on a live network. You learn to identify common components such as model servers (Triton, TorchServe, Ollama, vLLM), experiment trackers (MLflow), vector databases, Jupyter notebooks, and model registries by scanning their distinctive ports and fingerprinting their APIs. The room shows how to extract valuable metadata (model names, experiment histories, credentials, artifact locations) using tools like Nmap, curl, and grpcurl, and explains how these findings expand the traditional attack surface. It is defender oriented discovery work that complements threat modelling by confirming what AI systems are actually deployed and exposed.

## Key Takeaways / Personal Takeaways

- Many AI systems are not as proteted as they should be. Currently there is a pattern to finding and exploiting these AI/LLMs. Understanding these patterns helps us understand how to protect the AI Systems better.

---

## Learning Objectives

- Identify the common components of a production AI/ML system and the ports, protocols, and API paths each one exposes
- Fingerprint AI and ML services by analysing HTTP headers, API response structures, error messages, and endpoint naming conventions
- Enumerate model metadata, experiment histories, and deployment configurations from exposed tracking servers and inference endpoints
- Map how AI components expand the traditional network attack surface, including new data flows, internal APIs, and supply chain dependencies
- Apply a structured AI reconnaissance methodology using existing security tools with AI-specific configurations
- Recognise the logging and monitoring signatures that indicate AI-focused reconnaissance activity against your infrastructure

---

## Learning Objectives & Tasks

### Task 1 – Introduction
Introduction to the room with objectives and the reasons why this information is needed.
Need to understand basic Linux CLI and common commands including nmap.
### Task 2 – The AI Infrastructure Stack
| Component                  | Description                                                                 | Default Port(s)   | Protocol(s)            | Recon Endpoints                          |
|---------------------------|-----------------------------------------------------------------------------|-------------------|------------------------|------------------------------------------|
| **NVIDIA Triton**         | Loads models into memory and serves predictions at scale                    | 8000, 8001, 8002  | HTTP, gRPC, Prometheus | `/v2/health/ready`, `/v2/models`         |
| **TensorFlow Serving**    | Google's model serving framework for TensorFlow models                      | 8500, 8501        | gRPC, HTTP             | `/v1/models/<name>`                      |
| **TorchServe**            | PyTorch's official model serving framework                                  | 8080, 8081, 8082  | HTTP                   | `/ping`, `/models`                       |
| **Ollama**                | Local runtime for running LLMs on your own hardware                         | 11434             | HTTP                   | `/api/tags`, `/api/show`                 |
| **vLLM**                  | High-throughput LLM serving engine with OpenAI-compatible API               | 8000              | HTTP                   | `/v1/models`                             |
| **MLflow**                | Tracks experiments, stores models, and manages the ML lifecycle             | 5000              | HTTP                   | `/api/2.0/mlflow/experiments/search`     |
| **Kubeflow**              | Kubernetes-native platform for orchestrating ML pipelines                   | 80, 443           | HTTP                   | `/pipeline/apis/v1beta1/pipelines`       |
| **Ray**                   | Distributed compute framework for scaling AI workloads                      | 8265, 8000        | HTTP                   | `/api/jobs/`, Ray Dashboard              |
| **Qdrant**                | Vector database for semantic search and RAG pipelines                       | 6333, 6334        | HTTP, gRPC             | `/collections`                           |
| **Weaviate**              | Vector database with built-in GraphQL and module system                     | 8080              | HTTP, GraphQL          | `/v1/schema`, `/v1/meta`                 |
| **Milvus**                | Distributed vector database for large-scale embedding storage               | 19530             | gRPC                   | Port 19530 connection                    |
| **Jupyter Notebook**      | Interactive coding environment used by data scientists                      | 8888              | HTTP                   | `/api/kernels`, `/api/contents`          |
| **MinIO**                 | S3-compatible object storage often used for model artifacts                 | 9000, 9001        | HTTP (S3-compatible)   | Bucket listing                           |
| **Prometheus metrics**    | Built-in monitoring endpoint (exposed by Triton, TorchServe, etc.)          | 8002, 8082        | HTTP                   | `/metrics`                               |
- gRPC is faster for large tensor payloads  
- A model registry stores the actual model files  
- MLflow and model registries are among the highest-value targets

### Task 3 – Fingerprinting AI Services
Standard `nmap -sV` often mislabels AI services. Real fingerprinting uses:
- HTTP response headers (e.g. `NV-Status` for Triton, `Server: TorchServe`)
- JSON response structures
- Error messages from malformed requests
- Endpoint naming conventions
- gRPC reflection (`grpcurl -plaintext <host>:<port> list`)

### Task 4 – Enumerating AI Systems
Once a service is identified, extract intelligence:
- MLflow: experiments, registered models, model versions, artifact URIs, user IDs
- Inference servers: model configs, tensor specs
- Vector databases: collections / schemas
- Jupyter: notebook contents (often contain cleartext credentials)

### Task 5 – Mapping the AI Attack Surface
Connect individual findings into a full attack surface map.  
Shows how AI components expand the traditional network attack surface and links findings to MITRE ATLAS techniques (especially supply-chain related ones).

### Task 6 – Structured Reconnaissance Methodology and Detection
Pulls everything into a repeatable 5-phase methodology:
1. Passive Recon (Shodan/GitHub dorks)
2. Port Scanning (AI-specific ports)
3. API Fingerprinting
4. Metadata Extraction
5. Attack Surface Mapping  

Also covers what this activity looks like in SIEM logs from the defender’s side.

### Task 7 – Conclusion
Recap of the full reconnaissance workflow and mapping of techniques to industry frameworks (primarily MITRE ATLAS).

---

## Practical Notes

- Always start with the AI-specific port list rather than default Nmap top ports.
- MLflow, Jupyter, and model registries tend to yield the highest-value findings (credentials, artifact locations, experiment history).
- gRPC reflection is extremely useful when enabled — treat it like an exposed OpenAPI/Swagger.
- Look for cleartext secrets in Jupyter notebooks and environment variables.
- Map findings to ATLAS techniques for reporting (e.g. AML.T0010 for supply-chain exposure).

---

## References

- TryHackMe room: https://tryhackme.com/room/aisystemreconnaissance  
- MITRE ATLAS: https://atlas.mitre.org/  
