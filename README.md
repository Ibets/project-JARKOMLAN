# Project-JARKOMLAN

This is a project that will explain simple configuration about network , starting from Static Routing , OSPF , iBGP and eBGP. (All of these work were created and run in linux virtual machine , WSL and ubuntu related enivronment should be fine)

# Table of Content

- Static Routing
- OSPF
- iBGP
- eBGP

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them

Download Mininet
```
git clone https://github.com/mininet/mininet
cd mininet
git tag  # list available versions
git checkout -b mininet-2.3.0 2.3.0  # or whatever version you wish to install
cd ..
mininet/util/install.sh -a # to install everything 

sudo mn --switch ovsbr --test pingall # to test the instalation of mininet
```

full documentation is in this link https://mininet.org/download/

Download frrouting
```
sudo apt install frrouting
```
This command should be worked and will be downloading 8.1 version and it will work just fine , you can update it to 8.5.6 (newer version) if necessary

### Installing

A step by step series of examples that tell you how to get a development env running

1. clone this repository

```
https://github.com/Ibets/Project-JARKOMLAN/
```

2. Run the script !!
```
sudo python3 static_routing_2rtr.py
sudo python3 ospf-lab.py
sudo pyhton3 ibgp-ibgp.py
```
if you succeeded in running one of these then you should get into mininet CLI.
feel free to explore this project.

## Built With

* Python
* Mininet
