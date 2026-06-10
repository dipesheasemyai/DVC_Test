# Dataset Management with DVC

## Overview

This repository manages datasets using DVC (Data Version Control) and Git.

- DVC stores large dataset files in remote storage.
- Dataset versions are tracked using Git tag


## First create virtual eniverment and activate envirement

```bash
python3 -m venv venv
source venv/bin/activate
```

# Install dvc pip

```bash
pip install dvc
```

# For also need to add dvc ssh pip

```bash 
pip install "dvc[ssh]"
```

# Then activate git

```bash
git init
```

## Then activate dvc

```bash
dvc init
```

## Conncet to remote server SSH

```bash
dvc remote add -d remote_server_name ssh://user@example.com:2222/path
```

## if ssh key authencitation is not available than 

```bash
ssh-keygen -t rsa -b 4096 -C "email.id"
```

## Want to test remote server connection 

```bash 
dvc list-url ssh://user@example.com:2222/path
```

## Import remote sever database 

```bash
dvc import-url ssh://user@example.com:2222/path
```

## If want to remove remote server 

```bash
dvc remote remove remote_sever_name
```

## if want to add Dataset

```bash
dvc add Dataset
```

## if want to push Dataset to remote server

```bash
dvc push
```

## Download Dataset 

Download the dataset corresponding remote server:

```bash
dvc pull
dvc checkout Dataset.dvc
```

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

### Dataset version(v1.0)

```bash 
git checkout version
dvc pull
dvc checkout Dataset.dvc
```

### Latest Version

```bash
git checkout main/master
dvc pull
dvc checkout Dataset.dvc
```

## if want dataset from tag to master/main branch

```bash
git checkout version -- Dataset.dvc
```

---


## Add New Dataset and Model_checkpoint Changes

```bash
dvc add Dataset
dvc add Model_checkpoint
git add Dataset.dvc Model_checkpoint.dvc
git commit -m "Dataset and Model Checkpoint update"
git tag -a "latest version" -m "model latest version, trained Dataset number"
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