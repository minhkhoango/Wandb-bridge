# Wandb Bridge

A Proof-of-Concept for Bridging Weights & Biases Experiments with Production Kubernetes.

---

## The Gap Between Experiment and Production

Engineers track experiments in **Weights & Biases** to ensure reproducibility and collaboration.
But moving a successful run to a production Kubernetes environment like **CoreWeave** creates a gap.

Engineers must manually translate the experiment's configuration into complex and error-prone YAML manifests, slowing down the entire MLOps lifecycle.

## Business Impact: From Hours to Seconds

Automating the experiment-to-production pipeline is a key differentiator for elite engineering teams. **Wandb Bridge** directly drives these outcomes:

* **Reduce Model Deployment Lead Time:** The 2024 DORA State of DevOps Report finds that elite teams achieve lead times of less than a day. By automating YAML generation, this tool collapses what is traditionally a multi-hour manual process into seconds, enabling teams to meet elite performance benchmarks.
* **Increase Deployment Frequency:** The same report indicates elite performers deploy over 200x more frequently than low performers, driven by automation. Wandb Bridge removes the manual bottleneck, allowing teams to deploy model updates multiple times per day.
* **Cut Engineering Overhead:** Case studies on DevOps automation show that eliminating manual manifest authoring reduces per-deployment engineering hours by over 20%. Wandb Bridge provides this efficiency gain out of the box.

---

## The Solution: A Seamless Bridge

**Wandb Bridge** closes this gap.  
It's a simple CLI tool that inspects a completed W&B run and automatically generates the high-quality Kubernetes manifests needed to deploy it.

It turns a manual, multi-hour process into a reliable, one-command action.

### Core Features

- **Automated Manifest Generation**
  Creates production-grade `Job` and `PersistentVolumeClaim` manifests from a single W&B Run ID.

- **Intelligent Hyperparameter Injection**
  Reads the run's configuration and injects all hyperparameters as command-line args into the Kubernetes Job spec.

- **Built for Kubernetes-Native Workflows**
  The output is designed for immediate use with `kubectl`, fitting perfectly into the existing developer workflow at CoreWeave.

### Quickstart

1.  **Prerequisites:**
    * Python **3.9+**
    * `pip`
    * A logged-in W&B account (`wandb login`)
2.  **Installation:**
    ```bash
    git clone https://github.com/minhkhoango/Wandb-bridge.git
    cd Wandb-bridge
    pip install -r requirements.txt
    ```
3.  **Generate Manifests:**
    ```bash
    # Replace with your actual W&B run path
    python codegen.py "entity/project/run_id"
    ```
4.  **Deploy:**
    ```bash
    # A new directory (e.g., "cool-experiment-1_k8s") will be created.
    # Inspect the generated YAML files inside.
    cd cool-experiment-1_k8s

    # Assuming your kubectl is configured for CoreWeave
    kubectl apply -f .
    ```
