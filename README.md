# 🌟 **MLOps Pipeline with GitHub Actions & Hugging Face**

A fully automated **CI/CD pipeline** for Machine Learning using **GitHub Actions**, **Hugging Face Hub**, and Python.
This project demonstrates how to automate dataset registration, data preparation, model training, and deployment to a Hugging Face Space using a multi-stage workflow.

---

## 🚀 **Project Overview**

This repository showcases a complete **end-to-end MLOps workflow** that includes:

✔ Dataset upload to Hugging Face
✔ Data preprocessing
✔ Model training
✔ Auto-deployment to Hugging Face Spaces
✔ CI/CD using GitHub Actions
✔ Auto-trigger on every push to the `main` branch

All steps run automatically through a structured GitHub Actions pipeline.

---

## 📁 **Project Structure**

```
mlops/
│── model_building/
│     ├── data_register.py
│     ├── prep.py
│     ├── train.py
│
│── hosting/
│     ├── hosting.py
│
.github/
│── workflows/
│     ├── pipeline.yml
```

---

## 🔧 **Tech Stack**

* **Python**
* **GitHub Actions**
* **Hugging Face Datasets**
* **Hugging Face Spaces**
* **Transformers / ML Frameworks (as used inside scripts)**

---

## 🔐 **Setup Requirements**

### 1️⃣ Generate Hugging Face Token

1. Go to Hugging Face → Profile → *Access Tokens*
2. Create a **Write** token
3. Copy the token

### 2️⃣ Add Token to GitHub Secrets

In your GitHub repo:

```
Settings → Secrets and Variables → Actions → New Secret
Name: HF_TOKEN
Value: <paste your HF token>
```

---

## ⚙️ **GitHub Actions Workflow**

Your CI/CD pipeline is defined in:

```
.github/workflows/pipeline.yml
```

### **Pipeline Stages**

| Stage                | Description                             |
| -------------------- | --------------------------------------- |
| **register-dataset** | Upload dataset to Hugging Face          |
| **data-prep**        | Preprocess data and save artifacts      |
| **model-training**   | Train model using Hugging Face datasets |
| **deploy-hosting**   | Deploy model/code to Hugging Face Space |

---

## 📜 **pipeline.yml (Workflow)**

```yaml
name: MLOps pipeline

on:
  workflow_dispatch:
  push:
    branches:
      - main

jobs:

  register-dataset:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install Dependencies
        run: pip install -r mlops/requirements.txt
      - name: Upload Dataset to Hugging Face Hub
        env:
          HF_TOKEN: ${{ secrets.HF_TOKEN }}
        run: python mlops/model_building/data_register.py

  data-prep:
    needs: register-dataset
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install Dependencies
        run: pip install -r mlops/requirements.txt
      - name: Run Data Preparation
        env:
          HF_TOKEN: ${{ secrets.HF_TOKEN }}
        run: python mlops/model_building/prep.py

  model-traning:
    needs: data-prep
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install Dependencies
        run: pip install -r mlops/requirements.txt
      - name: Model Building
        env:
          HF_TOKEN: ${{ secrets.HF_TOKEN }}
        run: python mlops/model_building/train.py

  deploy-hosting:
    runs-on: ubuntu-latest
    needs: [model-traning, data-prep, register-dataset]
    steps:
      - uses: actions/checkout@v3
      - name: Install Dependencies
        run: pip install -r mlops/requirements.txt
      - name: Push files to Frontend Hugging Face Space
        env:
          HF_TOKEN: ${{ secrets.HF_TOKEN }}
        run: python mlops/hosting/hosting.py
```

---

## 🖥️ **How to Run the Pipeline**

You can trigger manually:

```
GitHub → Actions → MLOps pipeline → Run workflow
```

Or automatically whenever you push to **main**.

---

## 🎯 **Key Features**

* **Automated training pipeline**
* **Version-controlled datasets & models**
* **Auto-deployment to Hugging Face Space**
* **Secure token handling**
* **Modular and extensible folder structure**
* **Plug-and-play for any ML project**

---

## 📌 **Live Links**

🔗 **GitHub Repository: https://github.com/GovindYadav16/MLOps
🔗 **Hugging Face Space / App:** https://huggingface.co/spaces/yadavgovind/Bank-Customer-Churn

---

## 🏁 **Conclusion**

This project demonstrates a professional-grade MLOps workflow utilizing GitHub Actions and Hugging Face.
It automates the entire ML lifecycle — from dataset upload to model deployment — ensuring continuous integration and delivery.


Just tell me!
