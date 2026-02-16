# Projects Portfolio

## Production & Enterprise Projects

### Agent Mesh Platform - Microservices Architecture for GenAI
**Status**: Ongoing (2025-01 - Present)  
**Role**: Platform Architect & Lead Developer

**Description**: Platform engineering project for deploying and governing multi-agent systems. Designed microservices-based architecture with observability, security controls, and operational patterns for production GenAI agents.

**Key Features**:
- Governance framework for agent lifecycle: ownership, monitoring, SAST/DAST integration
- YAML-configurable RAG environments with dockerized agents
- Model/connector selection and API exposure
- Centralized observability with verbose logging per operation

**Technologies**: Python, Docker, Kubernetes, Azure Container Apps, LangChain, LangGraph, Azure OpenAI, Application Insights, Azure DevOps

**Keywords**: MLOps, GenAI, Platform Engineering, Microservices Architecture, Agent Orchestration, Multi-Agent Systems, Governance Framework, Observability

---

### Enterprise RAG on Azure - End-to-End GenAI Solution
**Status**: Completed (2024-06 - 2024-10)  
**Role**: Solution Architect & Developer

**Description**: Production RAG system on Azure with SharePoint as document source, hybrid search capabilities, vector storage, and enterprise-grade security/compliance controls.

**Key Achievements**:
- Architected end-to-end RAG solution with hybrid search (keyword + semantic) and reranking
- Implemented secure authentication with Azure AD, token management, and audit logging
- Designed cost optimization strategies and OPEX estimation model by usage patterns
- Delivered governance framework aligned with corporate compliance requirements

**Technologies**: Azure OpenAI, Azure AI Search, Cosmos DB, Azure Functions, SharePoint, LangChain, Python, Azure DevOps

**Keywords**: GenAI, RAG Architecture, Azure OpenAI, Enterprise AI, Security Compliance, Solution Architecture, Hybrid Search, Vector Databases

---

### GPU-Accelerated Deepfake Detection Pipeline
**Status**: Completed (2024-08 - 2024-11)  
**Role**: ML Engineer

**Description**: High-performance computer vision pipeline for deepfake detection supporting multiple SOTA models, efficient preprocessing with CUDA acceleration, and production deployment patterns.

**Key Achievements**:
- Evaluated and optimized **23 state-of-the-art deepfake detection models**
- Achieved **0.99 accuracy** on FaceForensics++/Celeb-DF datasets
- Implemented GPU-accelerated face detection, alignment, and landmark extraction reducing processing time **10x**
- Created reproducible training pipeline with experiment tracking and model versioning
- Designed inference optimization strategies with TensorRT for production deployment

**Technologies**: PyTorch, CUDA, TensorRT, OpenCV, Python, Docker, MLflow

**Keywords**: Computer Vision, Deepfake Detection, GPU Acceleration, PyTorch, MLOps, Production ML, CUDA, TensorRT, Model Optimization

---

### FaceForensics++ Production Pipeline - Large-Scale Dataset Engineering
**Status**: Completed (2024-09 - 2024-12)  
**Role**: Data Pipeline Engineer

**Description**: End-to-end data pipeline for processing FaceForensics++ dataset (>1TB) with focus on reproducibility, integrity validation, and balanced partitioning for distributed training.

**Key Achievements**:
- Implemented idempotent download/validation pipeline with integrity checks and resume capability
- Created balanced 20-shard partitioning strategy for distributed GPU training
- Optimized GPU-accelerated preprocessing replacing dlib with CUDA-enabled detectors
- Established traceability and versioning patterns for large-scale video datasets

**Technologies**: Python, AWS S3, boto3, Docker, CUDA, GPU acceleration, Pandas, tqdm

**Keywords**: Data Engineering, MLOps, Computer Vision, Data Pipeline, GPU Acceleration, AWS S3, Large-scale Datasets

---

### MLOps Platform - Self-hosted Experimentation Stack
**Status**: Completed (2023-10 - 2024-01)  
**Role**: Platform Engineer

