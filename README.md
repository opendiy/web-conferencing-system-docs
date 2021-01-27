<!-- TABLE OF CONTENTS -->
<details open="open">
<h3 align="center">Web Conferencing System</h3>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#bigbluebutton">What is BigBlueButton</a>
      <ul>
        <li><a href="#overview">Overview</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#greenlight">Greenlight</a>
    <ul>
        <li><a href="#overview-of-greenlight"> Overview of GreenLight</a></li>
        <li><a href="#configure-greenlight">Configure Greenlight</a></li>
      </ul>
      </li>
    <li><a href="#troubleshooting">Troubleshooting</a></li>
  </ol>
</details>

<!-- bigbluebutton -->
## BigBlueButton

BigBlueButton is an open source web conferencing system for online learning.

Open source - Full access to BigBlueButton’s source code under an open source license. With the source code it is easily possible to deploy your own BigBlueButton server. It is designed with all facilities for online web conferencing or online learning platforms. 

<!-- overview -->
## overview

BigBlueButton is an HTML5-based web application. BigBlueButton runs in a web browser. There is no plugin to download, no software to install. BigBlueButton provides high-quality audio, video, and screen sharing using the browser’s built-in support for web real-time communication (WebRTC) libraries.

WebRTC is a standard supported by all major browsers, including Chrome, FireFox, Safari, and Safari Mobile. For best results on desktop and laptops, BBB recommends Chrome or Firefox.

<!-- getting_started -->
## Getting Started


### Before Installation :


Minimum Hardware & Software requirements :

=> Ubuntu 18.04 64 bit 
=> 8/16 GB Memory
=> 4/8 CPU Cores
=> 50/500 GB free disk space without recording or with recording facility
=> TCP ports 80 & 443  are accessible
=> UDP ports 16384 - 32768 are accessible
=> TCP port 80 and 443 are not in use by another web application or reverse proxy
=> A Hostname for setup of a SSL certificate

| Requirements | Minimum | Recommended|
<!--
| ----------- | --------------- | --------------- | --------------- |--------------- | -->
|  | 64 bit | 8 GB | 4 | 50 GB|


| CPU | x64 Capable Ubuntu 16.04 or 18.04 | Row 2 Column 3 |
| OS Version | Row 3 Column 2 | Row 3 Column 3 |
| RAM | Row 3 Column 2 | Row 3 Column 3 |
| CPU | Row 3 Column 2 | Row 3 Column 3 |
| DISK SPACE | Row 3 Column 2 | Row 3 Column 3 |
| PORTS | Row 3 Column 2 | Row 3 Column 3 |
| DOMAIN | Row 3 Column 2 | Row 3 Column 3 |

| SSL | Row 3 Column 2 | Row 3 Column 3 |



<!-- installation -->
## Installation :

BigBlueButton only supports Ubuntu 16.04 64 bit server and Ubuntu 18.04 Server. We will install BigBlueButton in Ubuntu 18.04.  After Installation , We have to make ready our Server for BigBlueButton. 

Remember :

When Installing BigBlueButton there are two choices: One Scripted (bbb-install.sh) and another step by step process installation. It is also mendetory to install BBB, 
Installation should be done as the "ROOT" User.

Here, I will just mention the steps ,but if you want to know more please check the official documents 

