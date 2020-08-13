
Welcome at the Helm repository for JorritSalverda.

## Installation

To start using the Helm charts from this repository run the following command

```bash
helm repo add jorritsalverda https://helm.jorritsalverda.com
```

To update and view all available charts in the repository run

```bash
helm repo update jorritsalverda
helm search repo jorritsalverda
```

From here on you can install or upgrade helm charts as follows

```bash
helm upgrade --install evohome-bigquery-exporter jorritsalverda/evohome-bigquery-exporter --namespace evohome-bigquery-exporter --wait
helm upgrade --install evohome-hgi80-listener jorritsalverda/evohome-hgi80-listener --namespace evohome-bigquery-exporter --wait
helm upgrade --install p1-bigquery-exporter jorritsalverda/p1-bigquery-exporter --namespace p1-bigquery-exporter --wait
helm upgrade --install tp-link-hs110-bigquery-exporter jorritsalverda/tp-link-hs110-bigquery-exporter -n tp-link-hs110-bigquery-exporter --wait
```

## Local testing

If you'd like to test these Helm charts on your local machine first, follow the instructions below.

Prepare your Mac to run minikube with the following steps

```bash
brew install minikube
brew install hyperkit
brew install kubernetes-helm
```

Configure some defaults for minikube (optional)

```bash
minikube config set vm-driver hyperkit
minikube config set cpus 2
minikube config set memory 16384
minikube config set disk-size 50gb
```

Start minikube with RBAC enabled and configure Helm

```bash
minikube start --extra-config=apiserver.authorization-mode=RBAC
kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default
kubectl -n kube-system create serviceaccount tiller
kubectl create clusterrolebinding tiller --clusterrole=cluster-admin --serviceaccount=kube-system:tiller
helm init --service-account tiller --wait
```

From here on you can follow the steps as documented in the installation section above.

# Charts

| Chart                                                                                                | Description                                                                           |
| ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| [evohome-bigquery-exporter](https://github.com/JorritSalverda/evohome-bigquery-exporter)             | Reads zone temperatures from the public EvoHome api and stores it in BigQuery         |
| [evohome-hgi80-listener](https://github.com/JorritSalverda/evohome-hgi80-listener)                   | Reads heat demand from an Evohome system from an HGI80 connected via USB              |
| [p1-bigquery-exporter](https://github.com/JorritSalverda/p1-bigquery-exporter)                       | Reads meter readings from Dutch smart meters through a P1 to USB connection           |
| [tp-link-hs110-bigquery-exporter](https://github.com/JorritSalverda/tp-link-hs110-bigquery-exporter) | Reads energy usage metrics from TP-Link HS110 power plugs and stores them in BigQuery |   |


