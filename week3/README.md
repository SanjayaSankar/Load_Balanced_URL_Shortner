## Week 3: Scaling, Load Balancing & Monitoring

This folder contains the Kubernetes configurations for scaling, load balancing, and monitoring the URL shortener service.

## File Structure
```
week3/
├── k8s/
│   ├── url-shortener-hpa.yaml              # Horizontal Pod Autoscaler
│   ├── ingress.yaml                        # Ingress for better traffic routing
│   └── prometheus-grafana/                 # Monitoring setup
│       ├── prometheus-config.yaml
│       └── grafana-deployment.yaml
├── stress-test/
│   └── locustfile.py                      # Load testing script
└── README.md                              # Documentation

## Deployment and Testing Instructions

1. Apply the Horizontal Pod Autoscaler:
   ```
   kubectl apply -f k8s/url-shortener-hpa.yaml
   ```

2. Install NGINX Ingress Controller (if not already installed):
   ```
   # For Minikube
   minikube addons enable ingress
 
   ```

3. Apply the Ingress configuration:
   ```
   kubectl apply -f k8s/ingress.yaml
   ```

4. Set up monitoring with Prometheus and Grafana:
   ```
   kubectl apply -f k8s/prometheus-grafana/prometheus-config.yaml
   kubectl apply -f k8s/prometheus-grafana/grafana-deployment.yaml
   ```

5. Check the deployment status:
   ```
   kubectl get pods
   kubectl get services
   kubectl get hpa
   kubectl get ingress
   ```

6. Run a stress test using Locust:
   ```
   # Install Locust
   pip install locust
   
   # Start the Locust test
   cd stress-test
   locust -f locustfile.py --host=http://URL_OF_YOUR_SERVICE
   
   # Open Locust web interface at http://localhost:8089
   ```

7. Monitor the autoscaling:
   ```
   kubectl get hpa url-shortener-hpa --watch
   ```

8. Access Grafana for monitoring:
   ```
   # For Minikube
   minikube service grafana-service --url
   
   # For other environments, use the appropriate method to access the Grafana service
   ```

9. Set up Grafana:
   - Login with username 'admin' and password 'admin'
   - Add Prometheus as a data source (URL: http://prometheus-service:9090)
   - Import dashboards for Kubernetes and custom metrics

10. View logs:
    ```
    kubectl logs -l app=url-shortener
    ```