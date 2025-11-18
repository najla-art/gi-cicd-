Flask App with Docker & GitHub Actions CI/CD

A simple Flask-based web application containerized with Docker and deployed automatically to Docker Hub using GitHub Actions CI/CD.

This project demonstrates:

Building a minimal Python Flask web application

Containerizing the application using a Dockerfile

Automating Docker image builds & pushes using GitHub Actions

Secure authentication using GitHub Secrets

End-to-end continuous integration & deployment

🚀 Project Overview

This repository contains a lightweight Flask application that returns a simple response when accessed. The purpose of the project is to demonstrate:

How to containerize a Python web app

How to automate Docker builds

How to push Docker images to Docker Hub using CI/CD

The final workflow automatically:

Creates a Dockerfile (and optionally requirements file)

Builds the Docker image using Buildx

Tags the image with latest and commit SHA

Pushes the image to your Docker Hub repository

🖥️ Project Structure
.
├── app.py                    # Flask web application
├── requirements.txt          # Python dependencies
└── .github/
      └── workflows/
             └── docker-ci.yml  # GitHub Actions CI/CD pipeline

🧩 Application Details
app.py

A minimal Flask application:

from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello Bubu! Your Flask app is running successfully 🚀"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=3000)


Runs on port 3000

Container-friendly (binds to 0.0.0.0)

Returns a simple success message

requirements.txt
flask==3.0.0

🐳 Docker Configuration
Dockerfile

This Dockerfile (created dynamically by CI workflow) builds the Flask application into a container:

FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY app.py .
EXPOSE 3000
CMD ["python", "app.py"]

Key Features

Uses a lightweight Python base image

Installs only required dependencies

Exposes port 3000

Starts the Flask app automatically

🔐 GitHub Secrets Required

Go to
Repository → Settings → Secrets → Actions → New secret

Create:

Secret Name	Description
DOCKERHUB_USERNAME	Your Docker Hub username
DOCKERHUB_PASSWORD	Docker Hub password or access token

These are used by the CI/CD workflow to authenticate & push the Docker image.

⚙️ GitHub Actions CI/CD Workflow

Located at:

.github/workflows/docker-ci.yml

What the pipeline does:

Checks out the repository

Creates a Dockerfile (and optionally requirements.txt) dynamically

Logs into Docker Hub using secrets

Builds the Docker image using Buildx

Pushes it to Docker Hub with two tags:

latest

<commit-sha>

Workflow Triggers:

On any push to the main branch

Can be extended for pull requests or manual triggers

🐳 Final Docker Image Output

After the workflow completes, your Docker image is published at:

docker.io/<YOUR_DOCKERHUB_USERNAME>/bubu-flask-app:latest


You can pull it with:

docker pull <YOUR_DOCKERHUB_USERNAME>/bubu-flask-app:latest


Run it locally:

docker run -p 3000:3000 <YOUR_DOCKERHUB_USERNAME>/bubu-flask-app:latest

📦 How to Run Locally (Without Docker)
pip install -r requirements.txt
python app.py


Open:

http://localhost:3000

🏗️ Future Enhancements

You can extend this project by adding:

Automated deployment to:

AWS ECS

AWS EC2

Azure Web Apps

DigitalOcean Apps

Kubernetes cluster

Testing stages before build

Version tagging (v1.0, v1.1…)

Docker Compose setup

Multi-service architecture

🧾 Summary

This project is a complete example of building and automating deployment for a Python Flask application using:

Flask for the backend

Docker for containerization

GitHub Actions for automated CI/CD

Docker Hub as the container registry

It demonstrates best practices like:

Secure credential handling

Automated build pipelines

Lightweight Docker image creation

Versioned image publishing
