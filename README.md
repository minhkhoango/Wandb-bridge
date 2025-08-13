# W&B Bridge

A Proof-of-Concept for Bridging Weights & Biases Experiments with Production Kubernetes.

---

## The Gap Between Experiment and Production

Engineers track experiments in **Weights & Biases** to ensure reproducibility and collaboration.  
But moving a successful run to a production Kubernetes environment like **CoreWeave** creates a gap.  

Engineers must manually translate the experiment's configuration into complex and error-prone YAML manifests, slowing down the entire MLOps lifecycle.

---

## The Solution: A Seamless Bridge

**W&B Bridge** closes this gap.  
It's a simple CLI tool that inspects a completed W&B run and automatically generates the high-quality Kubernetes manifests needed to deploy it.

It turns a manual, multi-hour process into a reliable, one-command action.

---

## Core Features

- **Automated Manifest Generation**  
  Creates production-grade `Job` and `PersistentVolumeClaim` manifests from a single W&B Run ID.

- **Intelligent Hyperparameter Injection**  
  Reads the run's configuration and injects all hyperparameters as command-line args into the Kubernetes Job spec.

- **Built for Kubernetes-Native Workflows**  
  The output is designed for immediate use with `kubectl`, fitting perfectly into the existing developer workflow at CoreWeave.

## How to Use

### Prerequisites
- Python **3.9+**
- `pip`
- A logged-in W&B account (`wandb login`)

### Installation
```bash
git clone https://github.com/YOUR_USERNAME/wandb-k8s-codegen.git
cd wandb-k8s-codegen
pip install -r requirements.txt
```

### Generate Manifests
```bash
# Replace with your actual W&B run path
python codegen.py "entity/project/run_id"
```

### Deploy
```bash
# A new directory (e.g., "cool-experiment-1_k8s") will be created.
# Inspect the generated YAML files inside.
cd cool-experiment-1_k8s

# Assuming your kubectl is configured for CoreWeave
kubectl apply -f .
```