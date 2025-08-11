# 🏨 Hotel Reservation Prediction – Advanced MLOps Project

![MLOps](https://img.shields.io/badge/MLOps-CI%2FCD-blue)
![Python](https://img.shields.io/badge/Python-3.10%2B-brightgreen)
![License](https://img.shields.io/badge/License-GPL--3.0-orange)
![Docker](https://img.shields.io/badge/Docker-Ready-blue)
![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD-success)

An end-to-end MLOps project for predicting hotel reservation status using machine learning. This project demonstrates the integration of data pipelines, automated training, CI/CD deployment with Jenkins, Dockerization, and a web application for user interaction. It follows best practices for reproducibility, automation, and production-level deployment.

> 📁 **Repository**: `Advanced_MLOPS_Project1_Hotel_Reservation_Predection`

---

## 🚀 Project Highlights

- 📊 **Data Pipeline**: Automated ingestion and preprocessing of hotel reservation data
- 🤖 **ML Model Training**: Customizable model pipeline for prediction
- 🛠️ **MLOps Workflow**: Modular structure with configuration-driven design
- 🐳 **Dockerized**: Ready for local or cloud container deployment
- 🔄 **CI/CD with Jenkins**: Automated build, test, and deployment pipeline
- 🌐 **Web App**: User-friendly interface for hotel reservation predictions

---

## 🧠 Technical Stack

### 🛠️ Core Technologies
![Python](https://img.shields.io/badge/Python-3.10%2B-brightgreen)
![Docker](https://img.shields.io/badge/Docker-Ready-blue)
![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD-success)
![Flask](https://img.shields.io/badge/Flask-WebApp-lightgrey)

### 📦 Libraries & Utilities
- Pandas, NumPy, Scikit-learn
- YAML for configuration management

---

## 🏗️ Project Structure

```bash
Advanced_MLOPS_Project1_Hotel_Reservation_Predection/
├── DATASET/
│   └── Hotel Reservations.csv      # Raw dataset
├── PROJECT CODE/
│   ├── config/
│   │   ├── config.yaml            # Configuration file
│   │   ├── model_params.py        # ML model parameters
│   │   └── paths_config.py        # Path configs
│   ├── custom_jenkins/
│   │   ├── Dockerfile
│   │   └── Jenkinsfile            # Jenkins pipeline definition
│   ├── notebook/
│   │   └── notebook.ipynb         # EDA & prototyping
│   ├── pipeline/
│   │   ├── __init__.py
│   │   └── training_pipeline.py   # ML pipeline orchestration
│   ├── src/
│   │   ├── __init__.py
│   │   ├── custom_exception.py
│   │   ├── data_ingestion.py
│   │   ├── data_preprocessing.py
│   │   ├── logger.py
│   │   └── model_training.py
│   ├── static/
│   │   └── style.css              # Web app styling
│   ├── templates/
│   │   └── index.html             # Web app template
│   ├── utils/
│   │   ├── __init__.py
│   │   └── common_functions.py
│   ├── application.py             # Flask app entry point
│   ├── requirements.txt           # Python dependencies
│   ├── setup.py                   # Package setup
│   ├── LICENSE
│   ├── NOTES & WORKFLOW.pdf       # Documentation/workflow
│   └── README.md
├── .gitignore
```

---

## ⚡ Installation & Usage

### 1. Clone the repository
```bash
git clone https://github.com/mdzaheerjk/Advanced_MLOPS_Project1_Hotel_Reservation_Predection.git
cd Advanced_MLOPS_Project1_Hotel_Reservation_Predection/PROJECT CODE
```

### 2. Create and activate a virtual environment
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Run the end-to-end pipeline
```bash
python pipeline/training_pipeline.py
```

### 5. Run the web application
```bash
python application.py
```
Access the app at [http://127.0.0.1:5000](http://127.0.0.1:5000)

---

## 🐳 Docker & CI/CD

- **Docker:**  
  Build and run the project in a containerized environment using the provided `Dockerfile`.

- **Jenkins CI/CD:**  
  Use the `Jenkinsfile` for automating build, test, and deployment processes. Step-by-step instructions can be found in `STEPS FOR CI-CD Deployment on Jenkins.txt`.

---

## 📊 Example Use Cases

- **Hotel Reservation Prediction**: Classify if a reservation will be fulfilled or canceled
- **Real-time Web Inference**: User uploads reservation data and gets predictions
- **MLOps Demonstration**: Shows how to automate ML workflows from data to deployment

---

## ✍️ Author

**Mohammed Zaheeruddin**  
🎓 First-Year B.Tech Student | AI/ML & GenAI Enthusiast  
🏫 Shetty Institute of Technology, Gulbarga  
📧 info.zaheerjk@gmail.com

---

## 📜 License

This project is licensed under the **GPL-3.0 License** - see the LICENSE file for details.

---

#### Key Features:
1. End-to-end MLOps pipeline with modular code organization
2. Automated data processing, training, and deployment
3. Docker and Jenkins for reproducible CI/CD workflows
4. User-friendly web application for model inference
5. Ready for educational, research, and production demonstration
