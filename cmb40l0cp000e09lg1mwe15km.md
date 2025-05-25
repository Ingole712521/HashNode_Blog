---
title: "Grafana & Prometheus"
seoTitle: "Grafana & Prometheus"
seoDescription: "Observability is the ability to understand what's happening inside a system based on the data it emits. "
datePublished: Sun May 25 2025 18:51:00 GMT+0000 (Coordinated Universal Time)
cuid: cmb40l0cp000e09lg1mwe15km
slug: grafana-and-prometheus
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1748198290484/280d3984-8997-4a1a-8faa-6aa08c38b93a.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1748198282140/8014dd02-f187-41de-b2ed-7b4fcc3b8797.jpeg
tags: web-performance, devops, opensourcemonitoring, docker-kubernetes-aws-jenkins-prometheus-grafana-sonarqube-trivy-helm-argocd, nodejsobservability, backendmetrics, frontendtelemetry, loggingandtracing, performanceengineering, reactmonitoring

---

## 📌 Why Observability Matters

Observability is the ability to understand what's happening inside a system based on the data it emits. In software, this means using:

* **Metrics**: Numeric values over time (e.g., request count)
    
* **Logs**: Events and errors
    
* **Traces**: Request flows through systems
    

For developers, this means catching performance bottlenecks, detecting downtime, and optimizing user experience proactively.

---

## 🔎 What is Prometheus?

Prometheus is an open-source monitoring and alerting system built for reliability and scale.

### 🔧 Core Features:

* **Pull-based model**: Prometheus scrapes targets over HTTP
    
* **Time-series storage**: Optimized database
    
* **Flexible querying with PromQL**
    
* **Rules & alerts**: Define thresholds to notify incidents
    

### ⚙ Prometheus Components:

* **Prometheus Server**: Core scraper and query engine
    
* **Exporters**: Convert metrics to Prometheus format
    
* **PushGateway**: Accepts metrics from short-lived jobs
    
* **AlertManager**: Handles alert routing, silencing, grouping
    

### 📊 Example Metric:

```plaintext
http_requests_total{method="GET", path="/", status="200"} 12
```

### 📘 Prometheus Architecture Diagram:

