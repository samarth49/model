# 🔬 Marine Plankton Detection & Analysis System

**An AI-powered edge computing solution for automated plankton identification and biodiversity monitoring**

[![Python](https://img.shields.io/badge/Python-3.11-blue.svg)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.9-red.svg)](https://pytorch.org/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.28+-green.svg)](https://streamlit.io/)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)](https://www.docker.com/)
[![ARM64](https://img.shields.io/badge/ARM64-Compatible-orange.svg)](https://www.raspberrypi.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Problem Statement](#problem-statement)
- [Solution Architecture](#solution-architecture)
- [Business Model (SaaS)](#business-model-saas)
- [Dataset](#dataset)
- [Model](#model)
- [Features](#features)
- [Deployment](#deployment)
- [Technical Feasibility & Scalability](#technical-feasibility--scalability)
- [Impact](#impact)
- [Installation](#installation)
- [Usage](#usage)
- [API Documentation](#api-documentation)
- [Roadmap](#roadmap)

---

## 🌊 Overview

This system provides **real-time, automated identification and counting of marine plankton** using deep learning, designed for deployment on edge devices like Raspberry Pi for in-field marine biodiversity monitoring.

### Key Highlights

- **114 plankton species** classification capability
- **MobileNetV3-Small** architecture optimized for edge deployment
- **Real-time species classification** with human-in-the-loop review
- **Batch processing** with automated quality control
- **Real-time video processing** with annotated output
- **Automated database logging** with datetime, location & correction tracking
- **Natural language SQL queries** for data analysis
- **Modular microservices architecture** for SaaS deployment

---

## 🎯 Problem Statement

### The Challenge

Marine biodiversity monitoring is critical for:
- **Climate change research** - Plankton are key indicators of ocean health
- **Ecosystem management** - Understanding food chain dynamics
- **Water quality assessment** - Detecting environmental changes
- **Scientific research** - Long-term biodiversity studies
  
### 📌 Economic Impact (India)

- **Reduced fish stocks** lead to lower seafood yields, directly affecting a **₹1.5 lakh crore fishing industry**
- **Higher operational costs** for fishermen and aquaculture farms as natural plankton-based feed declines
- **Disruption in coastal livelihoods**, impacting millions who rely on marine-dependent micro-businesses
- **Decreased export revenue** due to reduced availability of commercial species like tuna, sardines, and shrimp

### Current Limitations

Traditional plankton analysis methods face significant challenges:

| Challenge | Impact | Our Solution |
|-----------|--------|--------------|
| **Manual identification** | Time-consuming (2-3 hours per sample) | Automated AI classification in <1 second |
| **Expert dependency** | Requires trained taxonomists | Accessible to field researchers |
| **Limited scalability** | Can't process large datasets | Batch processing of 10,000+ images/day |
| **Expensive equipment** | Lab-based microscopy  | Edge deployment on affordable hardware  |
| **No real-time analysis** | Delayed results (days/weeks) | Immediate on-site identification |
| **Poor image quality** | Blurry/duplicate images reduce accuracy | Automated image preprocessing & quality control |

### Why This Matters

**Statistics:**
- Plankton produce **50% of Earth's oxygen**
- **90% of ocean biomass** consists of plankton
- Traditional analysis: **100-200 images/day** per expert
- Our system: **10,000+ images/day** automated

**Impact Areas:**
1. **Climate Research** - Track ocean warming effects on plankton populations
2. **Fisheries Management** - Monitor food sources for commercial fish
3. **Pollution Detection** - Identify harmful algal blooms early
4. **Biodiversity Conservation** - Document species distribution changes

---

## 🏗️ Solution Architecture

### System Overview

Our system follows a **modular microservices architecture**, where each component is an independent Docker container that can be deployed and scaled separately.

![Application Container Architecture](image_6198d8.jpg)

```mermaid
graph TB
    subgraph "Client Layer"
        A[Web Browser]
        B[Mobile App]
        C[API Clients]
    end
    
    subgraph "Application Layer - Port 8501"
        D[Main Detection Service]
        D1[Image Analysis]
        D2[Video Processing]
        D3[Batch Processing]
        D4[Human Verification]
        D5[Database Logger]
    end
    
    subgraph "Preprocessing Layer - Port 8503"
        E[Image Preprocessor Service]
        E1[Blur Detection]
        E2[Image Enhancement]
        E3[Duplicate Removal]
        E4[Quality Metrics]
    end
    
    subgraph "Intelligence Layer - Port 8002"
        F[SQL Agent Service]
        F1[Natural Language Processing]
        F2[Query Router]
        F3[LLM Integration]
    end
    
    subgraph "Data Layer"
        G[(Detection Database)]
        H[(Species Database)]
        I[File Storage]
    end
    
    subgraph "ML Layer"
        J[YOLOv11 Model]
        K[MobileNetV3 Model]
    end
    
    A --> D
    B --> D
    C --> D
    
    D --> E
    D --> F
    D --> G
    D --> H
    D --> I
    D --> J
    D --> K
    
    E --> I
    F --> G
    F --> H
    
    style D fill:#4CAF50
    style E fill:#2196F3
    style F fill:#FF9800
