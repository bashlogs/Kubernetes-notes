# Jobs and CronJobs

### Jobs

* **Purpose**: Jobs are used for running one or more pods to completion. They are ideal for tasks that are expected to terminate successfully once their objectives are completed.
* **Use Cases**: Jobs are commonly used for batch processing tasks, one-time operations, or any task that runs to completion. For example, you might use a Job to process a batch of data, perform a database migration, or execute a script once.



{% tabs %}
{% tab title="jobs.yaml" %}
<pre class="language-yaml"><code class="lang-yaml"><strong>apiVersion: batch/v1
</strong>kind: Job
metadata:
  name: sleepy
spec:
  backoffLimit: 5 # number of retry to create jobs
  activeDeadlineSeconds: 100 # after 100s it's a dead job
  ttlSecondsAfterFinished: 60 # delete job after 60 seconds
  completions: 3 # Run our pod atleast 3 times
  parallelism: 2 # 2 pods will be created first time then remaining one
  template:
    spec:
      containers:
      - name: resting
        image: busybox
        command: ["/bin/sleep"]
        args: ["3"]
      restartPolicy: Never
</code></pre>
{% endtab %}
{% endtabs %}

Commands:

```
# To create the job
kubectl create -f job.yaml

# To get jobs
kubectl get job

# To describe jobs
kubectl describe jobs.batch sleepy

# To get the yaml files of job
kubectl get jobs.batch sleepy -o yaml

# To delete the job
kubectl delete jobs.batch sleepy
```

### CronJobs

* **Purpose**: CronJobs are used to schedule and run Jobs at specified times or intervals, similar to the cron utility in Unix-like operating systems. They automate the execution of tasks on a schedule.
* **Use Cases**: CronJobs are useful for recurring tasks that need to be performed at specific intervals, such as backups, log cleanups, database updates, and periodic maintenance tasks. They ensure that these tasks are executed automatically without manual intervention, according to the specified schedule.

{% tabs %}
{% tab title="cronjobs.yaml" %}
```yaml
apiVersion: batch/v1
kind: CronJob   #<-- Change this line
metadata:
  name: sleepy
spec:                        #<-- Remove completions:, parallelism:, and activeDeadlineSeconds:
  schedule: "*/2 * * * *"    #<-- Add Linux style cronjob syntax
  jobTemplate:               #<-- New jobTemplate and spec
    spec:
      template:   #<-- This and following lines space four to right
        spec:
          containers:
          - name: resting
            image: busybox
            command: ["/bin/sleep"]
            args: ["3"]
          restartPolicy: Never
```
{% endtab %}
{% endtabs %}

### CronJobs Timing example

In the cron schedule '10 3 16 12 3', each segment represents a specific time component. Let's break down the meaning of each segment:

<pre data-overflow="wrap"><code><strong>1) 10: Minutes - This specifies the minute at which the job should be scheduled to run. In this case, it's set to 10.
</strong><strong>
</strong>2) 3: Hours - This specifies the hour at which the job should be scheduled to run. In this case, it's set to 3, which represents 3:00 AM.

3) 16: Day of month - This specifies the day of the month at which the job should be scheduled to run. In this case, it's set to the 16th day of the month.

4) 12: Month - This specifies the month at which the job should be scheduled to run. In this case, it's set to December (the 12th month).

5) 3: Day of week - This specifies the day of the week at which the job should be scheduled to run. In the cron syntax, 0 and 7 both represent Sunday, so 1-6 represent Monday to Saturday. Here, it's set to 3, which represents Wednesday.
</code></pre>

So, '10 3 16 12 3' specifies a schedule to run the job at 3:10 AM on the 16th of December, specifically on a Wednesday. This means the specified task (in this case, the Job) will be executed on that specific date and time, which falls on a Wednesday.

Commands:

```
# To create cronjobs
kubectl create -f cronjobs.yaml

# To get cronjobs
kubectl get cronjobs

# To delete cronjobs
kubectl delete cronjobs.batch sleepy
```

Images:

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

#### Assignment

Create a new cronjob which runsbusyboxand thesleep 30command. Have the cronjob run every three minutes.View the job status to check your work. Change the settings so the pod runs 10 minutes from the current time, everyweek. For example, if the current time was 2:14PM, I would configure the job to run at 2:24PM, every Monday.

{% tabs %}
{% tab title="First.yaml" %}
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: job1
spec:
  schedule: "24 14 * * 1"  # Run at 14:24 (2:24PM) every Monday
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: job1
            image: busybox
            args:
            - /bin/sh
            - -c
            - sleep 30
          restartPolicy: OnFailure
```
{% endtab %}

{% tab title="Second.yaml" %}
```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: job1
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name:  job1
            image: busybox
            args:
            - /bin/sh
            - -c
            - date; sleep 30
          restartPolicy: OnFailure
```
{% endtab %}
{% endtabs %}
