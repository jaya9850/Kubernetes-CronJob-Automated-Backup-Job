# Kubernetes-CronJob-Automated-Backup-Job
This project demonstrates a simple **Kubernetes CronJob** that runs every 2 minutes to perform a backup task using a lightweight `busybox` container. It showcases how to schedule tasks in Kubernetes and use persistent host paths via volumes.



---

## 🚀 How to Run

### 1️⃣ Create the Namespace

```bash
kubectl create namespace nginx
2️⃣ Apply the CronJob
kubectl apply -f cron.yml -n nginx


🔍 Verify the Setup

kubectl get cronjob -n nginx


heck Jobs Created by CronJob
bash
Copy code
kubectl get jobs -n nginx
Check Pod Logs from Job
bash
Copy code
kubectl get pods -n nginx
kubectl logs <pod-name> -n nginx
🧩 Components Breakdown
📄 cron.yml
Section	Description
apiVersion	             Uses batch/v1, the current stable CronJob API.
kind	                   Specifies that this is a CronJob.
metadata.namespace	     Targets the nginx namespace (must be created first).
spec.schedule	            Runs the job every 2 minutes (*/2 * * * *).
jobTemplate	              Describes the actual job that will run at the schedule.
containers	               Uses busybox with a shell command to simulate a backup.
volumeMounts	              Mounts host paths to simulate real file operations.
volumes	                     Uses hostPath volumes pointing to /demo-data and /backup-data on the node.
restartPolicy	                Set to OnFailure to retry failed pods.


📦 Sample Command in the Jobs

sh -c "
  echo 'backup start';
  mkdir -p /backup &&
  mkdir -p /data &&
  cp -r /demo-data/ /backup &&
  echo 'backup complete';


✅ Use Cases
Scheduled backups of app data

Log archiving or rotation

Cron-based cleanup tasks



