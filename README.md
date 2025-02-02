# End-to-End Machine Learning Project: Student Performance Predictor

This project demonstrates how to build and deploy an end-to-end machine learning project that predicts student performance (specifically math scores) based on various factors. It covers data ingestion, preprocessing, model training, hyperparameter tuning, prediction pipeline creation, web application development with Flask, and deployment to AWS Elastic Beanstalk.

## Project Goal

The main goal of this project is to predict a student's math score based on features such as gender, race/ethnicity, parental level of education, lunch type, test preparation course, reading score, and writing score.

## Dataset

The project uses a dataset containing student performance information. The dataset includes the following features:

*   **gender:** Sex of students (male/female)
*   **race/ethnicity:** Ethnicity of students (group A, group B, group C, group D, group E)
*   **parental level of education:** Parent's final education (bachelor's degree, some college, master's degree, associate's degree, high school, some high school)
*   **lunch:** Type of lunch taken by the student (standard, free/reduced)
*   **test preparation course:** Test preparation course completed (completed, none)
*   **math score:** Score in math (target variable)
*   **reading score:** Score in reading
*   **writing score:** Score in writing

## Project Structure

The project follows a modular structure with the following directories and files:


ml_project/
├── .ebextensions/ # Configuration files for AWS Elastic Beanstalk
│ └── python.config # Python configuration for Elastic Beanstalk
├── .github/ # GitHub-related files (workflows, etc.)
├── artifacts/ # Folder to store model artifacts (pickle files)
│ ├── model.pickle # Trained machine learning model
│ └── preprocessor.pickle # Data preprocessor
├── logs/ # Stores logs from application
├── notebook/ # Jupyter notebooks for EDA and model experimentation
│ ├── data/ # data files for notebook
│ │ └── stud.csv
│ ├── eda.ipynb # Exploratory Data Analysis
│ └── model_trainer.ipynb # Model Training and Evaluation
├── requirements.txt # Project dependencies
├── setup.py # For creating the project as a package
├── src/ # Source code
│ ├── components/ # Project components
│ │ ├── init.py
│ │ ├── data_ingestion.py # Data ingestion component
│ │ ├── data_transformation.py # Data transformation component
│ │ └── model_trainer.py # Model training component
│ ├── pipeline/ # Prediction and training pipelines
│ │ ├── init.py
│ │ ├── predict_pipeline.py # Prediction pipeline
│ │ └── train_pipeline.py # Training pipeline (Optional, to be completed)
│ ├── init.py
│ ├── exception.py # Custom exception handling
│ ├── logger.py # Logging setup
│ └── utils.py # Utility functions
├── templates/ # HTML templates for the Flask app
│ ├── home.html # Home page for predictions
│ └── index.html # Default index page
├── application.py # Main Flask application file
├── gitignore # .gitignore file
└── README.md # This file

## Getting Started

### Prerequisites

*   Python 3.8
*   Git
*   AWS Account (for deployment)
*   Familiarity with machine learning concepts, Flask, and AWS.

### Installation

1. **Clone the repository:**

    
    git clone <repository_url>
    cd ml_project
    
    Replace `<repository_url>` with the actual URL of your forked repository.

2. **Create and activate a virtual environment (recommended):**

    
    conda create -n venv python=3.8
    conda activate venv


3. **Install dependencies:**

   
    pip install -r requirements.txt
    ```

### Running the Application

1. **Run the Flask app locally:**

    python application.py
    ```

    This will start the Flask development server. You can access the application in your browser at `http://127.0.0.1:5000/`.

2. **To make predictions, navigate to:**

    ```
    http://127.0.0.1:5000/predictdata
    ```

    Fill out the form with student information and click "Predict" to get the predicted math score.

### Deployment to AWS Elastic Beanstalk

1. **Create an AWS Account:** If you don't have one, sign up for an AWS account.

2. **Configure AWS Credentials:** Set up your AWS credentials locally. You can use the AWS CLI or environment variables.

3. **Create an Elastic Beanstalk Application:**
    *   Go to the AWS Management Console and search for "Elastic Beanstalk."
    *   Click "Create application."
    *   Provide an application name (e.g., "student-performance").
    *   Choose "Python" as the platform and select Python 3.8.
    *   Select "Sample application" for now.
    *   Click "Create application."

4. **Create a Code Pipeline:**
    *   Go to the AWS Management Console and search for "CodePipeline."
    *   Click "Create pipeline."
    *   Provide a pipeline name (e.g., "student-performance-pipeline").
    *   Choose "New service role" and click "Next."
    *   Select "GitHub (Version 1)" as the source provider.
    *   Connect to your GitHub account and authorize AWS CodePipeline.
    *   Choose your repository and branch (e.g., "ml_project" and "main").
    *   Click "Next."
    *   Skip the build stage for now (click "Skip build stage").
    *   Choose "AWS Elastic Beanstalk" as the deploy provider.
    *   Select your application name and environment name.
    *   Click "Next."
    *   Review the pipeline settings and click "Create pipeline."

5. **Update code to remove app.py file**

6. **Commit and Push Changes:**
    *   Make sure your code changes are committed and pushed to your GitHub repository.
    *   This will trigger the CodePipeline to deploy the latest code to Elastic Beanstalk.

7. **Monitor Deployment:**
    *   In the CodePipeline console, you can monitor the deployment progress.
    *   Once the deployment is successful, you can access your application through the Elastic Beanstalk environment URL.

## Further Improvements

*   **Continuous Integration (CI):** Implement a CI pipeline to automatically run tests and build the application whenever changes are pushed to the repository.
*   **Dockerization:** Containerize the application using Docker for easier deployment and portability.
*   **More Robust Web App:** Enhance the Flask application with better UI/UX, input validation, and error handling.
*   **Database Integration:** Read data from a database instead of a CSV file.
*   **Model Monitoring:** Implement monitoring to track model performance over time and retrain if necessary.