### Install Kops VM in Linux
curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
chmod +x kops
sudo mv kops /usr/local/bin/kops

### Install kubectl in Ubuntu
sudo snap install kubectl --classic
kubectl version --client

### Install AWS CLI
sudo snap install aws-cli --classic
aws --version

### Configure IAM and access permissions
aws configure

### Create S3 Bucket, Route53 Hosted Zone and Add NS Records for Godaddy domain 

### Create Cluster

kops create cluster --name=vprofile.vanluong203.online --state=s3://vprofilebucket203 --zones=us-east-1a,us-east-1b --node-count=2 --node-size=t3.small --control-plane-size=t3.medium --dns-zone=vprofile.vanluong203.online --node-volume-size=12 --control-plane-volume-size=12 --ssh-public-key ~/.ssh/id_ed25519.pub

kops update cluster --name=vprofile.vanluong203.online --state=s3://vprofilebucket203 --yes --admin