

# 🚀 URL Shortener Project (Docker + Kubernetes + Scaling & Monitoring)

This is a full-fledged URL Shortener system built using Python Flask and containerized with Docker. The project progresses through three phases:

* **Week 1:** Local Docker-based development
* **Week 2:** Kubernetes deployment
* **Week 3:** Scaling, Load Balancing, and Monitoring

---

## 📁 Project Structure

```
.
├── week1/                  # Flask app with Docker setup
├── week2/                  # Kubernetes deployment configs
└── week3/                  # Autoscaling, Ingress, and Monitoring setup
```

---

## 🔗 Features

* Shorten any long URL via a REST API
* Store and retrieve mappings from Redis
* Containerized using Docker
* Deployable on any Kubernetes cluster
* Auto-scaled using Horizontal Pod Autoscaler
* Load-balanced using Ingress
* Monitored using Prometheus & Grafana
* Stress-tested with Locust

---

## 🧑‍💻 Week 1: Local Docker Setup

### 🔧 How to Run Locally

1. **Navigate to Week 1 Folder**

   ```bash
   cd week1
   ```

2. **Start the Containers**

   ```bash
   docker-compose up -d
   ```

3. **Test the API**

   ```bash
   curl -X POST http://localhost:5000/shorten \
     -H "Content-Type: application/json" \
     -d '{"url": "https://example.com"}'
   ```

4. **Stop the Containers**

   ```bash
   docker-compose down
   ```

---

## ☸️ Week 2: Kubernetes Deployment

### 🌐 How to Deploy on Minikube

1. **Build the Docker Image Inside Minikube**

   ```bash
   cd ../week1
   eval $(minikube docker-env)
   docker build -t url-shortener:latest ./app
   ```

2. **Deploy from Week 2 Directory**

   ```bash
   cd ../week2
   ```

3. **Deploy Redis**

   ```bash
   kubectl apply -f k8s/redis-deployment.yaml
   kubectl apply -f k8s/redis-service.yaml
   ```

4. **Apply ConfigMap and Secret**

   ```bash
   kubectl apply -f k8s/configmap.yaml
   kubectl apply -f k8s/secret.yaml
   ```

5. **Deploy URL Shortener App**

   ```bash
   kubectl apply -f k8s/url-shortener-deployment.yaml
   kubectl apply -f k8s/url-shortener-service.yaml
   ```

6. **Access the Application**

   ```bash
   minikube service url-shortener-service --url
   ```

7. **Test from Ubuntu Terminal**

   ```bash
   curl -X POST http://<MINIKUBE_URL>/shorten \
     -H "Content-Type: application/json" \
     -d '{"url": "https://example.com"}'
   ```

---

## 📈 Week 3: Scaling, Ingress & Monitoring

### ⚙️ Setup Autoscaling and Ingress

1. **Enable Ingress (Minikube)**

   ```bash
   minikube addons enable ingress
   ```

2. **Apply Horizontal Pod Autoscaler**

   ```bash
   kubectl apply -f k8s/url-shortener-hpa.yaml
   ```

3. **Apply Ingress Configuration**

   ```bash
   kubectl apply -f k8s/ingress.yaml
   ```

### 📊 Monitoring with Prometheus & Grafana

4. **Deploy Monitoring Stack**

   ```bash
   kubectl apply -f k8s/prometheus-grafana/prometheus-config.yaml
   kubectl apply -f k8s/prometheus-grafana/grafana-deployment.yaml
   ```

5. **Access Grafana**

   ```bash
   minikube service grafana-service --url
   ```

6. **Grafana Setup**

   * **Login**: `admin` / `admin`
   * **Add Data Source**: Prometheus ([http://prometheus-service:9090](http://prometheus-service:9090))
   * **Import Dashboards** for Kubernetes metrics

---

## 🧪 Load Testing with Locust

1. **Install Locust**

   ```bash
   pip install locust
   ```

2. **Start the Test**

   ```bash
   cd week3/stress-test
   locust -f locustfile.py --host=http://<INGRESS_OR_SERVICE_URL>
   ```

3. **Access Locust UI**

   * [http://localhost:8089](http://localhost:8089)

---

## 📋 Commands Cheat Sheet

```bash
# View all pods
kubectl get pods

# View services
kubectl get services

# View autoscaling
kubectl get hpa

# View ingress rules
kubectl get ingress

# View application logs
kubectl logs -l app=url-shortener
```

---

## 📦 Tech Stack

* **Backend**: Python Flask
* **Database**: Redis
* **Containerization**: Docker, Docker Compose
* **Orchestration**: Kubernetes (Minikube)
* **Monitoring**: Prometheus & Grafana
* **Load Testing**: Locust
* **Scaling**: Kubernetes HPA
* **Routing**: NGINX Ingress Controller

---

## 📚 Resources

* [Flask Documentation](https://flask.palletsprojects.com/)
* [Kubernetes Documentation](https://kubernetes.io/docs/home/)
* [Prometheus Docs](https://prometheus.io/docs/)
* [Grafana Docs](https://grafana.com/docs/)
* [Locust Docs](https://docs.locust.io/)

---
