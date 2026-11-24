# BGG Application Deployment & Local Access Guide

## 1. Deploy Manifests in Sequence
Apply the configuration, database, and backend application manifests in order:

```bash
kubectl apply -f configmap.yaml
kubectl apply -f deployment-db.yaml
kubectl apply -f deployment-app.yaml
```

*(Note: `bggns` namespace is included in `configmap.yaml` so it is created first)*

---

## 2. Verify Pods Are Ready
Wait until all pods in the `bggns` namespace show `1/1` under `READY` and `Running` under `STATUS`:

```bash
kubectl get pods -n bggns
```
---

## 3. Port-Forward to Access Locally
Because this cluster runs inside Kind (Docker), forward local port `8080` to the `bggapp-svc` service:

```bash
kubectl port-forward svc/bggapp-svc 8080:8080 -n bggns
```

* Keep this terminal window open while using the app.
* Open your browser and go to: **`http://localhost:8080`**
* Health check endpoint: **`http://localhost:8080/healthz`**
* Press `Ctrl + C` in the terminal to stop port-forwarding.

---

## 4. Cleanup
To delete the namespace and all deployed resources:

```bash
kubectl delete ns bggns
```
