# Helm chart for Percona Everest

This repository contains a PoC Helm chart for the [Percona Everest](https://github.com/percona/everest) project.

> NOTE: This is an early-stage Proof of Concept (PoC) Helm chart. While it's still evolving and may not have full documentation or all features in place, we welcome your feedback and contributions to help improve it! Please feel free to explore, experiment, and collaborate with us as we work together to enhance its stability and functionality.

## Usage

### Install the Helm Chart

To get started with **Percona Everest** using **Helm**, follow these steps:

1. Add the Percona Everest Helm repository:

```bash
helm repo add everest-poc https://mayankshah1607.github.io/everest-helm-chart/
```

2. Install the Helm chart:

```bash
helm install everest everest/everest \
    --namespace=everest-system \
    --create-namespace \
    --version=1.1.1
```

This command installs the Everest chart into the `everest-system` namespace, creating the namespace if it doesn't already exist.

Expected Output:

After a few minutes, you should see an output similar to the following:

```bash
NAME: everest
LAST DEPLOYED: Wed Sep 11 13:54:08 2024
NAMESPACE: everest-system
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

This indicates that Percona Everest has been successfully deployed.

#### Retrieving Admin Credentials

Use `admin` as the default username for Percona Everest. To retrieve the password, run the following command:

```bash
kubectl get secret everest-accounts -n everest-system -o jsonpath='{.data.users\.yaml}' | base64 --decode  | yq '.admin.passwordHash'
```

This will return the password hash for the admin user.

Example Output:

```bash
8VpkqQ3lbQXR37psjbqNtdxAbWgSjCUwFJv2Qy82vAnbRMX10zaEYOUEXcz2hmG9
```

#### Setting Up Percona Everest

Once the installation is complete, you can forward the service port to access the Percona Everest User Interface (UI):

```bash
kubectl port-forward svc/everest 8080:8080 -n everest-system
```

Example Output:

```bash
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
Handling connection for 8080
Handling connection for 8080
Handling connection for 8080
```

You can now access the UI in your browser by navigating to `http://localhost:8080`.

#### Creating Your First Database

After logging into the UI, you can begin provisioning databases. For detailed steps on how to create a database, refer to the [official Percona Everest documentation](https://docs.percona.com/everest/use/db_provision.html).

### Upgrade

```bash
helm upgrade everest everest-poc/everest -n everest-system
```

### Uninstall

```bash
helm uninstall everest -n everest-system
```
