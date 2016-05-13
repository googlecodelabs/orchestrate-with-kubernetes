# Enable and Explore Google Cloud Shell

[Google Cloud Shell](https://cloud.google.com/shell/docs) provides you with command-line access to computing resources hosted on Google Cloud Platform and is available now in the Google Cloud Platform Console. Cloud Shell makes it easy for you to manage your Cloud Platform Console projects and resources without having to install the Google Cloud SDK and other tools on your system. With Cloud Shell, the Cloud SDK gcloud command and other utilities you need are always available when you need them.

## Explore Google Cloud Shell

Visit the Google Cloud Shell [getting started guide](https://cloud.google.com/shell/docs/quickstart) and work through the exercises.

## Configure Your Cloud Shell Environment

Create two Cloud Shell Sessions and run the following commands:

To avoid setting the compute zone for each command pick a zone from the list and set your config.

```
gcloud compute zones list
```

```
gcloud config set compute/zone europe-west1-d
```
