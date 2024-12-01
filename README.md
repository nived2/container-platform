# Container Platform

A scalable container platform built with Docker and Kubernetes, supporting multiple microservices with automated deployment.

## Features

- Multi-service architecture with Kubernetes orchestration
- Automated deployment pipeline
- Monitoring with Prometheus
- Service discovery and load balancing
- Helm charts for package management
- Horizontal pod autoscaling
- Persistent volume management

## Prerequisites

- Docker Desktop with Kubernetes enabled
- Helm v3.x
- kubectl CLI
- Prometheus Operator

## Project Structure

```
container-platform/
├── kubernetes/           # Kubernetes manifests
│   ├── deployments/     # Service deployments
│   ├── services/        # Service configurations
│   └── configmaps/      # Configuration files
├── helm-charts/         # Helm chart definitions
│   └── microservices/   # Charts for each service
├── monitoring/          # Prometheus configurations
│   ├── prometheus/      # Prometheus setup
│   └── grafana/        # Grafana dashboards
└── scripts/            # Deployment scripts
```

## Quick Start

For detailed setup instructions, please refer to our [Setup Guide](docs/SETUP.md).

1. Clone the repository:
```bash
git clone https://github.com/nived2/container-platform.git
cd container-platform
```

2. Deploy the platform:
```bash
# Initialize Kubernetes cluster
kubectl apply -f kubernetes/namespace.yaml

# Deploy Prometheus monitoring
helm install prometheus prometheus-community/kube-prometheus-stack

# Deploy microservices
helm install microservices helm-charts/microservices
```

3. Access the services:
```bash
# Get the service URLs
kubectl get ingress -n container-platform
```

## Monitoring

The platform includes comprehensive monitoring with Prometheus and Grafana:

- Prometheus: Metrics collection and alerting
- Grafana: Visualization and dashboards
- Custom metrics for application monitoring
- Alert manager for notification management

## Security

- RBAC implementation
- Network policies
- Pod security policies
- Secret management
- Container image scanning

## Scaling

The platform supports both vertical and horizontal scaling:

- Horizontal Pod Autoscaling (HPA)
- Vertical Pod Autoscaling (VPA)
- Cluster Autoscaling
- Load Balancing

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

MIT License - feel free to use this project for your own portfolio

## Contact

Nived Mahendran - nivedmahendran547@gmail.com
