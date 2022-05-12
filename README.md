### Aim:
Introduction to discrete event simulation tools NS2, NS3 & installation of NS3.

### Introduction:
Network simulator is a tool used for simulating the real world network on one computer by writing scripts in C++ or Python. Normally if we want to perform experiments, to see how our network works using various parameters. We don’t have required number of computers and routers for making different topologies. Even if we have these resources it is very expensive to build such a network for experiment purposes.

So to overcome these drawbacks we used NS3, which is a discrete event network simulator for Internet.

### NS2:
NS2 stands for Network Simulator Version 2. It is an open-source event-driven simulator designed specifically for research in computer communication networks.

Network Simulator 2 (NS2) provides substantial support for simulation of different protocols over wired and wireless networks. It provides a highly modular platform for wired and wireless simulations supporting different network elements, protocols, traffic, and routing types.

### NS3: 

ns-3 is a discrete-event network simulator, targeted primarily for research and educational use. ns-3 is free software, licensed under the GNU GPLv2 license, and is publicly available for research, development, and use.

The ns-3 project is committed to building a solid simulation core that is well documented, easy to use and debug, and that caters to the needs of the entire simulation workflow, from simulation configuration to trace collection and analysis.

Furthermore, the ns-3 software infrastructure encourages the development of simulation models that are sufficiently realistic to allow ns-3 to be used as a realtime network emulator, interconnected with the real world, and that allows many existing real-world protocol implementations to be reused within ns-3.

### Difference between NS3 & NS2: 
| NS3 | NS2 |
| ----------- | ----------- |
| NS3 can be act as the emulator that it can connect to the real world | NS2 can not be act as the emulator. |
| Some of the NS2 models can be imported to NS3 | NS3 scripts can not run in NS2 environment |
| NS3 is written using C++ | NS2 is written with the help of TCL and C++. |
| Compilation time is not a matter | C++ recompilation takes more time more than TCL so most of the scripts are written using TCL |
| Information needed to send through the packet can be added at the header ,trailer, buffer ,etc | The header part of the NS2 includes all the information of header parts in the specified protocol |
| NS3 frees the memory that used to store the packets, The packet of ns3 consist of single buffer and small tags. | NS2 never reuse or re allocate the memory until it get terminated, The packet of ns2 has headers and data for payload. |
| Network Animator visualization is available | Nam animator is available for visualization.|

### Installation of NS3:

Download the [NS3](https://www.nsnam.org/releases/ns-3-30/download/) tar file.

Go to download folder
```
cd Download/
```

To check that the tar file is downloaded properly run 
```
ls
```
You'll see a `ns-allinone-3.<version>.tar.bz2`.


To extract the tar file run: 
```
tar -xvf ./ns-allinone-3.30.1.tar.bz2
```

To enter the ns-3 folder run
```
cd ns-allinone-3.30.1
```

Once you're in the `ns-allinone-3.30.1` directory, run:
```
./build.py --enable-examples --enable-tests
```

To install all dependency (in ubuntu) run:
```
apt install gcc python python-dev qty-dev-tools libgtk-3-dev python-pygoocanvas python-pygraphvizwiresharkgnuplot openjdk-7-jdk
```
If you're on ubuntu 18.04+ run:
```
apt install gir1.2-goocanvas-2.0 python3-gi python3-gi-cairo python3-pygraphviz gir1.2-gtk-3.0 ipython3
```
To enter the ns-3 folder
```
cd ./ns-3
```

To run tests
```
./test.py -c core
```

Now, to create a connection between 2 machines, copy the file named `first.cc` in `./tutorial/example/` to `./scratch` run:
```
./waf --run scratch/first
```

Now, to run the animator
```
cd ../
ls
cd ./netanim-3.108
./NetAnim
```

After running the commands above, you'll see a application has started, select the xml file that is created after compiling step, after selecting it you'll be able to see the packets transferring.
