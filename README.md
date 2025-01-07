# MLOps-Production-Ready-NLP-Project: Text Summarization

## Table of Contents
1. [Project Overview](#project-overview)
2. [Directory Structure](#directory-structure)
3. [Features](#features)
4. [Setup and Installation](#setup-and-installation)
5. [Usage](#usage)
6. [Deployment](#deployment)
7. [Workflows](#workflows)
8. [License](#license)
9. [Author](#author)


## Project Overview

This project implements an end-to-end pipeline for text summarization using advanced MLOps principles. The pipeline includes steps for data ingestion, validation, transformation, model training, evaluation, and deployment. It is designed to be modular, scalable, and ready for production deployment using AWS and GitHub Actions.


## Directory Structure

```plaintext
MLOps-Production-Ready-NLP-Project
├── .github/workflows
│   └── main.yaml            # GitHub Actions CI/CD workflow file
├── config
│   └── config.yaml          # Configuration file for the pipeline
├── research
│   ├── 01_data_ingestion.ipynb
│   ├── 02_data_validation.ipynb
│   ├── 03_data_transformation.ipynb
│   ├── 04_model_trainer.ipynb
│   ├── 05_model_evaluation.ipynb
│   └── Text_Summarization.ipynb
├── src/textSummarizer
│   ├── config
│   │   ├── __init__.py
│   │   └── configuration.py
│   ├── components
│   │   ├── __init__.py
│   │   ├── data_ingestion.py
│   │   ├── data_validation.py
│   │   ├── data_transformation.py
│   │   ├── model_trainer.py
│   │   └── model_evaluation.py
│   ├── constants
│   │   └── __init__.py
│   ├── entity
│   │   └── __init__.py
│   ├── logging
│   │   └── __init__.py
│   ├── pipeline
│   │   ├── __init__.py
│   │   ├── prediction.py
│   │   ├── stage_01_data_ingestion.py
│   │   ├── stage_02_data_validation.py
│   │   ├── stage_03_data_transformation.py
│   │   ├── stage_04_model_trainer.py
│   │   └── stage_05_model_evaluation.py
│   └── utils
│       ├── __init__.py
│       └── common.py
├── Dockerfile                # Docker setup for containerization
├── LICENSE                   # Project license
├── README.md                 # Project documentation
├── app.py                    # FastAPI app for serving the model
├── main.py                   # Entry point for running the pipeline
├── params.yaml               # Hyperparameter configuration
├── requirements.txt          # Project dependencies
├── setup.py                  # Python package setup
└── template.py               # Template for future pipelines
```


## Features

- **Data Ingestion**: Automated data extraction from source systems.
- **Data Validation**: Ensure data quality through schema and content checks.
- **Data Transformation**: Preprocess and transform raw data for model training.
- **Model Training**: Train text summarization models with state-of-the-art techniques.
- **Model Evaluation**: Evaluate model performance using standard metrics.
- **API Deployment**: Serve the trained model using a FastAPI application.
- **AWS Integration**: Deploy with CI/CD workflows on AWS infrastructure.


## Setup and Installation

### Prerequisites
1. Python 3.8 or higher
2. Conda (for virtual environment management)
3. Docker (for containerization)
4. AWS account (for deployment)

### Steps
1. **Clone the repository**:
   ```bash
   git clone https://github.com/entbappy/End-to-end-Text-Summarization
   cd End-to-end-Text-Summarization
   ```

2. **Create and activate a conda environment**:
   ```bash
   conda create -n summary python=3.8 -y
   conda activate summary
   ```

3. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the application**:
   ```bash
   python app.py
   ```

5. **Access the application**:
   Open your browser and navigate to `http://localhost:8000`.


## Usage

### Running the Pipeline
Run the individual pipeline stages using the `main.py` script:
```bash
python main.py
```

### Serving the Model
The trained model can be served via the FastAPI app by running:
```bash
python app.py
```

![Web Application Demo](images\Web Application.PNG)

### Customization
- Modify configuration settings in `config/config.yaml` and `params.yaml`.
- Add new components or modify existing ones under `src/textSummarizer/components`.


## Deployment

### AWS Deployment with GitHub Actions
1. **Login to AWS Console** and create an IAM user with the following policies:
   - `AmazonEC2FullAccess`
   - `AmazonEC2ContainerRegistryFullAccess`

2. **Create an ECR Repository**:
   ```bash
   aws ecr create-repository --repository-name text-summarizer
   ```
   Save the repository URI.

3. **Create an EC2 Instance**:
   - Launch an Ubuntu EC2 instance.
   - Install Docker:
     ```bash
     sudo apt-get update -y
     sudo apt-get install docker.io -y
     sudo usermod -aG docker ubuntu
     ```

4. **Setup GitHub Secrets**:
   Add the following secrets in your GitHub repository:
   - `AWS_ACCESS_KEY_ID`
   - `AWS_SECRET_ACCESS_KEY`
   - `AWS_REGION` (e.g., `us-east-1`)
   - `AWS_ECR_LOGIN_URI` (e.g., `566373416292.dkr.ecr.us-east-1.amazonaws.com`)
   - `ECR_REPOSITORY_NAME` (e.g., `text-summarizer`)

5. **Run the GitHub Actions Workflow**:
   Push your code to GitHub, and the deployment pipeline will automatically build, push, and deploy the application.


## Workflows

- **Data Pipeline Development**: Update pipeline components and test functionality.
- **CI/CD Workflow**: Automate testing, building, and deployment using GitHub Actions.
- **Model Updates**: Train and fine-tune models as new data becomes available.
- **API Improvements**: Enhance the API for scalability and reliability.

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.


