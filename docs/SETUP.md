# Container Platform Setup Guide

## Prerequisites

1. Install Docker Desktop:
   ```bash
   # Windows (using winget)
   winget install Docker.DockerDesktop

   # macOS (using brew)
   brew install --cask docker
   ```

2. Install Kubernetes CLI:
   ```bash
   # Windows (using chocolatey)
   choco install kubernetes-cli

   # macOS
   brew install kubernetes-cli
   ```

3. Install Helm:
   ```bash
   # Windows
   choco install kubernetes-helm

   # macOS
   brew install helm
   ```

## Step-by-Step Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/nived2/container-platform.git
   cd container-platform
   ```

2. Create Kubernetes namespace:
   ```bash
   kubectl apply -f kubernetes/namespace.yaml
   ```

3. Deploy monitoring stack:
   ```bash
   # Add Prometheus repository
   helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
   helm repo update

   # Install Prometheus stack
   helm install prometheus prometheus-community/kube-prometheus-stack -n container-platform
   ```

4. Deploy microservices:
   ```bash
   kubectl apply -f kubernetes/deployments/
   ```

5. Verify deployment:
   ```bash
   kubectl get pods -n container-platform
   kubectl get services -n container-platform
   ```

## Accessing Services

1. Prometheus:
   ```bash
   kubectl port-forward service/prometheus-grafana 3000:80 -n container-platform
   # Access at http://localhost:3000
   # Default credentials: admin/prom-operator
   ```

2. Application:
   ```bash
   kubectl port-forward service/microservice 8080:80 -n container-platform
   # Access at http://localhost:8080
   ```

## Monitoring Setup

1. Access Grafana dashboard:
   - URL: http://localhost:3000
   - Username: admin
   - Password: prom-operator

2. Import dashboards:
   - Go to Dashboard → Import
   - Import dashboard ID: 315 (Kubernetes cluster monitoring)

## Scaling

1. Scale manually:
   ```bash
   kubectl scale deployment microservice --replicas=3 -n container-platform
   ```

2. Enable autoscaling:
   ```bash
   kubectl autoscale deployment microservice --min=2 --max=5 --cpu-percent=80 -n container-platform
   ```

## Troubleshooting

1. Check pod status:
   ```bash
   kubectl describe pod <pod-name> -n container-platform
   ```

2. View logs:
   ```bash
   kubectl logs <pod-name> -n container-platform
   ```

3. Common issues:
   - ImagePullBackOff: Check image name and registry credentials
   - CrashLoopBackOff: Check application logs and configuration
   - Pending: Check cluster resources and node availability

## Cleanup

1. Remove all resources:
   ```bash
   kubectl delete namespace container-platform
   ```

2. Uninstall Prometheus:
   ```bash
   helm uninstall prometheus -n container-platform
   ```

## Security Best Practices

1. Enable RBAC:
   ```bash
   kubectl apply -f kubernetes/rbac/
   ```

2. Network policies:
   ```bash
   kubectl apply -f kubernetes/network-policies/
   ```

3. Regular updates:
   ```bash
   kubectl get nodes
   kubectl get pods -A -o wide
   ```

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## Support

For issues and support:
- Create an issue on GitHub
- Email: nivedmahendran547@gmail.com
