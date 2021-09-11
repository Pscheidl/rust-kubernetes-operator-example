# Rust Kubernetes operator example
[![Rust](https://github.com/Pscheidl/rust-kubernetes-operator-example/actions/workflows/rust.yml/badge.svg)](https://github.com/Pscheidl/rust-kubernetes-operator-example/actions/workflows/rust.yml)

A Kubernetes operator built on top of [kube-rs](https://github.com/clux/kube-rs) project. There is an [explanatory article](https://www.pavel.cool/rust/rust-kubernetes-operators/) available.

Steps to run on Linux:

1. [Install](https://www.rust-lang.org/tools/install) Rust
1. Install Kubernetes, [K3S.io](https://k3s.io/) is an excellent choice, installed simply with `curl -sfL https://get.k3s.io | sh -`. Make sure to `sudo chown $USER /etc/rancher/k3s/k3s.yaml` if you're accessing the Kubernetes cluster using the kubeconfig at `/etc/rancher/k3s/k3s.yaml` as non-root user. Also, `export KUBECONFIG=/etc/rancher/k3s/k3s.yaml`, so the operator can find the kubeconfig.
1. Use `kubectl apply -f echoes.example.com.yaml` to create the CustomResourceDefinition inside Kubernetes.
1. Build the project with `cargo build`. If the build fails, make sure `libssl-dev` is available.
1. Run the operator using `cargo run`. It will run outside of the Kubernetes cluster and connect to the Kubernetes REST API using the account inside the `KUBECONFIG` automatically.

Finally, a custom `Echo` resource can be created with `kubectl apply -f echo-example.yaml`. A new deployment of two pods with `Echo` REST API service will be created. This can be checked with the `kubectl get pods` or `kubectl get deployments` command.

![Usage showcase](showcase.gif)
