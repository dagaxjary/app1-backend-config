# Argo CD -Projects

## Overview

This directory is the fifth module in the `ArgoCD-Basics-To-Production` repository. It focuses on Argo CD Projects and how to structure GitOps application delivery for multiple teams, environments, and destination clusters/namespaces.

The content here is intended to demonstrate:
- Argo CD Project definitions for grouping applications
- Application manifests and environment overlays
- GitOps workflows for deploying and promoting workloads
- Access controls and destination restrictions using Argo CD Projects

## Key Concepts and Features

- **Argo CD Projects**: logical boundaries for applications that define source repos, destination clusters/namespaces, and allowed operations.
- **Application grouping**: organize apps by team, environment, or service domain.
- **Environment promotion**: separate development, staging, and production manifests so changes can be validated before promotion.
- **Declarative deployment**: keep all Argo CD resources in Git so the cluster state can be rebuilt from source control.

## Repository Structure

This module generally contains resources related to projects and applications. Common folders and files include:

- `projects/` or project manifests: Argo CD `AppProject` definitions
- `applications/` or app manifests: Argo CD `Application` resources
- `env/`, `overlays/`, or similar: environment-specific settings for dev/stage/prod
- `README.md`: this documentation for the module

Because this module is part of a training path, the primary focus is on how Argo CD Projects are used rather than on application source code.

## Prerequisites

- A Kubernetes cluster accessible from your local environment
- Argo CD installed in the cluster
- `kubectl` configured to use the target cluster
- `argocd` CLI installed and configured, or access to the Argo CD web UI
- Git access to this repository

## Setup Instructions

1. Clone the repository and move into the module directory:

   ```bash
   git clone <repo-url>
   cd ArgoCD-Basics-To-Production/05-Projects
   ```

2. Confirm your Kubernetes context is set correctly:

   ```bash
   kubectl config current-context
   ```

3. Ensure Argo CD is available and reachable.

4. Apply the Argo CD Project resources from this module:

   ```bash
   kubectl apply -f <path-to-project-manifest>.yaml
   ```

5. Create or apply the Argo CD Applications defined in this module:

   ```bash
   kubectl apply -f <path-to-application-manifest>.yaml
   ```

6. If using the Argo CD CLI, log in to the server:

   ```bash
   argocd login <argocd-server> --username admin --password <password>
   ```

## Usage

Once the project and applications are applied, use Argo CD to manage them.

- List projects and applications:

  ```bash
  argocd proj list
  argocd app list
  ```

- View application status:

  ```bash
  argocd app get <app-name>
  ```

- Synchronize an application:

  ```bash
  argocd app sync <app-name>
  ```

- Promote a change by updating manifests in Git and letting Argo CD reconcile.

If you prefer the web UI, open the Argo CD dashboard and inspect the project and application resources directly.

## Best Practices

- Keep project boundaries narrow and aligned with teams or environments.
- Use explicit source repo and destination restrictions in each `AppProject`.
- Store environment-specific values in separate overlays or directories.
- Use Git commits and pull requests to promote changes through environments.
- Monitor sync status and health in Argo CD so drift can be detected quickly.

## Notes

This module is designed to help you learn how to configure and operate Argo CD Projects in a production-style GitOps workflow. If the exact file names differ in your copy of the repository, adapt the setup commands to point at the correct manifests.