[BigBlueButton Documents](https://docs.bigbluebutton.org/)

Steps :

Check the local of the server is  en_us.UTF-8 

```bash
$ cat /etc/default/locale
```

LANG="en_US.UTF-8"
If you don’t see LANG="en_US.UTF-8", enter the following commands to set the local to en_US.UTF-8.

```bash
$ sudo apt-get install -y language-pack-en
```

```bash
$ sudo update-locale LANG=en_US.UTF-8
```

Check the Server has Ubuntu is 18.04  and codename Bionic 

```bash
$ cat /etc/lsb-release
```

Check that your server is running the 64-bit version of ubuntu

```bash
$ uname -m
```

x86_64
Check your server is running Linux Kernel 4.x.

```bash
$ uname -r
```
4.15.0-38-generic
Check your server has installed Java

java -version (Remember to install JAVA version 8)
Otherwise Install the the Java

```bash
$ apt install openjdk-8-jre-headless
```

```bash
$ sudo apt-get update
```
 (Update the package)

### Add the bigbluebutton's repository

Add the 'multiverse repository' because BBB works with multiverse repository so you should check if it's present in your repository.

```bash
$ sudo echo "deb http://archive.ubuntu.com/ubuntu/ bionic multiverse" | sudo tee -a /etc/apt/sources.list
```

Next, You'll need to add the BBB key to your server so that you can install BigBlueButton. You can do that by following command.

```bash
$ sudo wget https://ubuntu.bigbluebutton.org/repo/bigbluebutton.asc -O- | sudo apt-key add -
```

Then, Once you added the public key, you will have to specify the URL of the BigBlueButton package to download.

Configure the package repository with the following command .

```bash
$ sudo echo "deb https://ubuntu.bigbluebutton.org/xenial-22/ bigbluebutton-xenial main" | sudo tee /etc/apt/sources.list.d/bigbluebutton.list
```

```bash
$ echo "deb https://ubuntu.bigbluebutton.org/bionic-230/ bigbluebutton-bionic main" | sudo tee /etc/apt/sources.list.d/bigbluebutton.list
```


### Next update the repository

```bash
$ sudo apt-get update
```

### Install BigBlueButton script by following command.

```bash
$ wget -qO- https://ubuntu.bigbluebutton.org/bbb-install.sh | bash -s -- -v bionic-230-dev -s 'Your FQDN Name' -e 'Your Email Address'  -a -w
```

### After the Installation finishes, You can restart the BigBlueButton

```bash
$ sudo bbb-conf --restart
```

### After the restart finishes , check the setup by following command.

```bash
$ sudo bbb-conf --check
```

### Now check the greenlight and docker is installed in your home directory otherwise follow the following process.

```bash
$ docker -v (check Docker is installed by running)
```

<!-- greenlight -->

## Greenlight

<!-- overview-of-greenlight -->
### Overview of GreenLight

Greenlight is a simple front-end interface for BigBlueButton server. At its heart, Greenlight provides a minimalistic web-based application that allows users to:

Signup/Login with Google, Office365, OpenID Connect, or through the application itself.

Manage your account settings and user preferences.

Create and manage your own personal rooms (BigBlueButton sessions).

Invite others to your room using a simple URL.

View recordings and share them with others.

<!-- configuration -->
### Greenlight Configuration


```bash
$sudo mkdir greenlight
$sudo cd greenlight
```

### Greenlight will read its environment configuration from the .env file. To generate this file and install the Greenlight Docker image, run:

```bash
$sudo docker run --rm bigbluebutton/greenlight:v2 cat ./sample.env > .env
```

### Configure Greenlight

If you open the .env file you’ll see that it contains information for all of the Greenlight configuration options. Some of these are mandatory.

After Installation, .env file you will see generated at ~/greenlight/.env.

### Generating a Secret Key

Greenlight needs a secret key in order to run in production. To generate this, run:

```bash
$ sudo docker run --rm bigbluebutton/greenlight:v2 bundle exec rake secret
```

Inside your .env file, set the SECRET_KEY_BASE option to this key. You don’t need to surround it in quotations.

### Setting BigBlueButton Credentials

By default, your Greenlight instance will automatically connect to test-install.blindsidenetworks.com if no BigBlueButton credentials are specified. To set Greenlight to connect to your BigBlueButton server (the one it’s installed on), you need to give Greenlight the endpoint and the secret. To get the credentials, run:

```bash
$ sudo bbb-conf --secret
```

In your .env file, set the BIGBLUEBUTTON_ENDPOINT to the URL, and set BIGBLUEBUTTON_SECRET to the secret.

### Setting Allowed Hosts

For reasons related to security, you’ll also need to specify the domain from which the application will be accessible from.

In your .env file, set the SAFE_HOSTS to your domain. If Greenlight is accessible at https://meetup.bounceme.net/b then SAFE_HOSTS=https://meetup.bounceme.net/

### Verifying Configuration

Once you have finished setting the environment variables above in your .env file, to verify that you configuration is valid, run:

```bash
$ sudo docker run --rm --env-file .env bigbluebutton/greenlight:v2 bundle exec rake conf:check
```

If you have configured an SMTP server in your .env file, then all four tests must pass before you proceed. If you have not configured an SMTP server, then only the first three tests must pass before you proceed.

### Configure Nginx to Route To Greenlight

Greenlight will be configured to deploy at the /b subdirectory. This is necessary so it doesn’t conflict with the other BigBlueButton components. The Nginx configuration for this subdirectory is stored in the Greenlight image. To add this configuration file to your BigBlueButton server, run:

```bash
$ sudo docker run --rm bigbluebutton/greenlight:v2 cat ./greenlight.nginx | sudo tee /etc/bigbluebutton/nginx/greenlight.nginx
```


### Verify the Nginx configuration file picks up the new configuration 

```bash
$ sudo systemctl restart nginx
```

###  Start Greenlight 

To start the Greenlight Docker container, you must install docker-compose, which simplifies the start and stop process for Docker containers.

Before you continue, verify that you have docker-compose installed by running:

```bash
$ cd greenlight> docker-compose -v 
```

Otherwise install the Docker-Compose

```bash
$ apt install docker-compose
```

Next, you should copy the docker-compose.yml file from the Greenlight image in to ~/greenlight directory. To do this, run:

```bash
$ docker run --rm bigbluebutton/greenlight:v2 cat ./docker-compose.yml > docker-compose.yml
```

Finally, randomly generate a password for the PostgreSQL database and replace the entries in the .env and .docker-compose.yml file with this command


```bash
$ export pass=$(openssl rand -hex 8); sed -i 's/POSTGRES_PASSWORD=password/POSTGRES_PASSWORD='$pass'/g' docker-compose.yml;sed -i 's/DB_PASSWORD=passwor
d/DB_PASSWORD='$pass'/g' .env 
```

Once you have completed these steps, from the ~/greenlight directory, start the application using:

 ```bash
$ docker-compose up -d
```



This will start Greenlight, and you should be able to access it at https://<hostname>/b.

### Create the user by following command

```bash
$ docker exec greenlight-v2 bundle exec rake user:create["User-Name","E-Mail Address","Password","User-Name"]
```

### Log File 

All of the logs from the application are also saved to the BigBlueButton server, which can be found at ~/greenlight/log


<!-- Troubleshooting -->

## Troubleshooting 

If you encounter an error  after follow all the instaraction please check the BigBlueButton Documentation.






```bash
$ docker exec greenlight-v2 bundle exec rake user:create["User-Name","E-Mail Address","Password","User-Name"]
```


