# How to Setup Lavanga on Ubuntu using AWS Lightsail

Requirements
* AWS account
* Lightsails
* Basic Linux Experience

# Quick Start Guide

## Prepare your AWS Lightsail
1. [Create a new lightsail Instance](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/how-to-create-amazon-lightsail-instance-virtual-private-server-vps)
2. [Select Instance type](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/compare-options-choose-lightsail-instance-image)
- Select OS Only + Ubuntu 20.04 instance type 
- Doesnt have to be the highest or most expensive. Cheap is best
3. Launch Instance and wait

### Login to your ubuntu server and apply security updates
1. [Click the quick console button](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/lightsail-how-to-connect-to-your-instance-virtual-private-server)
2. Run the following commands to update your server
> sudo apt-get update
>
>sudo apt-get upgrade

### Install Dependancy
1. Install wget
> sudo apt install wget
2. Install unzip
> sudo apt install unzip
3. Mysql Client
> sudo apt install mysql-client-core-8.0 

## Setup Java
> sudo apt install default-jre
>
> sudo apt install default-jdk
> 
> java -version

## Setup Jetty Server - Dependancy
> sudo apt install jetty9

## Download Lavagna
1. Goto https://lavagna.io/
2. [Click Downloads](https://lavagna.io/download/)

## Prepare Lavagna
1. Extract file (replace file name with current file name version)
> unzip lavagna-1.1.9-distribution.zip
2. Navigate to your directory for Lavagna (replace with current directory version)
> cd lavagna-1.1.9/
3. Does your Lavagna work or not? Yes or No
> /home/{username}/lavagna{current directory version}/bin/lavagna.sh

## Test your lavagna works
1. Your server should be accessable via the server [ip address listed in lightsail instance](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/understanding-public-ip-and-private-ip-addresses-in-amazon-lightsail)
2. Open your web browser
3. Copy the ip address of the instance from choosen lightsail
4. Enter the web address
> eg; http://{YOUR LIGHTSAIL INSTANCE IP ADDDRESS}:8080/login
5. Ignore the Lavagna setup step or address [found in the setup help guide](https://help.lavagna.io/02-install/02-02-configuration.html)

Do you see great success or not? If no RTFM and look at [Github Lavanga Issue Page - Show all issues](https://github.com/digitalfondue/lavagna/issues?q=)

6. Close the Lavagna server by pressing  control + z

## Configurate Lavanga
1. Open Configuration file
> nano lavagna-{VERSION}/bin/lavagna.sh
2. Copy to notepad and make the following changes to match your server infomation
> BASEDIR=$(dirname $0)
>
> java \
>        -Ddatasource.dialect="MYSQL" \
>        -Ddatasource.url="jdbc:mysql://localhost:3306/lavagna?useUnicode=true&characterEncoding=utf-8" \
>        -Ddatasource.username="someuser" \
>        -Ddatasource.password= "somepassword" \
>        -Dspring.profiles.active="prod" \
>        -jar $BASEDIR/../lavagna/lavagna-jetty-console.war
