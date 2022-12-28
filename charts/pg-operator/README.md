# Percona Operator for PostgreSQL

This helm chart deploys the Kubernetes Operator to manage Percona Distribution for PostgreSQL.

Useful links:
- [Operator Github repository](https://github.com/percona/percona-postgresql-operator/)
- [Operator Documentation](https://www.percona.com/doc/kubernetes-operator-for-postgresql/index.html)

A job will be created based on `helm` `install`, `upgrade`, or `uninstall`. After the
job has completed the RBAC will be cleaned up.

## Pre-requisites
* Kubernetes 1.19+
* At least `v3.2.3` version of helm

# Installation

This chart will deploy the Operator Pod for the further PostgreSQL creation in Kubernetes.

## Installing the chart
To install the chart with the `pg-operator` release name using a dedicated namespace (recommended):

```sh
helm repo add percona https://percona.github.io/percona-helm-charts/
helm install my-operator percona/pg-operator --version 2.0.0 --namespace my-namespace --create-namespace
```

## Configuration

The following shows the configurable parameters that are relevant to the Helm
Chart.

| Parameter                       | Description                                                             | Default                                          |
| ------------------------------- | ------------------------------------------------------------------------| -------------------------------------------------|
| `image`| PG Operator Container image full path| `percona/percona-postgresql-operator:2.0.0` |
| `imagePullPolicy`| PG Operator Container pull policy| `Always`|
| `imagePullSecrets`| PG Operator Pod pull secret| `[]`|
| `replicaCount`| PG Operator Pod quantity| `1`|
| `tolerations`| List of node taints to tolerate| `[]`|
| `resources`| Resource requests and limits| `{}`|
| `nodeSelector`| Labels for Pod assignment| `{}`|
| `disableTelemetry`| Disable sending PXC Operator telemetry data to Percona| `false`|
| `operatorDebug`| Enable/disable operators' extended log output | `false` |
| `watchNamespace`| Set this variable if the target cluster namespace differs from operators namespace | `` |
| `watchAllNamespaces`| K8S Cluster-wide operation | `false` |


## Deploy the database

To deploy Percona Operator for PostgreSQL cluster with disabled telemetry run the following command:

```sh
helm install my-db percona/pg-db --version 2.0.0 --namespace my-namespace
```

See more about Percona Operator for PostgreSQL deployment in its chart [here](https://github.com/percona/percona-helm-charts/tree/main/charts/pg-db) or in the [Helm chart installation guide](https://www.percona.com/doc/kubernetes-operator-for-postgresql/helm.html).
