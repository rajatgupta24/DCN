## Experiment 2

### Steps to run the code.

1. Code should be in the directory: `ns-allinone-3.27/ns-3.27/scratch`

2. Move to `ns-3.27` directory using the command: 
```bash
cd ../
```

3. Run the command: 
```bash
./waf --run/scratch/<program-name>
```

4. Output will be displayed on the terminal.

5. To view the animation run: 
```bash
cd ns-allinone-3.27/netanim-3.108
```

6. Run the command to launch the NetAnim application:
```bash
./NetAnim
```

8. Select the `XML` file, that is created after compilation.
9. Click the play button to run the animation.

## Experiment 2(a)

### Aim:
Create a 2 nodes point to point connection using ns3

### source Code:
```cpp
// Module Include
#include "ns3/core-module.h"
#include "ns3/network-module.h"
#include "ns3/internet-module.h"
#include "ns3/point-to-point-module.h"
#include "ns3/applications-module.h"
#include "ns3/netanim-module.h"

// C++ namespace called ns3
using namespace ns3;

NS_LOG_COMPONENT_DEFINE ("FirstScriptExample");

int main (int argc, char *argv[])
{
    // Allow the user to override any of the defaults and the above
    CommandLine cmd;
    cmd.Parse (argc, argv);

    // Enable two logging components
    Time::SetResolution (Time::NS);
    LogComponentEnable ("UdpEchoClientApplication", LOG_LEVEL_INFO);
    LogComponentEnable ("UdpEchoServerApplication", LOG_LEVEL_INFO);

    // Create the ns-3 Node objects
    NodeContainer nodes;
    nodes.Create (2);

    // Instantiates a PointToPointHelper object on the stack
    PointToPointHelper pointToPoint;
    pointToPoint.SetDeviceAttribute ("DataRate", StringValue ("5Mbps"));
    pointToPoint.SetChannelAttribute ("Delay", StringValue ("2ms"));

    // Create the NetDevice objects
    NetDeviceContainer devices;
    devices = pointToPoint.Install (nodes.Get(0), nodes.Get(1));

    // Install on each of the nodes in the node container
    InternetStackHelper stack;
    stack.Install (nodes);

    // To associate the devices on our nodes with IP addresses
    Ipv4AddressHelper address;
    address.SetBase ("10.1.1.0", "255.255.255.0");

    Ipv4InterfaceContainer interfaces = address.Assign (devices);
    
    // Populate routing tables for nodes 
    Ipv4GlobalRoutingHelper::PopulateRoutingTables();

    // Set up a UDP echo server application
    UdpEchoServerHelper echoServer (9);

    // Install server application node
    ApplicationContainer serverApps = echoServer.Install (nodes.Get (1));
    serverApps.Start (Seconds (1.0));
    serverApps.Stop (Seconds (10.0));

    // Set remote address and port
    UdpEchoClientHelper echoClient (interfaces.GetAddress (1), 9);
    echoClient.SetAttribute ("MaxPackets", UintegerValue (1));
    echoClient.SetAttribute ("Interval", TimeValue (Seconds (1.0)));
    echoClient.SetAttribute ("PacketSize", UintegerValue (1024));

    // Install client application node
    ApplicationContainer clientApps = echoClient.Install (nodes.Get (0));
    clientApps.Start (Seconds (2.0));
    clientApps.Stop (Seconds (10.0));

    // An XML file to be used by NetAnim
    AnimationInterface anim("m1.xml");
    anim.SetConstantPosition(nodes.Get(0), 1.0, 2.0);
    anim.SetConstantPosition(nodes.Get(1), 5.0, 5.0);

    // To run the simulation
    Simulator::Run ();
    Simulator::Destroy ();
    return 0;
}
```

### Output:

