# Ansible: Spark standalone cluster on Amazon EC2

## How to use
* Install Ansible
```
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update
sudo apt-get install ansible==1.9.4
```
* Install python boto package
```
sudo apt-get install python-pip
sudo pip install boto
```
* Put your `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` to `~/.boto` file:
```
[profile DSPlatform]
aws_access_key_id = ABCDEFGHIJKLMNOPQRST
aws_secret_access_key = XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```
* Check your access to AWS
```
./inventory/ec2.py --list
```
* Add your keypair to Amazon EC2 (see http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#how-to-generate-your-own-key-and-import-it-to-aws)
* Set your variables in `./group_vars/all/main.yml`
```yml
region: us-west-2
instance_type: m4.large
slave_count: 2
boto_profile: DSPlatform
remote_user: ubuntu

spark_download_url: http://d3kbcqa49mib13.cloudfront.net/spark-1.5.2-bin-hadoop2.6.tgz
spark_version: 1.5.2-bin-hadoop2.6
spark_root: /opt/spark

hadoop_download_url: http://www-us.apache.org/dist/hadoop/common/hadoop-2.6.4/hadoop-2.6.4.tar.gz
hadoop_version: 2.6.4
hadoop_root: /opt/hadoop
```
* Run the playbook
```
ansible-playbook ds_platform.yaml 
```
