# Trilio Metrics  Exporter for Prometheus

Trilio Metrics Exporter written in Golang, to export Triliovault metrics. The project is based on the official prometheus client library: [prometheus_client](https://github.com/prometheus/client_golang).

## Installation

There are two methods to scrape the metrics from Trilio Exporter:

1. **Using Annotations**: Since we have already annotated metrics exporter pod. If you have in-cluster prometheus then it should start scraping metrics. 

The annotations are described below:

```prometheus.io/scrape:``` The default configuration will scrape all pods and, if set to false, this annotation will exclude the pod from the scraping process.

```prometheus.io/path:``` If the metrics path is not /metrics, define it with this annotation.

```prometheus.io/port:``` Scrape the pod on the indicated port instead of the pod’s declared ports, Here it is 8080.

These annotations need to be part of the pod metadata. They will have no effect if set on other objects such as Services or Deployments. 

  
2. **Using Scrape Job**: You will need to configure a prometheus server to scrape the metrics from your
newly running exporter. Add the following scrape job to your `promethus.yml`
configuration file. 

```yaml
  - job_name: trilio_exporter
    scrape_interval: 30s
    file_sd_configs:
    static_configs:
      - targets: ['EXPORTER_ADDRESS:8080']
``` 
NOTE: If you are having Prometheus Operator stack then configure the ServiceMonitor same as above configurations.



## Metrics

Below are metrics included in trilio exporter which are exposed to the prometheus server. Each metric has addtional and related information for each resource in form of tags and has a value. Check given sample for more detail.
1. **trilio_backupplan_info**\
    description: this metric provide detail about BackupPlan CRD\
    tags: backupplan, creation timestamp, namespace, status, target\
    value: creation timestamp in unix format
    

```bash
# HELP trilio_backupplan_info BackupPlan Info
# TYPE trilio_backupplan_info gauge
trilio_backupplan_info{backupplan="postgresql-backupplan",creation_ts="2020-03-24 11:48:48 +0530 IST",namespace="triliovault",status="Available",target="sample-target"} 1.585030728e+09
```

2. **trilio_target_info**\
    description: this metric provide detail about target CRD\
    tags: backupplan, creation timestamp, namespace, status, target, vendor, vendorType\
    value: creation timestamp in unix format

```bash
# HELP trilio_target_info Target Info
# TYPE trilio_target_info gauge
trilio_target_info{backupplan="postgresql-backupplan",creation_ts="2020-03-22 18:03:35 +0530 IST",namespace="triliovault",status="Available",target="sample-target",vendor="Other",vendorType="NFS"} 1.584880415e+09
```

3. **trilio_backup_info**\
    description: this metric provide detail about backup CRD\
    tags: backupplan, backup, namespace, status, target\
    value: creation timestamp in unix format\

```bash
# HELP trilio_backup_info Backup Info
# TYPE trilio_backup_info gauge
trilio_backup_info{backupplan="sample-backupplan-1",backup="sample-backup",namespace="triliovault",status="Available",target="sample-target"} 1.584880561e+09
```

4. **trilio_backup_status_percentage**\
    description: this metric provide detail about backup and its percentage status\
    tags: backupplan, backup, completion timestamp, namespace, start timestamp, status, target\
    value: percentage status

```bash
# HELP trilio_backup_status_percentage Backup Status Percentage
# TYPE trilio_backup_status_percentage gauge
trilio_backup_status_percentage{backupplan="postgresql-backupplan",backup="postgresql-backupplan-63222b65-2d52-47d3-98dc-50053c73ad2e",completion_ts="2020-04-07 11:23:28 +0530 IST",namespace="triliovault",start_ts="2020-04-07 11:23:04 +0530 IST",status="Failed",target="sample-target"} 6
```

5. **trilio_backup_completed_duration**\
    description: this metric provide detail about backups that are in Available state with its duration taken. \
    tags: backupplan, backup, completion timestamp, namespace, start timestamp, status, target\
    value: duration in minutes

```bash
# HELP trilio_backup_completed_duration Backup Completed Duration
# TYPE trilio_backup_completed_duration gauge
trilio_backup_completed_duration{backupplan="sample-backupplan-1",backup="sample-backup",completion_ts="2020-03-22 12:37:53 +0000 UTC",namespace="triliovault",start_ts="2020-03-22 12:36:01 +0000 UTC",status="Available",target="sample-target"} 1
```

6. **trilio_backup_storage**\
    description: this metric provide detail about backup storage. \
    tags: backupplan, backup, completion timestamp, namespace, start timestamp, status, target\
    value: size in bytes
    
```bash
# HELP trilio_backup_storage Backup Storage in bytes
# TYPE trilio_backup_storage gauge
trilio_backup_storage{backupplan="postgresql-backupplan",backup="postgresql-backupplan-63222b65-2d52-47d3-98dc-50053c73ad2e",completion_ts="2020-04-07 11:23:28 +0530 IST",namespace="triliovault",start_ts="2020-04-07 11:23:04 +0530 IST",status="Failed",target="sample-target"} 43223
```

7. **trilio_restore_info**\
    description: this metric provide detail about restore CRD. \
    tags: backup, namespace, restore, status, target\
    value: creation timestamp in unix
    
```bash
# HELP trilio_restore_info Restore Info
# TYPE trilio_restore_info gauge
trilio_restore_info{backup="db-backup",namespace="triliovault",restore="cockroachdb-restore",status="Completed",target="sample-target"} 1.585069927e+09
```
8. **trilio_restore_status_percentage**\
    description: this metric provide detail about backup and its percentage status \
    tags: backup, completion timestamp, namespace, restore, start timestamp, status, target\
    value: status percentage
    
```bash
# HELP trilio_restore_status_percentage Restore Status Percentage
# TYPE trilio_restore_status_percentage gauge
trilio_restore_status_percentage{backup="db-backup",completion_ts="2020-03-24 22:44:50 +0530 IST",namespace="triliovault",restore="cockroachdb-restore",start_ts="2020-03-24 22:42:07 +0530 IST",status="Completed",target="sample-target"} 100
```

9. **trilio_restore_completed_duration**\
    description: this metric provide detail about restore that are in Completed state with its duration taken. \
    tags: backup, completion timestamp, namespace, restore, start timestamp, status, target\
    value: duration in minutes
    
```bash
# HELP trilio_restore_completed_duration Restore Status Percentage
# TYPE trilio_restore_completed_duration gauge
trilio_restore_completed_duration{backup="db-backup",completion_ts="2020-03-24 22:44:50 +0530 IST",namespace="triliovault",restore="cockroachdb-restore",start_ts="2020-03-24 22:42:07 +0530 IST",status="Completed",target="sample-target"} 2
```

10. **trilio_controlplane_available**\
    description: this metric provide detail about control plane deployment with available replicas. \
    tags: deployment, namespace \
    value: available replicas count
    
```bash
# HELP trilio_controlplane_available Trilio Control Plane Ready Replicas
# TYPE trilio_controlplane_available gauge
trilio_controlplane_available{deployment="k8s-triliovault-control-plane",namespace="triliovault"} 1
```


11. **trilio_webhook_available**\
    description: this metric provide detail about webhook deployment with available replicas. \
    tags: deployment, namespace \
    value: available replicas count
    
```bash
# HELP trilio_webhook_available Trilio Webhook Ready Replicas
# TYPE trilio_webhook_available gauge
trilio_webhook_available{deployment="k8s-triliovault-admission-webhook",namespace="triliovault"} 1
```


12. **trilio_executor_available**\
    description: this metric provide detail about executor deployment with available replicas. \
    tags: deployment, namespace \
    value: available replicas count
    
```bash
# HELP trilio_executor_available Trilio Executor Ready Replicas
# TYPE trilio_executor_available gauge
trilio_executor_available{deployment="k8s-triliovault-executor",namespace="triliovault"} 1
```

13. **trilio_exporter_available**\
    description: this metric provide detail about exporter deployment with available replicas. \
    tags: deployment, namespace \
    value: available replicas count
    
```bash
# HELP trilio_exporter_available Trilio Exporter Ready Replicas
# TYPE trilio_exporter_available gauge
trilio_exporter_available{deployment="k8s-triliovault-exporter",namespace="triliovault"} 1
```

<hr>
