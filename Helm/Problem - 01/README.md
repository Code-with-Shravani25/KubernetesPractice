# Helm
---
- It is a package manager in kubernetes
- It helps you install, configure, and manage applications on Kubernetes clusters using reusable, pre-configured packages called charts.
- Helm is a tool that makes deploying and managing Kubernetes applications faster, repeatable, and less error-prone.
- Core idea
  - Instead of manually writing and applying many Kubernetes YAML files, Helm lets you bundle them together and manage them as a single unit.
## Key concepts
1. Chart
- A Helm package containing Kubernetes resource definitions (like deployments, services, etc.).
2. Release
- A running instance (one installed and deployed copy of an application in your cluster) of a chart in a Kubernetes cluster.
3. Values
- Configuration variables you can customize when installing a chart.
4. Repository
- A place where charts are stored and shared.
---
## What Helm does for you

- Simplifies deployment of complex apps
- Manages versioning and upgrades
- Supports rollbacks to previous versions
- Makes configuration reusable and customizable