**Description**: Personal MLOps platform built with Docker Compose featuring MLflow for experiment tracking, MinIO for artifact storage, and supporting tools for collaborative development.

**Key Achievements**:
- Deployed persistent multi-user MLflow instance with backend storage and access controls
- Integrated S3-compatible MinIO for artifact versioning and model registry
- Implemented idempotent deployment scripts and infrastructure-as-code patterns
- Created operational runbooks for backup, scaling, and troubleshooting

**Technologies**: Docker Compose, MLflow, MinIO, Python, Terraform, Linux

**Keywords**: MLOps, Platform Engineering, MLflow, Experiment Tracking, Model Registry, Infrastructure as Code, DevOps

---

### RAG Evaluation Framework - GenAI Quality Assurance
**Status**: Completed (2024-11 - 2025-01)  
**Role**: ML Engineer

**Description**: Comprehensive evaluation harness for RAG systems including custom metrics, automated testing, synthetic dataset generation, and performance benchmarking aligned with MLOps best practices.

**Key Achievements**:
- Designed evaluation framework with semantic similarity, retrieval accuracy, and response quality metrics
- Implemented synthetic dataset generation and validation pipeline for RAG testing
- Created automated testing harness integrated with CI/CD for quality gates
- Established traceability and versioning for prompts, retrievers, and model configurations

**Technologies**: Python, LangChain, Azure AI Search, Cosmos DB, MLflow, Pandas, OpenAI

**Keywords**: GenAI, RAG Evaluation, Evaluation Metrics, MLOps, Testing Framework, Quality Assurance

---

### Remote Development Environment on AWS
**Status**: Completed (2024-03 - 2024-05)  
**Role**: DevOps Engineer

**Description**: Enterprise-grade remote development solution for ML workloads bypassing local restrictions. EC2-based workstation with GPU support, persistent volumes, and GUI/SSH access.

**Key Achievements**:
- Designed and deployed persistent remote development environment with GPU capabilities
- Implemented secure access patterns with VPN, SSH keys, and IAM controls
- Created reproducible infrastructure-as-code deployment with Terraform
- Established cost optimization strategies for GPU instance usage

**Technologies**: AWS EC2, Docker, Linux, Terraform, VPN, GPU instances

**Keywords**: AWS, DevOps, Infrastructure as Code, GPU Instances, Remote Development, MLOps Infrastructure

---

## Academic & Learning Projects

### Coursera Machine Learning Exercises
**Repository**: [github.com/larusso94/Coursera-Machine-learning-exercises](https://github.com/larusso94/Coursera-Machine-learning-exercises)

Series of exercises covering fundamental machine learning concepts, implemented in MATLAB, as part of Andrew Ng's Machine Learning course.

---

### Shark Species Dataset on Kaggle
**Dataset**: [kaggle.com/datasets/larusso94/shark-species](https://www.kaggle.com/datasets/larusso94/shark-species)

Created from scratch using Google Image APIs, comprising images for shark species classification. Cleaned with FastAI Python libraries and used with pre-trained ResNet model.

---

### Shark Species Classifier
**Repository**: [github.com/larusso94/Sharks](https://github.com/larusso94/Sharks)

Binder-enabled Jupyter Notebook for interactive testing of shark species classification model using pre-trained ResNet.

---

### Labyrinth Pathfinder Project
**Repository**: [github.com/larusso94/labirynth_damavis](https://github.com/larusso94/labirynth_damavis)

Python-based solution for pathfinding in a labyrinth using object-oriented principles and breadth-first search algorithm. Emphasizes code quality through unit testing.

---

### IBM Data Science Capstone Project
**Repository**: [github.com/larusso94/IBM-Proffessional-Certificate-Data-Science-Capstone-Course](https://github.com/larusso94/IBM-Proffessional-Certificate-Data-Science-Capstone-Course)

Detailed analysis of 911 call data showcasing in-depth exploratory and predictive data analysis techniques.