![Prometheus architecture](https://prometheus.io/assets/architecture.png align="left")

---

## 🎨 What is Grafana?

Grafana is a visualization platform that helps turn time-series data into dashboards.

### 🌟 Key Features:

* Multiple data sources (Prometheus, Loki, InfluxDB, SQL, etc.)
    
* Beautiful, customizable dashboards
    
* Alerting, sharing, annotations
    
* User roles, folders, and provisioning
    

### 📋 Grafana Key Terms:

* **Panel**: A chart, graph, gauge, or stat
    
* **Dashboard**: Collection of panels
    
* **Data Source**: Backend connection (e.g., Prometheus)
    
* **Variables**: For dynamic dashboards
    

---

## 🏗 System Architecture Overview

Here’s how data flows in your observability setup:

```xml
React App
   ↓
Sends metrics to → Node.js App → /metrics
                         ↑
Prometheus scrapes ←──────
                         ↓
Grafana visualizes ←──── Prometheus data
```

### Optional Path for Short-Lived Jobs:

```plaintext
Job → PushGateway → Prometheus → Grafana
```

---

## ⚙️ Setting Up Your Monitoring Stack

### Requirements

* Node.js + TypeScript
    
* React + TypeScript
    
* Docker
    

Install backend dependencies:

```bash
npm install express prom-client
npm install typescript ts-node @types/node @types/express --save-dev
```

Frontend (React):

```bash
npx create-react-app react-metrics-app --template typescript
npm install axios
```

---

## 🧠 Optimized Node.js Backend

### Step 1: `metrics.ts`

```ts
import { Counter, Gauge, Histogram, collectDefaultMetrics, Registry } from 'prom-client';

export const register = new Registry();
collectDefaultMetrics({ prefix: 'nodejs_', register });

export const httpCounter = new Counter({
  name: 'http_requests_total',
  help: 'Total HTTP requests',
  labelNames: ['method', 'path', 'status_code'],
  registers: [register],
});

export const userGauge = new Gauge({
  name: 'active_users',
  help: 'Active users count',
  registers: [register],
});

export const httpDuration = new Histogram({
  name: 'http_request_duration_seconds',
  help: 'Request duration in seconds',
  labelNames: ['method', 'path', 'status_code'],
  buckets: [0.1, 0.3, 0.5, 1, 2, 5],
  registers: [register],
});
```

### Step 2: `index.ts`

```ts
import express from 'express';
import { register, httpCounter, httpDuration, userGauge } from './metrics';

const app = express();
app.use(express.json());

app.use((req, res, next) => {
  const timer = httpDuration.startTimer({ method: req.method, path: req.path });
  res.on('finish', () => {
    httpCounter.inc({ method: req.method, path: req.path, status_code: res.statusCode.toString() });
    timer({ status_code: res.statusCode.toString() });
  });
  next();
});

app.get('/users', (req, res) => {
  userGauge.set(Math.floor(Math.random() * 100));
  res.json([{ id: 1, name: 'Alice' }]);
});

app.get('/metrics', async (req, res) => {
  res.set('Content-Type', register.contentType);
  res.end(await register.metrics());
});

app.listen(3000, () => console.log('Server running on http://localhost:3000'));
```

---

## 🌐 Sending Metrics from React

### `metricsService.ts`

```ts
import axios from 'axios';

export const sendMetric = async (name: string, value: number, labels: Record<string, string>) => {
  await axios.post('http://localhost:3000/api/metrics', { name, value, labels });
};
```

### `App.tsx`

```tsx
import { useEffect } from 'react';
import { sendMetric } from './metricsService';

function App() {
  useEffect(() => {
    const loadTime = performance.now() / 1000;
    sendMetric('frontend_page_load_duration', loadTime, { page: 'home' });
  }, []);

  return (
    <div>
      <h1>Hello Metrics</h1>
    </div>
  );
}

export default App;
```

### Backend Route to Accept Frontend Metrics

```ts
app.post('/api/metrics', (req, res) => {
  const { name, value, labels } = req.body;
  if (name === 'frontend_page_load_duration') {
    frontendPageLoadDuration.observe(labels, value);
  }
  res.sendStatus(200);
});
```

---

## 📡 Configuring Prometheus

### `prometheus.yml`

```yaml
global:
  scrape_interval: 15s
scrape_configs:
  - job_name: 'nodejs_app'
    static_configs:
      - targets: ['host.docker.internal:3000']
```

### Run Prometheus

```bash
docker run -d --name prometheus -p 9090:9090 \
  -v $(pwd)/prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus
```

---

## 📊 Visualizing with Grafana

### Run Grafana

```bash
docker run -d --name=grafana -p 3000:3000 grafana/grafana
```

Login: `admin / admin` → Change password → Add data source → Prometheus URL

### Connect to Prometheus:

* URL: `http://host.docker.internal:9090`
    
* Save & Test
    

---

## 📈 Frontend + Backend Dashboards

### Request Rate Panel

```plaintext
rate(http_requests_total[5m])
```

### P95 Latency Panel

```plaintext
histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (le, path))
```

### Page Load Time Panel (React)

```plaintext
histogram_quantile(0.95, sum(rate(frontend_page_load_duration_bucket[5m])) by (le, page))
```

---

## 🚨 Bonus: Alerting & Automation

### Prometheus Alerts

```yaml
alerting:
  alertmanagers:
    - static_configs:
        - targets: ['localhost:9093']
```

### Grafana Alerts

* Go to any panel → Alert tab → Set rule
    
* Condition: `WHEN avg() OF query > threshold`
    
* Notifications: Slack, Email, PagerDuty, Webhook
    

---

## 🎯 Conclusion

Implementing comprehensive observability with Prometheus and Grafana empowers you to gain deep insights into both your backend and frontend applications. By systematically capturing metrics such as request rates, latency distributions, and user experience data, you can proactively identify bottlenecks, track system health, and optimize performance with confidence.

This guide walked you through setting up a robust monitoring stack using TypeScript for type safety and maintainability, integrating metrics collection in your Node.js backend and React frontend, and visualizing real-time data with Grafana dashboards. Leveraging alerting mechanisms further strengthens your ability to respond swiftly to incidents, minimizing downtime and improving reliability.

Ultimately, observability is a critical pillar for modern software development and operations. By adopting these best practices, you not only enhance your system’s resilience but also create a data-driven culture that fosters continuous improvement and exceptional user experiences.

Keep evolving your monitoring strategies as your applications grow, and never underestimate the power of visibility in building trustworthy, scalable systems.

Happy monitoring! 🚀

---

## ✅ Best Practices Recap

| Tip | Description |
| --- | --- |
| Use labels | Helps filter metrics easily |
| Use middleware | Automatically track all routes |
| Histogram for latency | Enables P95/P99 insights |
| Docker for infra | Quick setup for local dev |
| TypeScript typing | Reduces metric name typos |

---

## 📚 Resources

* [Prometheus Docs](https://prometheus.io/docs/)
    
* [Grafana Docs](https://grafana.com/docs/)
    
* [prom-client GitHub](https://github.com/siimon/prom-client)
    
* [Grafana Dashboard Repo](https://grafana.com/grafana/dashboards/)
    

> 🚀 With this setup, you now have full visibility from server performance to user experience!

**Connect with us:**

* Hashnode: [https://hashnode.com/@Nehal71](https://hashnode.com/@Nehal71)
    
* Twitter : [https://twitter.com/IngoleNehal](https://twitter.com/IngoleNehal)
    
* LinkedIn: [https://www.linkedin.com/in/nehal-ingole/](https://www.linkedin.com/in/nehal-ingole/)