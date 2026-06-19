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

## Install Requirements

```bash
pip install -r requirement.txt
```
---

# Create folder to Mount

```bash
mkdir remote_dataset
```
---

# Mount Remote Server using NFS

Mount the dataset from the NAS server so that it can be accessed directly without downloading it locally.

## Mount Dataset

```bash
sudo mount -t nfs USER_IP_ADDRESS:/volume1/ai_data_collection/anpr_selection/ANPR_DVC/Dataset /path_to_local_Dataset_folder
```

## Verify Mount

```bash
ls /mnt/anpr_dataset
```

Expected output:

train/
validation/
test/

## Use Mounted Dataset in Training Code

```python
train_data_dir = "/mnt/anpr_dataset/train"
validation_data_dir = "/mnt/anpr_dataset/validation"
```

Training scripts will read data directly from the mounted storage.

## Check Mount Status

```bash
df -h
```

## Unmount Dataset

```bash
sudo umount /mnt/anpr_dataset
```

> **Note:** When using NFS, datasets remain on the remote server and are accessed directly. This avoids storing large datasets on local machines.

---

# Configure DVC Remote Storage cache

## Add Remote Storage

```bash
dvc remote add -d remote_storage_cache ssh://user@example.com:2222/path/to/dvc-cache
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

# Dataset update

```bash
dvc update remote_dataset.dvc
```

# Dataset Management

## Add Dataset

```bash
dvc add mount_folder_name
```

This creates:

Dataset.dvc


Track the metadata file using Git:

```bash
git add Dataset.dvc
git commit -m "Add dataset"
```

---

## Check previous Dataset using 

```bash 
git checkout version -- file_name.dvc # like to view dataset using dataset.dvc or  model_checkpoint.dvc to check model peformance
```

or 

if want to check both things

```bash
git checkout version
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

# Create a New Dataset Version

After updating the dataset:

```bash
git add Dataset.dvc
git commit -m "Update dataset"

dvc push
```

Create a version tag:

```bash
git tag -a v1.0 -m "Dataset version 1.0"
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
git checkout <tag_version>

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

Create a checkpoint tag:

```bash
git tag v3
git push origin v3
```

---

# Check Dataset Status

View dataset changes:

```bash
dvc status
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
