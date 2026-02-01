# vcluster Requests

This directory contains vcluster configuration files. Each file represents a virtual Kubernetes cluster request.

## How to Request a vcluster

### Step 1: Copy the Template
```bash
cp templates/request-template.yaml vclusters/my-team.yaml
```

### Step 2: Customize Your Configuration

Edit `vclusters/team-my-team.yaml`:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-team-vcluster-config
  namespace: my-team  # Your namespace
  labels:
    app: vcluster
    team: my-team
data:
  values.yaml: |
    resources:
      limits:
        cpu: 2000m      # Adjust as needed
        memory: 1Gi     # Adjust as needed
      requests:
        cpu: 500m
        memory: 512Mi
    storage:
      size: 10Gi        # Adjust as needed
```

### Step 3: Commit and Push
```bash
git add vclusters/my-team.yaml
git commit -m "Request vcluster for my-team"
git push origin main
```

### Step 4: Wait for Provisioning

ArgoCD will automatically:
1. Detect your new file
2. Create a namespace for your team
3. Deploy your vcluster
4. Provision isolated Kubernetes environment

### Step 5: Access Your vcluster
```bash
# List available vclusters
vcluster list

# Connect to your vcluster
vcluster connect my-team -n my-team

# Now you're inside your virtual cluster!
kubectl get nodes
kubectl get namespaces
```

## Current vclusters

| Team | Namespace | Status | Created |
|------|-----------|--------|---------|
| (none yet) | - | - | - |

## Resource Limits

- **Default CPU Limit**: 1 core
- **Default Memory Limit**: 512Mi
- **Default Storage**: 5Gi
- **Max CPU Limit**: 4 cores
- **Max Memory Limit**: 8Gi
- **Max Storage**: 50Gi

