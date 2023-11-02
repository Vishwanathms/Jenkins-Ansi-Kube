# Lab Details for Setting up Jenkins, Docker , Ansible and Kubernetes.

## Install Jenkins, Ansible, and Docker

### Log in to the Jenkins instance

1. Install Python 3, Ansible,  ÷module:
```
sudo apt update && sudo apt install -y python3 && sudo apt install -y python3-pip && sudo pip3 install ansible 
```
2. By default, pip installs binaries under a hidden directory in the user’s home folder. We need to add this directory to the $PATH variable so that we can easily call the command:

```
echo "export PATH=$PATH:~/.local/bin" >> ~/.bashrc && . ~/.bashrc
```

3. The jenkins-file is easier than it looks. Basically, the pipeline contains four stages:

* Build is where we build the Go binary and ensure that nothing is wrong in the build process.
* Test is where we apply a simple UAT test to ensure that the application works as expected.
* Publish, where the Docker image is built and pushed to the registry. After that, any environment can make use of it.
* Deploy, this is the final step where Ansible is invoked to contact Kubernetes and apply the definition files.


## Testing Our CD Pipeline
The last part of this LAB is where we actually put our work to the test. We are going to commit our code to GitHub and ensure that our code moves through the pipeline until it reaches the cluster:

* Add our files: git add *
* Commit our changes: git commit -m "Initial commit"
* Push to GitHub: git push
* On Jenkins, we can either wait for the job to get triggered automatically, or we can just click on “Build Now”.
* If the job succeeds, we can examine our deployed application using the following commands:

### Now, let’s initiate an HTTP request to the app:
