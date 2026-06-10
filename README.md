# Dataset Management with DVC

## Overview

This repository uses **Git** and **DVC (Data Version Control)** to manage datasets and model checkpoints.

* **Git** tracks source code and dataset metadata (`.dvc` files).
* **DVC** stores large datasets and model checkpoints in remote storage.
* **Git Tags** are used to track dataset versions (v1.0, v2.0, v3.0, etc.).

---

# Environment Setup

## Create and Activate Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

## Install DVC

```bash
pip install dvc
```

## Install DVC SSH Support

```bash
pip install "dvc[ssh]"
```

---

# Initialize Repository

## Initialize Git

```bash
git init
```

## Initialize DVC

```bash
dvc init
```

---

# Configure DVC Remote Storage

## Add Remote Storage

```bash
dvc remote add -d remote_storage ssh://user@example.com:2222/path/to/storage
```

## Verify Remote Configuration

```bash
dvc remote list
```

## Remove Remote Storage

```bash
dvc remote remove remote_storage
```

---

# SSH Authentication (Optional)

If SSH key authentication is not configured:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Copy the generated public key to the remote server.

Test SSH connection:

```bash
ssh user@example.com
```

---

# Dataset Management

## Add Dataset

```bash
dvc add Dataset
```

This creates:

```text
Dataset.dvc
```

Track the metadata file using Git:

```bash
git add Dataset.dvc
git commit -m "Add dataset"
```

---

## Push Dataset to Remote Storage

```bash
dvc push
```

This uploads dataset files to the configured DVC remote storage.

---

## Pull Dataset from Remote Storage

```bash
dvc pull
```

Restore dataset files:

```bash
dvc checkout Dataset.dvc
```

---

# Clone Repository on a New Machine

## Clone Repository

```bash
git clone <repository_url>
cd <repository_name>
```

## Install Dependencies

```bash
pip install -r requirements.txt
```

## Fetch All Tags

```bash
git fetch --tags
```

## Pull Dataset

```bash
dvc pull
dvc checkout Dataset.dvc
```

---

# Dataset Version Management

## List Available Dataset Versions

```bash
git tag
```

---

## Checkout Dataset Version

```bash
git checkout tag_version

dvc pull
dvc checkout
```
---

## Checkout Latest Version

```bash
git checkout master

dvc pull
dvc checkout
```

---

# Create a New Dataset Version

After updating the dataset:

```bash
dvc add Dataset

git add Dataset.dvc
git commit -m "Update dataset"

dvc push
```

Create a version tag:

```bash
git tag -a v3.0 -m "Dataset version 3.0"
```

Push changes and tags:

```bash
git push origin master
git push origin --tags
```

---

# Model Checkpoint Versioning

Add model checkpoints:

```bash
dvc add Model_Checkpoint

git add Model_Checkpoint.dvc
git commit -m "Update model checkpoint"

dvc push
git push
```

---

# Freeze Dataset

Prevent accidental updates:

```bash
dvc freeze Dataset.dvc
```

---

# Unfreeze Dataset

Allow dataset updates:

```bash
dvc unfreeze Dataset.dvc
```

---

# Check Dataset Status

View dataset changes:

```bash
dvc status
```

Check remote synchronization status:

```bash
dvc status -c
```

---

# Useful Commands

## Show Current DVC Remotes

```bash
dvc remote list
```

## Show Git Tags

```bash
git tag
```

## Show Current Branch

```bash
git branch
```


