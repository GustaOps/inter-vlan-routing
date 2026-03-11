# Explanations
# step 2

VLANs 10 and 20 must be properly configured and assigned before being used in the network, it's common to apply it a name after configuring it.

# switchport access

In switchport access mode, a switch port is associated with a single VLAN. Frames sent to the end device are transmitted untagged because hosts generally do not process 802.1Q tags.

In trunk mode, the port is configured to carry traffic from multiple VLANs. The switch adds or preserves the VLAN tag (802.1Q) so that the receiving network device can properly identify the VLAN of each frame.

# step3

# no shutdown

On Cisco routers, interfaces are administratively down by default.
The no shutdown command is used to manually enable the interface.
Without this command, the interface will remain disabled even if a cable is connected.

# encapsulation dot1q ...

in router-on-a-stick method we're commonly using a single physical link between router and switch, but since there is only one link to carry all the VLAN traffic, subinterfaces are required to logically separe multiple VLANs over a single physical interface, so this command is identifying which subinterface receives each VLAN id.

# ip address

after configuring encapsulation, we must assign an IP address to the subinterface. this IP acts as the default gateway for the devices within that VLAN. that's why we made it twice, once for each VLAN.


# STP

STP protocol must appear once you settle the 3 switches or more connected through physical link, Spanning Tree Protocol acts blocking one of your routes preventing it from turning an infinite loop.

[STP](images.md#STP)

# ACL 

enable >> configure terminal >> ip >> access-list >> extended >> 100
once inside the ACL configuration >> permit >> tcp >> 192.168.1.0 0.0.0.255 host 192.168.2.2

explanation:
100 stands for the acl identifier, you must place a number between 100 and 199 if it is extended or you can just name it
tcp and icmp are 2 different types of protocol.
first IP is the host or the source                                                                                                          wildcard 0.0.0.255 means first three octets must correspond while the last varies.                                                          host = 0.0.0.0(it is actually a shortcut) thats why theres no wildcard after the server's IP.

I'll show you some images to help you visualize it clearly.

[check-it-here](images.md#ACL-Ping-test)
