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
mkdir remote_dataset # Create same folder name to given dataset_folder.dvc
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

## Check Mount Status

```bash
df -h
```

## Unmount Dataset

```bash
sudo umount -f /mnt/anpr_dataset
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

---


## Push Dataset to Remote Storage

```bash
dvc push
```

This uploads dataset files to the configured DVC remote storage.

---

Track the metadata file using Git:

```bash
git add Dataset.dvc
git commit -m "Add dataset"
```

---

## Checkout Dataset Version

```bash
git checkout <tag_version> -- dataset.dvc   

dvc checkout dataset.dvc
```

---

## Checkout Model Checkpoint Version

```bash
git checkout <tag_version> -- Model_checkpoint.dvc   

dvc checkout Model_checkpoint.dvc
```

---

# Create a New Dataset Version

After updating the dataset:

```bash
dvc push

git add Dataset.dvc
git commit -m "Update dataset"

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
---

# Dataset Version Management

## List Available Dataset Versions

```bash
git tag
```

---


## Checkout Latest Version

```bash
git checkout master
dvc checkout
```

---

# Create a New Dataset Version

After updating the dataset:

```bash
dvc add Dataset

dvc push

git add Dataset.dvc
git commit -m "Update dataset"

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
dvc push

git add Model_Checkpoint.dvc
git commit -m "Update model checkpoint"

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
