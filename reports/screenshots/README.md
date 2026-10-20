# Deployment Evidence

Local Kubernetes (Docker Desktop) deployment verified on 2026-10-20. Screenshots document Kubernetes workloads, API endpoints, Grafana monitoring, GitHub Actions CI, and live kubectl/curl verification. See `../FINAL_REPORT.md` for results and `../../README.md` for setup and local API access.

The end-to-end pipeline video is hosted on Google Drive: [watch the recording](https://drive.google.com/file/d/1ZjDVIeZ9_H_q8ydrz-FwBvNCeN9P8ndM/view?usp=sharing).

## Screenshot inventory

| File | Contents |
|------|----------|
| `00-kubectl-cluster-info.png` | `kubectl get nodes` + `kubectl get all -n heart-disease` — cluster node Ready, all pods/services/deployments/replicasets running |
| `01-kubernetes-workloads.png` | `kubectl get pods,services -n heart-disease` — all three pods (API, Prometheus, Grafana) Running |
| `02-health-endpoint.png` | `GET /health` returning `{"status":"ok","model_loaded":"true"}` |
| `03-predict-endpoint.png` | `POST /predict` returning prediction, label, confidence, and probabilities |
| `04-grafana-dashboard.png` | Grafana Heart Disease API dashboard — Requests per second and 95th percentile latency panels |
| `05-grafana-dashboard-continued.png` | Grafana dashboard continued — Requests by status class and API target up panels |
| `06-github-actions-success.png` | GitHub Actions CI run showing successful `quality-and-training` job (green check) |
| `07-fastapi-swagger-ui.png` | FastAPI Swagger UI listing `GET /health` and `POST /predict` endpoints |
| `08-fastapi-swagger-predict-body.png` | Swagger `/predict` request body schema with all 13 feature fields |
| `09-fastapi-swagger-predict-response.png` | Swagger `/predict` response schemas (200 success, 422 validation error) |
| `10-fastapi-swagger-schemas.png` | Swagger data model schemas: `HeartDiseaseInput`, `PredictionResponse`, validation types |
| `11-fastapi-swagger-health-schema.png` | Swagger `/health` endpoint with 200 response schema |
| `12-docker-build-success.png` | Docker build terminal output — all 7 build steps completed, image tagged `heart-disease-api:latest` |
| `13-kubectl-pods-health-check.png` | Terminal: `curl /health` via Kubernetes port-forward returning `model_loaded: true` |
| `14-kubectl-predict-curl.png` | Terminal: `curl /predict` via Kubernetes port-forward returning `{"prediction":0,"label":"no_disease","confidence":0.5901,...}` |
| `15-mlflow-training-runs.png` | MLflow UI — heart-disease-model-development experiment showing both runs (Random Forest and Logistic Regression) |
| `16-mlflow-run-metrics.png` | MLflow Logistic Regression run — all 8 metrics logged (accuracy, precision, recall, ROC-AUC means and std deviations) |
| `17-mlflow-run-artifacts.png` | MLflow Logistic Regression run — artifacts tab showing outer CV metrics plot with accuracy 0.858, precision 0.864, recall 0.820, ROC-AUC 0.920 |
