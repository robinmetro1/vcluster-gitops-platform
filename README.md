# Kubernetes inside Kubernetes" — A Self-Service Multi-Tenant Platform
A lightweight Cluster-as-a-Service (CaaS) platform using vcluster and ArgoCD. Providing on-demand, isolated Kubernetes environments with a minimal footprint

📖 Overview

In a typical on-prem environment, spinning up a new Kubernetes cluster is slow and resource-heavy. This project demonstrates a Platform Engineering approach to solving that.

Instead of creating new VMs, I use vcluster to create fully isolated, "virtual" Kubernetes clusters inside a single namespace of a host cluster. Everything is managed via GitOps (ArgoCD), making cluster creation as easy as pushing a YAML file.
