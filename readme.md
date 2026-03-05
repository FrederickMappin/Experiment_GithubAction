## Learning GitHub Actions

This repository is a hands-on practice project for learning how GitHub Actions automates code quality checks in a Python codebase.

## Goal

Use small, practical workflows to understand how CI (Continuous Integration) works when code is pushed or reviewed in pull requests.

## What I Am Learning

- How to trigger workflows on `push` and `pull_request`
- How to set up a Python environment in GitHub Actions
- How to install project dependencies in a clean runner
- How to run linting and tests automatically
- How workflow feedback helps catch issues before merge

## Purpose of `ci.yml`

The workflow file at `.github/workflows/ci.yml` is your main CI pipeline.

It is designed to:

1. Run on every push to `main` and every pull request targeting `main`.
2. Check out your repository code.
3. Install Python `3.10`.
4. Install dependencies from `requirements.txt`.
5. Run `flake8` to enforce linting standards.
6. Run `pytest` to validate functionality through tests.

In short, `ci.yml` helps ensure that new changes are clean, testable, and less likely to break the project.

## Docker Workflows

This repository has two Docker-related GitHub Actions workflows.

### 1. Package Docker Image as Artifact

Workflow file: `.github/workflows/docker-package.yml`

This workflow:

1. Runs on push to `main` and on manual trigger (`workflow_dispatch`).
2. Builds the image from the root `Dockerfile`.
3. Exports the image as a tarball (`simplecalculator-image.tar`).
4. Uploads it as the `simplecalculator-docker-image` artifact.

To use the artifact locally after download:

`docker load -i simplecalculator-image.tar`

### 2. Build and Publish to Docker Hub

Workflow file: `.github/workflows/dockerhub-publish.yml`

This workflow:

1. Runs on push to `main` and on manual trigger (`workflow_dispatch`).
2. Logs into Docker Hub using repository secrets.
3. Builds the image from the root `Dockerfile`.
4. Pushes image tags to Docker Hub:
	- `latest`
	- short commit SHA tag

Required repository secrets:

- `DOCKER_HUB_USERNAME`
- `DOCKER_HUB_ACCESS_TOKEN`

Published image name:

`<DOCKER_HUB_USERNAME>/simplecalculator`

## Why This Matters

By using this workflow, you get fast and consistent validation of your code. This builds good engineering habits and makes collaboration safer as the project grows.
