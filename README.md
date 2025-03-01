# What it is

This project makes it easy for you to:
* Create a K3S cluster using Multipass virtual machine(s)
* Install Falco Helm chart (local files or published version number) with Kubernetes audit log enabled
* Optionally deploy Falco Sidekick with UI
* Optionally deploy Kubeless with `delete-pod` function (triggered by a running in a pod in `default` namespace)
  * Set up the whole chain of components `audit-logs` > `falco` > `falcosidekick` > `falcosidekick-ui` & `kubeless`
* Optinally run tests to check that Falco can detect a runtime event and a Kubernetes audit log event.

## Usage

```bash
# Create cluster, deploy chart, and execute tests with default values
make

# Check summary log
make summary

# In case of Falco pod errors, check logs
make pod_logs

# Setup kubeconfig to access the cluster 
export KUBECONFIG=~/.kube/k3s.yaml

# Just execute tests on existing cluster any number of times
make tests

# Destroy multipass cluster
make delete-cluster
```

Check `makefile` and `scripts/*.sh` for more options

### Additional examples

```bash
# Execute local Falco helm chart tests
git clone https://github.com/falcosecurity/charts.git

# Create cluster, deploy local chart, execute tests
make all-local-chart
```

```bash
# Deploy everything with latests versions
K3S_VERSION="latest" FALCO_CHART_VERSION="latest" KUBELESS_VERSION="latest" \
  SIDEKICK_UI_VERSION="latest" INSTALL_KUBELESS=1 INSTALL_SIDEKICK=1 \
  ./bootstrap.sh
```

## Configuration

See variable definitions at the beginning of the `scripts/bootstrap.sh` script.

## Prerequisites

* multipass
* kubectl
* helm
* tee
* ts
* cut
* grep

## Authors

Vicente Herrera [[@vicenteherrera](https://github.com/)]  
Thomas Labarussias [[@Issif](https://github.com/Issif)]
