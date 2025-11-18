# open-stack
## Install dependencies
```
SSH into the instance:

sudo apt update
sudo apt install -y git vim net-tools linux-modules-extra-$(uname -r)
```
## Enable nested virtualization (should already be active on metal)

Check:

egrep -c '(vmx|svm)' /proc/cpuinfo


Output should be > 0.

##  Clone DevStack
```
git clone https://opendev.org/openstack/devstack
cd devstack

## Create local.conf
nano local.conf

```
Paste:
```
[[local|localrc]]
ADMIN_PASSWORD=admin
DATABASE_PASSWORD=admin
RABBIT_PASSWORD=admin
SERVICE_PASSWORD=admin

HOST_IP=$(curl -s http://169.254.169.254/latest/meta-data/local-ipv4)
LOGFILE=/opt/stack/logs/stack.sh.log

# Enable services
ENABLED_SERVICES+=,swift,s-proxy,s-object,s-container,s-account
ENABLED_SERVICES+=,heat,h-api,h-api-cnf,h-api-cw,h-eng
```
## 6. Start the installation
```
./stack.sh
```

### Installation takes 20–40 minutes.

## 7. Access Horizon Dashboard

Open your browser to:

http://<EC2_PUBLIC_IP>/


## Login:

user: admin

password: admin




Configure inventory → deploy.

This is the recommended method if you want a serious OpenStack environment on EC2.
