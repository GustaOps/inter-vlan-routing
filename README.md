# Inter-vlan-routing

# Objective 
to configure a connection between 2 different VLANs among the computer network. Project using router-on-a-stick method

# Tools in use
1 router (model 1941)
3 switches (model 2950T-24)
4 PCs 
straight-through and crossover internet cables 

# IP Addressing Table
| Device  | VLAN | IP Address     | Subnet Mask     | Port/Interface        | Default Gateway |
|----------|------|---------------|----------------|-----------------------|-----------------|
| PC0      | 10   | 192.168.0.2   | 255.255.255.0  | Fa0/1 - Switch0       | 192.168.0.1     |
| PC1      | 20   | 192.168.1.2   | 255.255.255.0  | Fa0/2 - Switch0       | 192.168.1.1     |
| PC2      | 10   | 192.168.0.3   | 255.255.255.0  | Fa0/1 - Switch1       | 192.168.0.1     |
| PC3      | 20   | 192.168.1.3   | 255.255.255.0  | Fa0/2 - Switch1       | 192.168.1.1     |
| Router   | 10   | 192.168.0.1   | 255.255.255.0  | G0/0.10 - Switch2     | —               |
| Router   | 20   | 192.168.1.1   | 255.255.255.0  | G0/0.20 - Switch2     | —               |

# STEP BY STEP/PROCEDURE
First of all, we're going to assure a connection in equal VLANs
to make it more managable (each VLAN will use a different subnet to enable proper Layer 3 routing)
# FOLLOW THE IP ADDRESSING TABLE!!
# STEP 1
place the devices
straight-through cable connection between different devices (e.g. PC-SWiTCH and SWITCH-ROUTER).
crossover cable connection between SWITCHES
assign manually an IP address and the default gateway corresponding to each PC
# STEP 2 
configure VLAN 10 and 20 for each SWITCH 0 and SWITCH 1  
text: enable >> configure terminal >> VLAN 10 >> (optional) name ... >> exit          
interface fa 0/1 >> switchport mode access >> switchport access vlan 10 >>         
exit and then repeat: enable >> configure terminal >> VLAN 20 >> exit              
interface fa 0/2 >> switchport mode access >> switchport access vlan 20 

For SWITCH 2, text: enable >> configure terminal >> VLAN 10 >> exit           
repeat: VLAN 20
(although there's no need to assign interfaces to these VLANs, you still need to create it)              
exit and then make sure trunk mode is connected between SWITCH 2-ROUTER            
stil in the configure terminal, >> interface fa 0/3 >> switchport mode trunk                
Now already able to ping in equal VLANs.              
# STEP 3
now in the router we're going to configure sub-interfaces          
but first, enable the connection between router and switch to happen            
text: enable >> configure terminal >> interface g 0/0 >> no shutdown >> exit
then
text: interface g 0/0.10 >> encapsulation dot1Q 10 >> IP address 192.168.0.1 255.255.255.0 >> exit              
repeat: interface g 0/0.20 >> encapsulation dot1Q 20 >> IP address 192.168.1.1 255.255.255.0             

# TEST IT
enter PC0 prompt command >> ping 192.168.1.3
if successful, vlan should be working properly.
