## Experiment 3
### Aim:
To simulate the given architecture in NS3

![arch-img-2](https://user-images.githubusercontent.com/55191777/168140934-672c9339-5847-48a7-9d19-ec9c400af941.png)


### Source Code:
```cpp
#include "ns3/core-module.h"
#include "ns3/network-module.h"
#include "ns3/internet-module.h"
#include "ns3/point-to-point-module.h"
#include "ns3/applications-module.h"
#include "ns3/netanim-module.h"

using namespace ns3;

NS_LOG_COMPONENT_DEFINE ("FirstScriptExample");

int main (int argc, char *argv[])
{
    CommandLine cmd;
    cmd.Parse (argc, argv);

    Time::SetResolution (Time::NS);
    LogComponentEnable ("UdpEchoClientApplication", LOG_LEVEL_INFO);
    LogComponentEnable ("UdpEchoServerApplication", LOG_LEVEL_INFO);

    NodeContainer hosts;
    NodeContainer routers;
    hosts.create(1)
    routers.Create(4);
    
    InternetStackHelper stack;
    Ipv4AddressHelper address;
    
    stack.Install(routers);
    stack.Install(hosts);

    PointToPointHelper p1, p2, p3 p4;

    NodeContainer subnet1;
    subnet1.Add(hosts.Get(0));
    subnet1.Add(routers.Get(0));
    
    NetDeviceContainer subnet1device = p1.install(subnet1);
    address.SetBase ("10.1.1.0", "255.255.255.0");
    
    Ipv4InterfaceContainer subnet1interface = address.Assign (subnet1devices);

    NodeContainer subnet2;
    subnet2.Add(routers.Get(0));
    subnet2.Add(routers.Get(1));
    
    NetDeviceContainer subnet2device = p2.install(subnet2);
    address.SetBase ("10.1.2.0", "255.255.255.0");
    
    Ipv4InterfaceContainer subnet2interface = address.Assign (subnet2devices);

    NodeContainer subnet3;
    subnet3.Add(routers.Get(1));
    subnet3.Add(routers.Get(2));
    
    NetDeviceContainer subnet3device = p3.install(subnet3);
    address.SetBase ("10.1.3.0", "255.255.255.0");
    
    Ipv4InterfaceContainer subnet3interface = address.Assign (subnet3devices);

    NodeContainer subnet4;
    subnet4.Add(routers.Get(1));
    subnet4.Add(routers.Get(3));
    
    NetDeviceContainer subnet4device = p4.install(subnet4);
    address.SetBase ("10.1.4.0", "255.255.255.0");
    
    Ipv4InterfaceContainer subnet4interface = address.Assign (subnet4devices);
    
    Ipv4GlobalRoutingHelper::PopulateRoutingTables();

    UdpEchoServerHelper echoServer (9);

    ApplicationContainer serverApps = echoServer.Install (routers.Get(3));
    serverApps.Start (Seconds (1.0));
    serverApps.Stop (Seconds (10.0));

    UdpEchoClientHelper echoClient (interfaces.GetAddress (1), 9);
    echoClient.SetAttribute ("MaxPackets", UintegerValue (1));
    echoClient.SetAttribute ("Interval", TimeValue (Seconds (1.0)));
    echoClient.SetAttribute ("PacketSize", UintegerValue (1024));

    ApplicationContainer clientApps = echoClient.Install (nodes.Get(0));
    clientApps.Start (Seconds (2.0));
    clientApps.Stop (Seconds (10.0));

    AnimationInterface anim("m1.xml");
    anim.SetConstantPosition(hosts.Get(0), 10, 10);
    anim.SetConstantPosition(routers.Get(0), 20, 10);
    anim.SetConstantPosition(routers.Get(1), 30, 10);
    anim.SetConstantPosition(routers.Get(2), 40, 20);
    anim.SetConstantPosition(routers.Get(3), 40, 0);

    Simulator::Run ();
    Simulator::Destroy ();
    return 0;
}
```
