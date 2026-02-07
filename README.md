# vcluster GitOps Platform

A self-service platform for creating virtual Kubernetes clusters on-demand using GitOps principles.

## 🎯 Project Overview

This platform enables developers to request isolated Kubernetes clusters by simply committing a YAML file to Git. ArgoCD automatically provisions a virtual cluster (vcluster) in response, providing true "Clusters-as-a-Service."

### Why This Matters

- 💰 **cost reduction** vs. dedicated clusters per team
- ⚡ **5-minute provisioning** time (vs. days for traditional clusters)
- 🔒 **Complete isolation** between teams
- 📝 **Full audit trail** via Git history
- 🚀 **Zero ops overhead** for developers

---

**Components:**
- **Host Cluster**: k3d (Kubernetes v1.35)
- **GitOps Engine**: ArgoCD
- **Virtual Clusters**: vcluster
- **Automation**: ArgoCD ApplicationSet
## 🏗️ Architecture

### High-Level Flow
```
┌──────────────┐      ┌─────────────┐      ┌──────────────┐      ┌─────────────────┐
│  Developer   │──────▶│     Git     │──────▶│   ArgoCD     │──────▶│   vcluster      │
│  (Team-Alpha)│ Commit│  (GitHub)   │ Watch │ ApplicationSet│Deploy │ (Isolated K8s)  │
└──────────────┘      └─────────────┘      └──────────────┘      └─────────────────┘
```

### Infrastructure Stack
```
┌─────────────────────────────────────────────────────────────┐
│                    k3d Host Cluster (v1.35)                  │
│  ┌────────────────┐  ┌────────────────┐  ┌───────────────┐ │
│  │  team-alpha    │  │   team-beta    │  │  team-gamma   │ │
│  │  namespace     │  │   namespace    │  │  namespace    │ │
│  │  ┌──────────┐  │  │  ┌──────────┐  │  │ ┌──────────┐  │ │
│  │  │ vcluster │  │  │  │ vcluster │  │  │ │ vcluster │  │ │
│  │  │   pods   │  │  │  │   pods   │  │  │ │   pods   │  │ │
│  │  └──────────┘  │  │  └──────────┘  │  │ └──────────┘  │ │
│  └────────────────┘  └────────────────┘  └───────────────┘ │
│                                                              │
│  ┌────────────────────────────────────────────────────────┐ │
│  │              ArgoCD (GitOps Controller)                 │ │
│  └────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────┘
```
## 📁 Repository Structure
```
vcluster-gitops-platform/
├── README.md
├── argocd/
│   ├── applications/
│   │   └── vcluster-appset.yaml       # ArgoCD ApplicationSet
│   └── install/
│       └── argocd-install.yaml        # ArgoCD installation manifests
├── vclusters/
│   ├── team-alpha.yaml                # Example: Team Alpha's vcluster
│   ├── team-beta.yaml                 # Example: Team Beta's vcluster
│   └── README.md                      # How to request a vcluster
├── templates/
│   ├── vcluster-values.yaml           # Default vcluster Helm values
│   └── request-template.yaml          # Template for developers
└── docs/
    ├── architecture.md                # Architecture diagrams
    ├── setup.md                       # Setup instructions
    └── usage.md                       # User guide
```

## 🚀 How It Works

### For Developers (Self-Service)

1. Copy `templates/request-template.yaml` to `vclusters/your-team.yaml`
2. Customize with your team name and resource limits
3. Commit and push to Git
4. ArgoCD automatically creates your isolated Kubernetes cluster
5. Access credentials are provided via Kubernetes secrets

### For Platform Teams

ArgoCD monitors the `vclusters/` directory and automatically:
- Detects new vcluster requests
- Validates resource limits
- Provisions the virtual cluster
- Manages lifecycle (updates, deletions)

## 💡 Key Features

- ✅ **GitOps-Driven**: All infrastructure as code
- ✅ **Self-Service**: Developers provision clusters without platform team intervention
- ✅ **Multi-Tenancy**: Multiple isolated clusters on shared infrastructure
- ✅ **Cost-Efficient**: Virtual clusters share node resources
- ✅ **Audit Trail**: Full Git history of all cluster requests
- ✅ **Declarative**: Kubernetes-native configuration

## 🛠️ Tech Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| Host Cluster | k3d | Lightweight Kubernetes for local dev |
| Virtual Clusters | vcluster | Isolated K8s environments |
| GitOps | ArgoCD | Automated deployment pipeline |
| Version Control | Git/GitHub | Source of truth |

## 📋 Prerequisites

- Docker
- kubectl
- k3d
- vcluster CLI
- ArgoCD CLI (optional)

## 🏁 Quick Start

### 1. Create Host Cluster

### 2. Install ArgoCD


### 3. Deploy ApplicationSet

### 4. Request a vcluster
```bash
cp templates/request-template.yaml vclusters/my-team.yaml
# Edit my-team.yaml with your configuration
git add vclusters/my-team.yaml
git commit -m "Request vcluster for my-team"
git push
```

ArgoCD will automatically provision your cluster!

## 📊 Project Goals

This project demonstrates:

1. **Platform Engineering**: Building internal developer platforms
2. **Multi-Tenancy**: Secure resource isolation
3. **GitOps**: Declarative infrastructure management
4. **Automation**: Reducing manual operational overhead
5. **Cost Optimization**: Efficient resource utilization


## 🔗 Links

- [vcluster Documentation](https://www.vcluster.com/docs)
- [ArgoCD Documentation](https://argo-cd.readthedocs.io/)
- [GitOps Principles](https://opengitops.dev/)
