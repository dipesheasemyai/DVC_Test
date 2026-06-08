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
git pull
dvc checkout Dataset.dvc
```

### Dataset v2

```bash 
git checkout v2.0
git pull
dvc checkout Dataset.dvc
```

### Dataset v2

```bash 
git checkout v2.0
git pull
dvc checkout Dataset.dvc
```

### Latest Version

```bash
git checkout main
dvc pull
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

---

## Create New Dataset Version

```bash
git tag v3
git push origin v3
```