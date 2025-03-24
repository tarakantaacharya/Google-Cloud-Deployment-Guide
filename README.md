# Google Cloud Deployment Guide

## Overview
This repository contains a comprehensive guide for deploying applications on Google Cloud Platform (GCP) using the Google Cloud CLI. It includes authentication steps, IAM role configuration, enabling necessary services, Cloud SQL management, App Engine deployment, and Cloud Storage setup.

## Prerequisites
Before using this guide, ensure you have:
- A Google Cloud account
- Google Cloud SDK installed ([Installation Guide](https://cloud.google.com/sdk/docs/install))
- Billing enabled for your GCP project
- A valid project set up on GCP

## Setup Instructions
1. **Authenticate & Set Project**
   ```sh
   gcloud auth login
   gcloud config set project PROJECT_ID
   ```

2. **Enable Required Services**
   ```sh
   gcloud services enable appengine.googleapis.com
   gcloud services enable cloudbuild.googleapis.com
   gcloud services enable sqladmin.googleapis.com
   gcloud services enable storage-component.googleapis.com
   ```

3. **Configure IAM Policies**
   ```sh
   gcloud projects add-iam-policy-binding PROJECT_ID --member="user:YOUR_EMAIL" --role="roles/owner"
   gcloud projects add-iam-policy-binding PROJECT_ID --member="serviceAccount:PROJECT_ID@appspot.gserviceaccount.com" --role="roles/editor"
   ```

4. **Deploy App Engine Application**
   ```sh
   gcloud app create --region=us-central
   gcloud app deploy
   gcloud app browse
   ```

5. **Set Up Cloud SQL**
   ```sh
   gcloud sql instances create my-instance --tier=db-custom-4-16384 --region=us-central1
   gcloud sql instances describe my-instance --format="value(connectionName)"
   ```

6. **Configure Cloud Storage**
   ```sh
   gcloud storage buckets add-iam-policy-binding gs://BUCKET_NAME --member="allUsers" --role="roles/storage.objectViewer"
   ```

## Monitoring & Logs
- **Stream application logs:**
  ```sh
  gcloud app logs tail -s default
  ```

- **View deployed application in browser:**
  ```sh
  gcloud app browse
  ```

## Contributing
Feel free to fork this repository, make improvements, and submit pull requests.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

