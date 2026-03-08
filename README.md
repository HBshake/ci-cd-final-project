# ci-cd-final-project

## CI/CD Tools and Practices Final Project

This project demonstrates a full CI/CD pipeline for a RESTful counter microservice using GitHub Actions and OpenShift Pipelines (Tekton).

## CI with GitHub Actions

The `.github/workflows/workflow.yml` pipeline:
- Triggers on push and pull requests to `main`
- Runs on `ubuntu-latest` using `python:3.9-slim`
- Steps: Checkout → Install dependencies → Lint (flake8) → Unit tests (nose)

## CD with OpenShift Pipelines (Tekton)

The `.tekton/tasks.yml` file defines:
- **cleanup** – clears the workspace
- **nose** – runs unit tests

The `.tekton/pipeline.yaml` defines the full CD pipeline:
- init → clone → lint → tests → build → deploy

## How to Run

### GitHub Actions
Push to `main` — the workflow triggers automatically.

### OpenShift Pipeline
```bash
kubectl apply -f .tekton/tasks.yml
oc apply -f .tekton/pipeline.yaml
```

Then start the pipeline from the OpenShift console with your repo URL, branch, image, and app name.