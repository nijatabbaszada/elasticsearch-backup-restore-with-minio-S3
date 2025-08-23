# Elasticsearch Backup & Restore with MinIO S3 Step by Step

This repository provides step-by-step documentation and examples on how to backup and restore Elasticsearch data using **MinIO** as an S3-compatible storage.

## 📌 Contents
1. Introduction  
2. Configure Elasticsearch
3. Configure MinIO  
4. Register Snapshot Repository in Elasticsearch  
5. Create Backup (Snapshot)  
6. Verify Snapshots  
7. Restore from Snapshot  
8. Common Issues & Troubleshooting  

## 🚀 Quick Start

## 2. Configure Elasticsearch

### 🔌 Install S3 Plugin and Configure Keystore on Elasticsearch

In order to enable snapshot and restore functionality with MinIO (S3-compatible storage), you must install the `repository-s3` plugin and configure Elasticsearch keystore with the appropriate credentials.

### 1. Install the repository-s3 Plugin

```bash
/usr/share/elasticsearch/bin/elasticsearch-plugin install repository-s3 --batch
```
>⚠️ After installation, you must restart Elasticsearch for the changes to take effect.

```bash
systemctl restart elasticsearch
```

Verify Installed Plugins

```bash
curl -X GET "http://<elasticsearch-ip>:9200/_cat/plugins?v"
```

Or check directly on the server:

```bash
/usr/share/elasticsearch/bin/elasticsearch-plugin list
ls /usr/share/elasticsearch/modules/
```

### 2. Configure Elasticsearch Keystore

Check available keystore entries:

```bash
/usr/share/elasticsearch/bin/elasticsearch-keystore list
```

Add MinIO credentials (Access Key and Secret Key) to the keystore:
```bash
/usr/share/elasticsearch/bin/elasticsearch-keystore add s3.client.default.access_key
/usr/share/elasticsearch/bin/elasticsearch-keystore add s3.client.default.secret_key
```

When prompted, enter your MinIO Access Key and Secret Key.

Verify Keystore Configuration

```bash
/usr/share/elasticsearch/bin/elasticsearch-keystore list
```

You should now see the newly added S3 client entries.
