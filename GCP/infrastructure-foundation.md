# Instrastructure: Foundation

You can interact with GCP in 4 ways: the console, cloud shell/SDK, the mobile app, and a REST API 

## Cloud Shell Intro

Cloud Shell is an interactive terminal window that gives you:

- built-in authorization for access to resources and instances
- 5 GB of persistent storage
- Command-line access to a free temporary Compute Engine VM

You can create buckets for storing data and files, then upload files from your computer or elsewhere using the shell. Finally, you can copy files from there into the bucket of your choice

```sh
# make a bucket
gsutil mb gs://my_bucket_1

# copy file to that bucket
gsutil cp some_filt gs://my_bucket_1

# Best practice is to use environment variables
# configure the `.profile` file to update shell (it's like bashrc)
MY_BUCKET=gs://my_bucket_1
```
