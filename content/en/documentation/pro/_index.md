---
title: "JobRunr Pro"
subtitle: "Add some steroids to JobRunr to support your difficult business processes."
date: 2020-04-30T11:12:23+02:00
layout: "documentation"
menu: 
  main: 
    identifier: jobrunr-pro
    parent: 'documentation'
    weight: 50
---
JobRunr Pro is a drop-in replacement for JobRunr, available under a [paid subscription]({{< ref "/pricing.md" >}}) and adds a lot of extra functionality to support your difficult business processes:
- __[Job Filtering]({{< ref "job-filtering.md" >}}):__ are you processing a lot of jobs and do you quickly need to find that one job? Thanks to the Job Filter feature in the JobRunr Pro dashboard you will quickly find any job by name, method signature or any other filters.
- __[Queues]({{< ref "queues.md" >}}):__ or are you processing a lot of jobs and do you have critical business processes that must finish on-time? Queues to the rescue! Just schedule your job with a higher priority and it will bypass all the other jobs.
- __[Job Chaining]({{< ref "job-chaining.md" >}}):__ reuse existing service methods and chain jobs to have cleaner code and an immediate overview of your business process.
- __[Batches]({{< ref "batches.md" >}}):__ batches allow you to create a bunch of background jobs atomically and combined with [Job Chaining]({{< ref "job-chaining.md" >}}) they can make complex workflows easy!
- __[Server Tags]({{< ref "server-tags.md" >}}):__ do you have jobs that can only run on certain servers (e.g. Jobs that should only run on Windows, Linux, ...)? Server Tags let you filter jobs by certain tags so that they are only run on certain servers.
- __[Mutexes]({{< ref "mutexes.md" >}}):__ do you consume a resource in your jobs that can not be shared? Thanks to mutexes, JobRunr will postpone jobs with shared mutexes until the mutex is free.
- __[Job Migrations]({{< ref "migrations.md" >}}):__ easily migrate existing scheduled jobs via job migrations - CI/CD for your background jobs is now easier than ever. Or, you can just make your old job methods package private and JobRunr Pro will still execute them.
- __[Custom delete policy]({{< ref "custom-delete-policy.md" >}}):__ You probably like clean code? Then you also like a clean dashboard. Using a custom delete policy, you can delete jobs faster and keep dashboard and database clean.
- __Pause recurring jobs:__ Do you want to pause your recurring jobs? Just pause them from the dashboard and resume them whenever you are ready.
- __Database fault-tolerance:__ is your SQL / NoSQL database sometimes going down? Are you having connection troubles from your application to your database? JobRunr Pro has you covered and it will automatically stop job processing temporarily in this case. The moment your database is back online, JobRunr will start processing jobs again as if nothing ever happened.

### Upcoming features
JobRunr Pro is by no means a finished product - subscribing will allow me to build extra features including:
- Notification support if suddenly many jobs start failing
- a Slack and Microsoft Teams plugin which allows you to follow up on jobs and be notified if batches are finished (so business does not have to disturb you to find out how long a job will take)
- feature requests from you!