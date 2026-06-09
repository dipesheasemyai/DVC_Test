# Dataset Management with DVC

## Overview

This repository manages datasets using DVC (Data Version Control) and Git.

- DVC stores large dataset files in remote storage.
- Dataset versions are tracked using Git tag


## Prerequisites

## Clone Repository

```bash
git clone  <repository_url>
```

Install requirements:

```bash
pip install -r requirements.txt
```

Fetch all tags:

```bash
git fetch --tags
```

## Configure DVC Remote

Check Configure remotes:

```bash
dvc remote list
```

## Download Dataset 

Download the dataset corresponding to current git version:

```bash
dvc pull
```

List available tags:

```bash
git tag
```

## Switch Dataset Version

### Dataset v1

```bash 
git checkout v1.0
dvc pull
dvc checkout Dataset.dvc
```

### Dataset v2

```bash 
git checkout v2.0
dvc pull
dvc checkout Dataset.dvc
```

### Latest Version

```bash
git checkout main
dvc pull
dvc checkout Dataset.dvc
```
---


## Add New Dataset Changes

```bash
dvc add Dataset 
git add Dataset.dvc
git commit -m "Dataset update"
dvc push
git push
```

## Add Model_checkpoint Changes

```bash
dvc add Model_checkpoint
git add Model_checkpoint.dvc
git commit -m "Model Checkpoint update"
dvc push
git push
```
## Dataset is Froze 

```bash 
dvc unfreeze <Dataset_folder>.dvc
```

## Forze Dataset 

```bash
dvc freeze <Dataset_folder>.dvc
```

## Status of Current Changes

```bash
dvc status
```

---

## Create New Dataset Version

```bash
git tag v3
git push origin v3
```