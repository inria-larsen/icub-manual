# porting icub inside drake

For more info check the slack channel. 

# Brice install :

I installed in my docker.

# pybind11 :
```
git clone https://github.com/pybind/pybind11.git /home/icubuser/pybind11
```

# install gfortran compiler :
```
sudo apt-get update
sudo apt-get install -y gfortran-7

echo "export FC=gfortran-7" >> /home/icubuser/.bashrc;
echo "export F77=\$FC" >> /home/icubuser/.bashrc;
```

# install eigen :
```
sudo apt-get install -y zip unzip
wget "http://bitbucket.org/eigen/eigen/get/3.3.3.zip" -P /home/icubuser
unzip /home/icubuser/3.3.3.zip
rm /home/icubuser/3.3.3.zip
mv eigen-eigen-* /home/icubuser/eigen-3.3.3

cd /home/icubuser/eigen-3.3.3; \
	mkdir build; \
	cd build; \
	cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr/local ..; \
	make -j8; \
	make install;"
```

# install java :
```
apt-get install -y default-jre default-jdk
```

# install pip :
```
sudo apt-get update
sudo apt-get install -y python-pip
pip install --upgrade pip
sudo apt-get install -y python3-setuptools python-numpy
```

# install qt4 :
```
sudo apt-get install -y qt4-dev-tools qt4-default python-qt4
```

# install glib2 :
```
sudo apt-get install -y libglib2.0-0 libglib2.0-dev
```

# install vtk :
```
sudo apt-get install -y libvtk5-qt4-dev libvtk-java libvtk5-dev python-vtk
sudo apt-get update
```

# install ipopt :
```
sudo apt-get install -y coinor-libipopt-dev
sudo apt-get update
```

# Install Drake from sources :
```
git clone https://github.com/RobotLocomotion/drake.git ~/.
```

# With Bazel :

Install [Bazel](https://bazel.build/) :
```
sudo apt-get install openjdk-8-jdk
sudo apt-get update && sudo apt-get install bazel
sudo apt-get upgrade bazel
```

Setup your installation, for ubuntu 16.04 :
```
./~/drake/setup/ubuntu/16.04/install_prereqs.sh
```

## Build only :
```
bazel build //:install
```

Maybe you'll need --compiler=gcc-5 if clang can't find basic headers. Or set clang properly. Here i used gcc-5, check your gcc.

## Install :
```
bazel run //:install -- /opt
(or for me it was : bazel run --compiler=gcc-5 //:install -- /opt )
```
