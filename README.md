# Kubernetes Cheatsheet

## Grundlagen

### Kubernetes Konfiguration
```sh
export KUBECONFIG=./configmap.txt  # Setzt die Konfigurationsdatei
kubectl cluster-info  # Zeigt Cluster-Informationen an
kubectl get nodes  # Listet alle Nodes im Cluster
```

### Namespace-Verwaltung
```sh
kubectl create namespace xxx  # Erstellt einen Namespace
```

## Pods und Deployments

### Pod erstellen und verwalten
```sh
kubectl apply -f pod.yaml  # Erstellt oder aktualisiert einen Pod
kubectl delete pod -n namespace  # Löscht einen Pod
kubectl delete pods --all -n namespace # Löscht alle Pods im Namespace
```

## Check the cluster

``` bash
kubectl get pods -n <your_namespace>

kubectl get svc -n <your_namespace>

kubectl get ing -n <your_namespace>

kubectl logs <pod_name> -n <your_namespace>

kubectl describe pod <pod_name> -n <your_namespace>
```



## ConfigMaps und Secrets

### ConfigMap erstellen und verwalten
```sh
echo "Dein Konfigurationsinhalt" > config  # Erstellt eine Konfigurationsdatei
kubectl create configmap configfile-map -n namespace --from-file=config  # Erstellt eine ConfigMap
kubectl get configmaps -n namespace  # Listet alle ConfigMaps
```

## ServiceAccounts und Security

### ServiceAccount für Pods
```sh
kubectl create serviceaccount custom-sa  # Erstellt einen spezifischen ServiceAccount
kubectl apply -f serviceaccount.yaml  # Bindet einen ServiceAccount an einen Pod
```

### Sicherheitskontext setzen
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secure-pod
spec:
  securityContext:
    runAsUser: 1000  # Führt den Pod mit User-ID 1000 aus
```

## Networking in Kubernetes

### Innerhalb des Pods und Clusters
- **Container Networking Interface (CNI)**: Standard für Netzwerk-Plugins
- **CoreDNS**: Kubernetes-interne DNS-Lösung
- **Service Discovery**: Erlaubt das Finden anderer Dienste über DNS

### Externe Erreichbarkeit
- **Ingress API**: Regelbasierter HTTP/S-Zugang
- **Gateway API**: Moderner Ersatz für Ingress
- **Network Policies**: Regeln für Traffic-Kontrolle

## Deployment-Strategien

### Blue/Green Deployment
- Zwei Versionen laufen parallel, Traffic wird schrittweise umgeleitet

### Canary Deployment
- Eine kleine Anzahl an Nutzern erhält die neue Version, bevor sie vollständig ausgerollt wird

### Rolling Updates
- Anwendung wird schrittweise aktualisiert, ohne Downtime

## Storage in Kubernetes

### Ephemeral Storage
- **emptyDir**: Temporäre Speicherung, gelöscht nach Pod-Neustart
- **ConfigMaps, Secrets, Downward API**: Speicherung von Konfigurationsdaten

### Persistent Storage
- **PersistentVolumes (PV) & PersistentVolumeClaims (PVC)**: Externe Speicherzuweisung
- **Container Storage Interface (CSI)**: API für Storage-Plugins

## Health Checks und Resilienz

### Probes (Gesundheitsprüfungen)
- **Liveness Probe**: Neustartet fehlerhafte Container
- **Readiness Probe**: Markiert Pods als bereit oder nicht bereit
- **Startup Probe**: Verhindert zu frühe Anfragen an den Container

### Ressourcenverwaltung
- **Resource Quotas**: Begrenzen Ressourcenverbrauch pro Namespace
- **Limit Ranges**: Setzen Minimal- und Maximalwerte für CPU & Speicher


