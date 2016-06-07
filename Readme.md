Amazon / EC2 Experiment
=======================

Experiment to provision an EC2 instance with Ansible.
Based largely on Ben Cornelius's [example](https://github.com/cornaholic/rails_test_project)
and [troubleshooting](https://vimeo.com/167157877).

Steps:
------

### Set up an EC2 instance

* Get an EC2 instance. Don't really remember how I did this,
  but you can log into the console [here](https://us-west-2.console.aws.amazon.com/ec2/v2/home?region=us-west-2#Instances:sort=instanceId)
  and I added an app.
* Somewhere in the unspecified above step, you'll need to create an SSH key pair,
  do that in `EC2 Dashboard -> Network and Security -> Key Pairs`
  Download your private key and put it here (there's probably other better ways to do this, eg uploading your public key)
* Make sure everything worked by verifying that you can SSH in
  The username will depend on your AMI, I went with the default Amazon Linux, and my user wound up being `ec2-user`.
  The IP is your "Public IP" on your instance, which you can see in
  `EC2 Dashboard -> Instances -> Instances`

  ```
  $ ssh -i ./josh-test.pem  ec2-user@52.26.87.177
  ```

### Configure it with Ansible

* Install ansible (this works on my Mac)

  ```
  $ brew install ansible
  ```
* First make sure you can SSH in, like above, then this should set up the server
  to run [this](https://github.com/JoshCheek/ec2-experiment) code on port 3000.

  ```
  ansible-playbook --key-file ./josh-test.pem playbook.yml -i '52.26.87.177,'
  ```
