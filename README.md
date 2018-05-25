# Getting started with AWS

1. Create an AWS account
2. Go to the EC2 Management console
![Go to EC2](images/aws_home.png)
3. Create a key pair
![Select key pairs](images/select_key_pairs.png)
![Create key pair](images/key_pairs.png)
![Create key pair](images/create_key_pair.png)

Save the key file locally.

Go back to the EC2 Management console.

![Create EC2 instance](images/aws_home_1.png)
Select the Ubuntu AMI
![Select Ubuntu AMI](images/select_ami.png)
Select an instance type
![Select instance type](images/choose_instance_type.png)
Enable public IP address and click add storage
![Add user_data](images/user_data.png)

Under Advanced Details > User data, add:

```sh
#!/usr/bin/env bash

cat > index.html <<EOF
<h1>Hello world, Here I am </h1>
EOF

nohup busybox httpd -f -p 80 &
```

Your instance will run this script as soon as it boots up, serving your `index.html` file on port 80.

Click add tags
![Add storage](images/add_storage.png)
Click configure security groups
![Add tags](images/add_tags.png)
Configure SSH and HTTP
![Configure security groups](images/configure_security_group.png)
Review your settings and click launch
![Review and launch](images/review_and_launch.png)
Add your key to the instance. This is what you will need to connect via SSH
![Add existing key pair and launch](images/use_existing_key_pair_and_launch.png)
Check that your instance is up and running
![Check and view your EC2 instance](images/check_and_view_instances.png)
Get your public IP address and your DNS hostname
![Get your public DNS](images/get_public_dns.png)
Visit your web page
![Go to your web page](images/your_web_page.png)
Log in to your instance via SSH

Change key permissions

```sh
chmod 0600 <private_key_directory>/<your_private_key>.pem
ssh-add <private_key_directory>/<your_private_key>.pem
```

Check your key is added to ssh-agent

```sh
ssh-add -l
```

![SSH into your instance](images/ssh_in.png)
![Yay](images/hacker_yay.png)

## Important caveats
Please note that this set up is for demonstration purposes only.

This setup is not secure.

You should be enforcing HTTPS.

It is also not best practice to allow SSH connections directly into your web server, as we do here.

If you want to know more, search google to learn how to set up private and public subnets and learn about bastion hosts.
