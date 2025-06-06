
# DevOps Project

This project demonstrates a basic CI/CD pipeline using Jenkins, Docker, and SonarQube.

## Components

✅ Jenkinsfile  
✅ Dockerfile  
✅ SonarQube static code analysis  
✅ Slack notifications  
✅ Minimal Flask application  
✅ GitHub integration

## Pipeline Steps

1. **Checkout code** from GitHub.
2. **Set version** (based on Git commit hash).
3. **Static code analysis** using SonarQube.
4. **Build Docker image** for the Flask app.
5. **Push Docker image** to DockerHub.
6. **Run tests** using `pytest`.
7. **Deploy** step (dummy placeholder).
8. **Slack notifications** on success/failure.

## Files

- `Jenkinsfile` — defines the CI/CD pipeline.
- `Dockerfile` — defines how to containerize the application.
- `sonar-project.properties` — config for SonarQube analysis.
- `app/` — minimal Flask application:
  - `app.py` — basic Flask app.
  - `requirements.txt` — dependencies.

## Custom Application

The project includes a basic **Flask app** (`app/app.py`) as required:

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello from DevOps Pipeline!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

## Notes

- **Ansible** playbooks were removed as not required.
- The pipeline uses **Slack notifications** (you need to configure Slack Webhook).
- The pipeline uses **SonarQube** (you need to configure SonarQube server).

---

## Points Mapping

| Criteria                                             | Points |
|------------------------------------------------------|--------|
| Jenkins installation and configuration               | 1.0    |
| Use of Jenkinsfile in GitHub repository              | 1.0    |
| Creating Dockerfile and building Docker images       | 1.0    |
| Defining the full application lifecycle in Jenkinsfile| 0.25   |
| Setting up notifications (Slack)                     | 0.5    |
| Static code analysis tools (SonarQube)                | 0.5    |
| Custom application (Flask app)                       | 0.25   |
| **Total**                                            | **4.5**|

---

## How to run locally

```bash
# Build the Docker image
docker build -t myflaskapp .

# Run the Flask app in Docker
docker run -p 5000:5000 myflaskapp
```

Visit: [http://localhost:5000](http://localhost:5000)

---

Prepared for submission as part of **DevOps CI/CD project** ✅