![](https://raw.githubusercontent.com/rajatgupta24/DCN/master/exp-2-a.png)
![](https://raw.githubusercontent.com/rajatgupta24/DCN/master/exp-2-a-1.png)


## Experiment 2(b)

### Aim:
To simulate a network containing 3 nodes with point-to-point connection using NS3.

### Source Code:
```cpp
// Module Include
#include "ns3/core-module.h"
#include "ns3/network-module.h"
#include "ns3/internet-module.h"
#include "ns3/point-to-point-module.h"
#include "ns3/applications-module.h"
#include "ns3/netanim-module.h"

// C++ namespace called ns3
using namespace ns3;

NS_LOG_COMPONENT_DEFINE ("FirstScriptExample");

int main (int argc, char *argv[])
{
    // Allow the user to override any of the defaults and the above
    CommandLine cmd;
    cmd.Parse (argc, argv);

    // Enable two logging components
    Time::SetResolution (Time::NS);
    LogComponentEnable ("UdpEchoClientApplication", LOG_LEVEL_INFO);
    LogComponentEnable ("UdpEchoServerApplication", LOG_LEVEL_INFO);

    // Create the ns-3 Node objects
    NodeContainer nodes;
    nodes.Create (3);

    // Instantiates a PointToPointHelper object on the stack
    PointToPointHelper pointToPoint;
    pointToPoint.SetDeviceAttribute ("DataRate", StringValue ("5Mbps"));
    pointToPoint.SetChannelAttribute ("Delay", StringValue ("2ms"));

    // Create the NetDevice objects
    NetDeviceContainer devices;
    devices = pointToPoint.Install (nodes.Get(0), nodes.Get(1));

    // Install on each of the nodes in the node container
    InternetStackHelper stack;
    stack.Install (nodes);

    // To associate the devices on our nodes with IP addresses
    Ipv4AddressHelper address;
    address.SetBase ("10.1.1.0", "255.255.255.0");

    Ipv4InterfaceContainer interfaces = address.Assign (devices);

    PointToPointHelper pointToPoint1;
    pointToPoint1.SetDeviceAttribute ("DataRate", StringValue ("5Mbps"));
    pointToPoint1.SetChannelAttribute ("Delay", StringValue ("2ms"));

    devices = pointToPoint1.Install (nodes.Get(1), nodes.Get(2));
    address.SetBase ("10.1.2.0", "255.255.255.0");
    interfaces = address.Assign(devices);
    
    // Populate routing tables for node
    Ipv4GlobalRoutingHelper::PopulateRoutingTables();

    // Set up a UDP echo server application
    UdpEchoServerHelper echoServer (9);

    // Install server application node
    ApplicationContainer serverApps = echoServer.Install (nodes.Get(1));
    serverApps.Start (Seconds (1.0));
    serverApps.Stop (Seconds (10.0));

    // Set remote address and port
    UdpEchoClientHelper echoClient (interfaces.GetAddress (1), 9);
    echoClient.SetAttribute ("MaxPackets", UintegerValue (1));
    echoClient.SetAttribute ("Interval", TimeValue (Seconds (1.0)));
    echoClient.SetAttribute ("PacketSize", UintegerValue (1024));

    // Install client application node
    ApplicationContainer clientApps = echoClient.Install (nodes.Get(0));
    clientApps.Start (Seconds (2.0));
    clientApps.Stop (Seconds (10.0));

    // An XML file to be used by NetAnim
    AnimationInterface anim("m1.xml");
    anim.SetConstantPosition(nodes.Get(0), 1.0, 2.0);
    anim.SetConstantPosition(nodes.Get(1), 5.0, 5.0);
    anim.SetConstantPosition(nodes.Get(2), 10.0, 10.0);

    // To run the simulation
    Simulator::Run ();
    Simulator::Destroy ();
    return 0;
}
```

### Output

![](https://raw.githubusercontent.com/rajatgupta24/DCN/master/exp-2-b-1.png)
![](https://raw.githubusercontent.com/rajatgupta24/DCN/master/exp-2-b-2.png)

## Experiment 2(c)

### Aim:
To simulate a network containing 4 nodes with point-to-point connection using NS3.

### Source Code:
```cpp
// Module Includes
#include "ns3/core-module.h"
#include "ns3/network-module.h"
#include "ns3/internet-module.h"
#include "ns3/point-to-point-module.h"
#include "ns3/applications-module.h"
#include "ns3/netanim-module.h"

// C++ namespace called ns3
using namespace ns3;

NS_LOG_COMPONENT_DEFINE ("FirstScriptExample");

// Define a main function
int main (int argc, char *argv[])
{
    // Allow the user to override any of the defaults and the above
    CommandLine cmd;
    cmd.Parse (argc, argv);

    Time::SetResolution (Time::NS);
    // Enable two logging components
    LogComponentEnable ("UdpEchoClientApplication", LOG_LEVEL_INFO);
    LogComponentEnable ("UdpEchoServerApplication", LOG_LEVEL_INFO);

    // Create the ns-3 Node object
    NodeContainer nodes;
    nodes.Create (4);

    PointToPointHelper pointToPoint;
    pointToPoint.SetDeviceAttribute ("DataRate", StringValue ("5Mbps"));
    pointToPoint.SetChannelAttribute ("Delay", StringValue ("2ms"));

    // Create the NetDevice objects
    NetDeviceContainer devices;
    // Install NICs to Nodes and link Point-to-point
    devices = pointToPoint.Install (nodes.Get(0), nodes.Get(1));

    // Install on each of the nodes in the node container
    InternetStackHelper stack;
    stack.Install (nodes);

    // To associate the devices on our nodes with IP addresses
    Ipv4AddressHelper address;
    address.SetBase ("10.1.1.0", "255.255.255.0");

    Ipv4InterfaceContainer interfaces = address.Assign (devices);

    // Instantiates a PointToPointHelper object on the stack
    PointToPointHelper pointToPoint1;
    pointToPoint1.SetDeviceAttribute ("DataRate", StringValue ("5Mbps"));
    pointToPoint1.SetChannelAttribute ("Delay", StringValue ("2ms"));

    devices = pointToPoint1.Install (nodes.Get(1), nodes.Get(2));
    address.SetBase ("10.1.2.0", "255.255.255.0");
    interfaces = address.Assign(devices);
    
    PointToPointHelper pointToPoint2;
    pointToPoint2.SetDeviceAttribute ("DataRate", StringValue ("5Mbps"));
    pointToPoint2.SetChannelAttribute ("Delay", StringValue ("2ms"));

    devices = pointToPoint2.Install (nodes.Get(2), nodes.Get(3));
    address.SetBase ("10.1.3.0", "255.255.255.0");
    interfaces = address.Assign(devices);
    
    Ipv4GlobalRoutingHelper::PopulateRoutingTables();

    // Set up a UDP echo server application
    UdpEchoServerHelper echoServer (9);

    ApplicationContainer serverApps = echoServer.Install (nodes.Get(1));
    serverApps.Start (Seconds (1.0));
    serverApps.Stop (Seconds (10.0));

    // Set remote address and port
    UdpEchoClientHelper echoClient (interfaces.GetAddress (1), 9);
    echoClient.SetAttribute ("MaxPackets", UintegerValue (1));
    echoClient.SetAttribute ("Interval", TimeValue (Seconds (1.0)));
    echoClient.SetAttribute ("PacketSize", UintegerValue (1024));

    // Install client application node
    ApplicationContainer clientApps = echoClient.Install (nodes.Get(0));
    clientApps.Start (Seconds (2.0));
    clientApps.Stop (Seconds (10.0));

    // An XML file to be used by NetAnim
    AnimationInterface anim("m1.xml");
    anim.SetConstantPosition(nodes.Get(0), 1.0, 2.0);
    anim.SetConstantPosition(nodes.Get(1), 5.0, 5.0);
    anim.SetConstantPosition(nodes.Get(2), 10.0, 10.0);
    anim.SetConstantPosition(nodes.Get(3), 15.0, 15.0);

    //To run the simulation
    Simulator::Run ();
    Simulator::Destroy ();
    return 0;
}
```
### Output

![](https://raw.githubusercontent.com/rajatgupta24/DCN/master/exp-2-c-1.png)