# Helm chart for Percona Everest

This repository contains a PoC Helm chart for the [Percona Everest](https://github.com/percona/everest) project.

> NOTE: This is a PoC only and not meant for production use. It is still unpolished, lacks proper documentation,
and contains many hacks.

## Usage

### Install

```bash
helm repo add everest https://mayankshah1607.github.io/everest-helm-chart/
helm install everest everest/everest \
    --namespace=everest-system \
    --create-namespace \
    --version=1.1.1
```

### Upgrade
```bash
helm upgrade everest everest-poc/everest -n everest-system
```

### Uninstall

```bash
helm uninstall everest -n everest-system
```
