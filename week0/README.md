# VSD RISC V Workshop 



## Week 0 Tasks - 

1. ### Install Oracle Virtual Machine to run Linux on a Windows OS. System requirements are as mentioned below -



* 6 GB RAM
* 50 GB HDD
* Ubuntu 20.04 or higher (Check your laptop processor specs before downloading)
* 4 vCPU



### 2\. Resize the Ubuntu window to fit monitor screen. Use commands - 


```bash
$ sudo apt update
$ sudo apt install build-essential dkms linux-headers-$(uname -r)
$ cd /media/spatha/VBox\_GAs\_7.1.8/
$ ./autorun.sh  
```



### 3\. Installing Tools - 



#### Yosys 


```bash
$ sudo apt-get update
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys
$ sudo apt install make               # If make is not installed
$ sudo apt install build-essential clang bison flex \
   libreadline-dev gawk tcl-dev libffi-dev git \
   graphviz xdot pkg-config python3 libboost-system-dev \
   libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make config-gcc // Yosys build depends on a Git submodule called abc, which hasn't been initialized yet. You need to run the following command before running make
$ git submodule update --init --recursive
$ make 
$ sudo make install
```
![Yosys Installed Image](images/Yosys_installed.png)


#### Iverilog 

To install Iverilog use these commands - 

```bash
$ sudo apt update
$ sudo apt install iverilog
```

![Iverilog Installed Image](images/Iverilog_installed.png)

#### GTK Wave 

To install GTK Wave use these commands - 

```bash
$ sudo apt update 
$sudo apt install gtkwave
```

![GTK Wave Installed Image](images/GTKWave_installed.png)

#### OpenSTA
To install OpenSTA use commoand - 

```bash
$ git clone https://github.com/The-OpenROAD-Project/OpenSTA
```
#### ngspice

To install ngspice follow these steps - 

1. Download the tarball from https://sourceforge.net/projects/ngspice/files/ to your working directory \
2. Unpack it using these commands - 

```bash 
$ tar -zxvf ngspice-37.tar.gz
$ cd ngspice-37
$ mkdir release
$ cd release
$ ../configure --with-x --with-readline=yes --disable-debug
$ make
$ sudo make install 
``` 
![ngspice Installed Image](images/ngspice%20successfull%20installation.png)

#### Magic 

To install magic use these commands - 

```bash
$ sudo apt-get install m4
$ sudo apt-get install tcsh
$ sudo apt-get install csh
$ sudo apt-get install libx11-dev
$ sudo apt-get install tcl-dev tk-dev
$ sudo apt-get install libcairo2-dev
$ sudo apt-get install mesa-common-dev libglu1-mesa-dev
$ sudo apt-get install libncurses-dev
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
make
make install 
```
![Magic Installed Image](images/magic%20successfull%20installation.png)

#### OpenLane 

To install OpenLane use these commands - 

```bash 
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt install -y build-essential python3 python3-venv python3-pip make git 
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common 
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o
/usr/share/keyrings/docker-archive-keyring.gpg 
$ echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg]
https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee
/etc/apt/sources.list.d/docker.list > /dev/null 
$ sudo apt update 
$ sudo apt install docker-ce docker-ce-cli containerd.io
$ sudo docker run hello-world
$ sudo groupadd docker 
$ sudo usermod -aG docker $USER 
$ sudo reboot // Your system will restart, do not panic
$ docker run hello-world //After restarting, go to the same folder and enter this command
```
![Docker Installed and Running Image](images/Docker%20Download%20Success.png)

#### Check your dependencies 

```bash 
$ git --version
$ docker --version
$ python3 --version
$ python3 -m pip --version
$ make --version
$ python3 -m venv -h
```

![Dependency Versions Image](images/Dependency%20Versions.png)

#### SkyWater 130 PDK 

Use these commands to install the PDK -

```bash 
$ cd $HOME
$ git clone https://github.com/The-OpenROAD-Project/OpenLane 
$ cd OpenLane 
$ make // While doing this command, make sure ciel is upto date and enable the PDK version that OpenLane is asking for. Make sure to create a virtual environment prior to this step.
$ make test 
```
 













