# Management VPC

```
sudo apt-get install git-core
svn export https://github.com/ddimri/terraform-docker/trunk/certs
cd certs
aws iam delete-server-certificate --server-certificate-name docker-hello-world --profile deepakprasad
aws iam upload-server-certificate --server-certificate-name docker-hello-world --certificate-body file://aws.training.com.cert.pem --certificate-chain file://ca-chain.cert.pem --private-key file://aws.training.com.key --profile deepakprasad
```

# usage
Enable by putting the following in your main.tf
```
module "vpc" {
  source = "git::https://github.com/ddimri/management-vpc.git"
  home_dir = "/Users/deepak.prasad"
  aws_profile = "ddimri-personal"
  project =  "awstraining"
  environment = "training"
  vpc_cidr_block = "10.88.0.0/24"
  private_subnet1_cidr_block = "10.88.0.32/28"
  private_subnet2_cidr_block= "10.88.0.48/28"
  public_subnet1_cidr_block = "10.88.0.1/28"
  public_subnet2_cidr_block = "10.88.0.16/28"
  availability_zones = ["us-west-2a", "us-west-2b"]
  ccjumpbox_ami = "ami-0bb5806b2e825a199"
  awstraining_server_ami = "ami-0bb5806b2e825a199"
  awstraining_openvpn_proxy_ami = "ami-0bb5806b2e825a199"
  instance_type = "t2.micro"
  key_name = "e2-key-file"
  aws_region = "us-west-2"
  vpc_name = "awstraining-mgmt-vpc"
  inboud_ssh = "199.16.196.4/32"
  private_key = "~/.ssh/e2-key-file.pem"
  #ssl_certificate = "arn:aws:iam::398818754185:server-certificate/docker-hello-world"
}
```


