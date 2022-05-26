## Experiment 3
### Aim:
To simulate the given architecture in NS3

![arch-img-2](https://raw.githubusercontent.com/rajatgupta24/DCN/master/pic.png)


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

    // Create the ns-3 Node objects (hosts & routers)
    NodeContainer hosts;
    NodeContainer routers;
    hosts.create(1)
    routers.Create(4);
    
    InternetStackHelper stack;
    Ipv4AddressHelper address;
    
    // Install on each of the nodes in the node container
    InternetStackHelper stack;
    stack.Install(routers);
    stack.Install(hosts);

    // Instantiates a PointToPointHelper object on the stack
    PointToPointHelper p1, p2, p3 p4;

    // Append the contents of another NodeContainer to the end of this container
    NodeContainer subnet1;
    
    // Append the contents of another NodeContainer to the end of this container
    subnet1.Add(hosts.Get(0));
    subnet1.Add(routers.Get(0));
    
    NetDeviceContainer subnet1device = p1.install(subnet1);
    address.SetBase ("10.1.1.0", "255.255.255.0");
    
    Ipv4InterfaceContainer subnet1interface = address.Assign (subnet1devices);

    // Append the contents of another NodeContainer to the end of this container
    NodeContainer subnet2;
    subnet2.Add(routers.Get(0));
    subnet2.Add(routers.Get(1));
    
    NetDeviceContainer subnet2device = p2.install(subnet2);
    address.SetBase ("10.1.2.0", "255.255.255.0");
    
    Ipv4InterfaceContainer subnet2interface = address.Assign (subnet2devices);

    // Append the contents of another NodeContainer to the end of this container
    NodeContainer subnet3;
    subnet3.Add(routers.Get(1));
    subnet3.Add(routers.Get(2));
    
    NetDeviceContainer subnet3device = p3.install(subnet3);
    address.SetBase ("10.1.3.0", "255.255.255.0");
    
    Ipv4InterfaceContainer subnet3interface = address.Assign (subnet3devices);

    // Append the contents of another NodeContainer to the end of this container
    NodeContainer subnet4;
    subnet4.Add(routers.Get(1));
    subnet4.Add(routers.Get(3));
    
    NetDeviceContainer subnet4device = p4.install(subnet4);
    address.SetBase ("10.1.4.0", "255.255.255.0");
    
    Ipv4InterfaceContainer subnet4interface = address.Assign (subnet4devices);
    
    // Populate routing tables for nodes
    Ipv4GlobalRoutingHelper::PopulateRoutingTables();

    // Set up a UDP echo server application
    UdpEchoServerHelper echoServer (9);

    // Install server application node
    ApplicationContainer serverApps = echoServer.Install (routers.Get(3));
    serverApps.Start (Seconds (1.0));
    serverApps.Stop (Seconds (10.0));

    // Set remote address and port
    UdpEchoClientHelper echoClient (interfaces.GetAddress (1), 9);
    echoClient.SetAttribute ("MaxPackets", UintegerValue (1));
    echoClient.SetAttribute ("Interval", TimeValue (Seconds (1.0)));
    echoClient.SetAttribute ("PacketSize", UintegerValue (1024));

    //Install client application node
    ApplicationContainer clientApps = echoClient.Install (nodes.Get(0));
    clientApps.Start (Seconds (2.0));
    clientApps.Stop (Seconds (10.0));

    // An XML file to be used by NetAnim
    AnimationInterface anim("m1.xml");
    anim.SetConstantPosition(hosts.Get(0), 10, 10);
    anim.SetConstantPosition(routers.Get(0), 20, 10);
    anim.SetConstantPosition(routers.Get(1), 30, 10);
    anim.SetConstantPosition(routers.Get(2), 40, 20);
    anim.SetConstantPosition(routers.Get(3), 40, 0);

    // To actually run the simulation
    Simulator::Run ();
    Simulator::Destroy ();
    return 0;
}
```
### Output

![](https://raw.githubusercontent.com/rajatgupta24/DCN/master/exp-3-1.png)
![](https://raw.githubusercontent.com/rajatgupta24/DCN/master/exp-3-2.png)