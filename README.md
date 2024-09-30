# Small Office Network Lab
### Introduction

This project is about creating a network of user end devices and servers. The Project Objectives below were provided to me by a good [friend](https://www.linkedin.com/in/matthew-straub1/) that pushed me to apply theoretical knowledge into a real-world practical setting. I was provided with objectives list below and tasks to pursue that would help further develop my skills of networking concepts such as VLANs, router and switch configurations, DHCP, Spanning Tree protocols, and configuring routing protocols and much more. This lab was designed and simulated inside **Cisco Packet Tracer**.

## Project Objectives
<details>
  <summary>Project Objectives</summary>

1. **Create a logical network** that includes:
   - One router, one access point, two switches, and one cable modem for infrastructure.
   - Three servers, one printer, five PCs, and two laptops as end-user devices.
   - Connect all devices using either a hierarchical or mesh topology.
   - Create rectangles around the PCs/Laptops (endpoints) and Servers/Printers/Access Point (Services) to keep end-user devices separate from infrastructure devices.
   - Add a note to designate the client and server networks.

2. **Configure all network appliances, servers, and services** at a basic level:
   - Set hostnames, IP addresses, MOTDs, encrypted passwords/secrets, etc.
   - Allow communication from PC3 to Server1 via IP and hostname without being on the same switch, utilizing both static and DHCP addressing.
   - Ensure all uplink traffic utilizes at least 1 GB cabling (fiber/SFP or Ethernet).
   - Validate the network by ensuring communication on at least 3 different devices using wired and wireless connectivity.

3. **Block all inbound communications to PC5** but allow outbound communication only to the endpoint LAN (labeled client network).

4. **Create a network loop** and ensure connectivity is slowed or stopped (provide documentation of loop/proof). Then configure STP/RSTP on all switches and ensure connectivity is restored.

5. **Secure the switches**:
   - Disable all unused ports on all switches.
   - Add a hostname to all devices if not already done.
   - Configure all switch ports as access ports, aside from one port on each switch to be used as a trunk.
   - Assign all ports to VLAN 1.
   - Configure port security/MAC filtering on at least one port.

6. **Configure VLANs**:
   - Properly label/add descriptions to all ports.
   - Configure one port to utilize VLAN 5 on each switch and add one workstation to utilize VLAN 5.
   - Ensure traffic can be passed from switch to switch via the trunk ports and to the workstation.
   - Ensure the workstation on VLAN 5 is isolated from the rest of the network on VLAN 1.

7. **Configure your router** to send all traffic coming from PC1 to PC2.

8. **Configure a dynamic routing protocol** (e.g., RIP, BGP, OSPF).

</details>


## Network Overview
This project details a SOHO network architecture designed to accommodate a **seven** user-end devices, comprising **five** Personal Computers (PCs) and **two** Laptops. These devices are integrated into the network to facilitate data communication and resource sharing. The network topology employed here is a refined **hybrid star topology**, structured to optimize connectivity and network performance.

At the core of this network design, the five PCs are connected through a centralized switch, **Switch 2**, establishing a star topology configuration. This arrangement simplifies network management and also enhances reliability, as each PC directly connects to **Switch 2**, ensuring an isolated and secure communication path. Similarly, the two laptops establish wireless connections to a dedicated access point, which in turn connects back to **Switch 2**, mirroring the star topology configuration.

**Switch 2** serves an important function in the network's infrastructure, acting as a conduit between user-end devices and critical network resources. It is directly connected to another switch, **Switch 1**, through a dedicated link. **Switch 1** is positioned on the **server side** of the network, where it connects three servers and a printer, maintaining the star topology principle. This arrangement of Switch 1 and Switch 2 encapsulates the essence of the hybrid star topology, combining both wired and wireless configurations to create a versatile network infrastructure.

Further enhancing the network's functionality, **Switch 1** interfaces with a **Gateway router**. This **router** is instrumental in facilitating inter-VLAN routing, allowing seamless communication across different network segments. It serves as the gateway to the wider internet, connecting to a **cable modem** that provides external network access. This configuration ensures that both internal resources and external internet services are readily accessible to all network devices.

The IP addressing scheme is a critical component of this network design, as outlined in **Table 1** of the project documentation. It employs a mix of static and dynamic IP addressing strategies to cater to the varied requirements of the network's components. Specifically, the 192.168.1.0 subnet is designated for dynamic IP addressing, primarily assigned to the PCs, to support flexibility and ease of management. The other two subnets are configured with static IP addresses, ensuring stable and predictable network communication paths for essential services and devices. **Server 3** is designated as the **DHCP (Dynamic Host Configuration Protocol) server**, centralizing the dynamic IP address allocation process and simplifying network administration.

This network design highlights a thoughtful integration of hardware and logical configurations, tailored to meet the project's requirements while ensuring scalability, reliability, and efficient network performance.

**Table 1: IP Address Scheme**

| **Vlan** | **Subnet** | **Subnet Mask** | **Usable IP Addresses** | **1st Usable Address** | **Last Usable Address** | **Broadcast Address** |
| --- | --- | --- | --- | --- | --- | --- |
| Vlan1 | 192.168.1.0 | 255.255.255.0 | 254 | 192.168.1.1 | 192.168.1.254 | 192.168.1.255 |
| Vlan2 | 192.168.2.0 | 255.255.255.0 | 254 | 192.168.2.1 | 192.168.2.254 | 192.168.2.255 |
| Vlan3 | 192.168.3.0 | 255.255.255.0 | 254 | 192.168.3.1 | 192.168.3.254 | 192.168.3.255 |
| Vlan5 | 192.168.5.0 | 255.255.255.0 | 254 | 192.168.5.1 | 192.168.5.254 | 192.168.5.255 |

---
### **Task**

**Create a logical network that has the following devices and endpoints and create rectangles around the PCs/Laptops (endpoints) and Servers/Printers/Access Point (Services) being sure to keep end user devices separate from the infrastructure devices, add a note to designate the client and server networks. One router, one access point, two switches, and one cable modem for infrastructure. Three servers, one printer, five PCs, and two laptops as end-user devices. Connect all devices using either a hierarchical or mesh topology.**

- The diagram below represents the network diagram as created and simulated in the cisco packet tracer application.
    ![Untitled](https://github.com/user-attachments/assets/d454c266-4d01-4e3b-ae45-08e3e6f5cb57)
---

### **Task: Configure all network appliances, servers and services at a basic level (Hostnames, IP address, MOTD, encrypted password/secret, enabled etc.)**

The basic configuration including username (admin), password (abc123), enable secret (abc123), password encryption, hostname, IP addresses and message of the day of the router and the two switches are as follows:

- **Router1 Configuration**
  ```
  username admin password abc123
  enable secret abc123
  service password-encryption
  hostname “Gateway”
  banner motd c Hello!! c
  ```
    ![image](https://github.com/user-attachments/assets/a9bc7aa0-daed-4a47-bd7c-143728ba7da8)
    ![image](https://github.com/user-attachments/assets/3643ff3e-7e21-4aa7-b609-abd99d4936ea)
    ![image](https://github.com/user-attachments/assets/ffe47088-c725-467b-9884-cec0d445bc47)
    ![image](https://github.com/user-attachments/assets/ac7c6972-46c2-40d9-a8ac-fcf277690052)

- **Switch 1 Configuration**
    
    ```
    username admin password abc123
    enable secret abc123
    service password-encryption
    hostname “Gateway”
    banner motd c Hello!! c
    ```
    ![image](https://github.com/user-attachments/assets/c037ab6d-aa1d-4091-9912-ee5f63cbfd11)
    ![image](https://github.com/user-attachments/assets/3584a662-1c40-467c-b453-1719c895b741)

- **Switch 2 Configuration**
    
    ```
    username admin password abc123
    enable secret abc123
    service password-encryption
    hostname “Switch2”
    banner motd c Hello!! C
    interface vlan 1
    ip address 192.168.1.249
    ip default-gateway 192.168.1.254
    ```
    ![image](https://github.com/user-attachments/assets/4a5d5034-2072-4fed-9383-e0082ed4158f)
    ![image](https://github.com/user-attachments/assets/7394a42d-39c0-4f08-94dc-dd9905ff852e)
    

The `username command` creates a user with a password. The `enable command` sets a secret that is needed to be entered when entering into privileged mode. The `service password-encryption` command encrypts the password that has been set by username command earlier. The `hostname command` sets the hostname of device. The `banner command` configures the message of the day. 

In order to set the IP address of switch the `interface VLAN` command is used because the IP address is set in a virtual interface on a switch. The `ip default-gateway` command is entered in global configuration mode on the switches in order for the switches to be accessed by any PC or laptop that are not in VLAN 1.

From the above figures we can see that the password “abc123” has been encrypted with the command service password-encryption.

---

### **Task: Allow communication from PC3 to Server1 via IP and hostname without being on the same switch, utilize both static and DHCP addressing**

- In order to permit traffic from PC3 to Server 1 only, an access list named as MYLIST has been created that allows traffic from PC3 with an address of 192.168.3.1 to Server 1 which has the IP address of 192.168.1.251. The next entry in the access list denies traffic from PC3 to all other devices. The access list configuration is done by the following commands:
    
    ```
    ip access-list extended MYLIST
    permit ip host 192.168.3.1 host 192.168.1.251
    deny ip any any
    ```
    
    ![image](https://github.com/user-attachments/assets/bddeacfd-9858-42e4-8ee0-017d374b6fc5)
    
    - The first command creates the access list MYLIST. The second command allows all the traffic from PC3 having IP address of 192.168.3.1 to Server 1 having IP address of 192.168.1.251. The third command denies all the traffic that is other than the traffic between PC3 and Server 1. In order to apply the access list the following command is needed to be entered on sub interface that acts as gateway for PC3 on the router:
    
    ```
    ip access-group MYLIST in
    ```
    
    - The `in` keyword in the above command means the access list is applied on traffic coming from inside this interface. The outcome of the access list is shown in the figure below
    
    ![image](https://github.com/user-attachments/assets/ca778850-a15e-4d41-8023-fd17c2b83d1d)
    

- PC3 has to have a static IP address for that purpose therefore a static IP address of 192.168.3.1 has been assigned to it as shown in the figure below
    
    ![image](https://github.com/user-attachments/assets/f02349b1-7ebb-46b5-94bb-9d0ade8c365f)

---

### **Task: Ensure all uplink (destined for router & modem) traffic utilizes at least 1 GB cabling (fiber / SFP or ethernet)**

- The figures below show that the link going from switch 2 to the router and from router to the cable modem are Gigabit Ethernet links.
- In the first figure the router is detected on Gig 0/1 of switch 2 as a neighbor while in the second figure the port Gig 0/0/1 has been assigned an IP address of 10.10.10.1 that is connected to the cable modem.
    
    ![image](https://github.com/user-attachments/assets/ab5c2311-7ec6-422b-8337-5abfadac1883)
    
    ![image](https://github.com/user-attachments/assets/9218b214-77c3-4c72-8561-586499c7da83)

---

### **Task: Validate the network by ensuring communication on at least 3 different devices using wired and wireless connectivity**

- **PC1 to Laptop2**
    - The following figure shows PC1 sending four pings to Laptop 2 having IP address of 192.168.1.5 and receiving replies
        
      ![image](https://github.com/user-attachments/assets/fb9e1790-28a1-4434-a79d-43d4303a780e)
        
- **PC2 to Laptop1**
    - The following figure shows PC2 sending four pings to Laptop1 having IP address of 192.168.1.4 and receiving replies
        
        ![image](https://github.com/user-attachments/assets/1aeb5db1-3d3d-4943-81f9-5e15a6ce329e)
        
- **PC4 to Printer**
    - The following figure shows PC4 sending four pings to the printer having IP address of 192.168.1.201 and receiving replies.
    - The printer has been assigned a static IP address while all other end user devices in VLAN 1 receive their IP addresses from the DHCP server from server3.
        
        ![image](https://github.com/user-attachments/assets/fe51e3aa-52c0-4973-83eb-8994de5508ea)

---

### **Task: Block all inbound communications to PC 5 but allow communication outbound only to the endpoint LAN (labeled client network)**

- **PC5 Communication**
    - All the traffic coming towards PC5 has been denied at the router with the help of an access list named as BLOCK-VLAN5. Only the ping response from the local PCs and laptops has been allowed in the access list therefore, PC5 cannot communicate with any other device except the local LAN devices. The commands used to configure this access list are following:
        
        ```
        Extended IP access list BLOCK-VLAN5
        10 permit icmp 192.168.1.0 0.0.0.255 192.168.5.0 0.0.0.255 echo-reply
        20 deny ip any any
        ```
        - The first command creates the access list named BLOCK-VLAN5. The second command on permits the ping replies from devices that lies in the local VLAN1 subnet. The final command denies all other traffic headed towards PC5. In order to apply the access list the following command is needed to be entered on sub interface that acts as gateway for PC5 on the router
        
        ```
        ip access-group BLOCK-VLAN5 out
        ```
        
        - The `out` keyword in the above command means the access list is applied on traffic coming from outside towards this interface. The effect of the access list has been shown in the figures below in which PC5 pings PC4 successfully while PC4 cannot ping PC5
            
            ![image](https://github.com/user-attachments/assets/3fd4632a-7469-41e9-b4ca-eda670f834f5)
            
            ![image](https://github.com/user-attachments/assets/e425613b-4cac-4257-852e-11e35a5e1aaf)

---

### **Task: Create a loop within the network and ensure connectivity is slowed or stopped (provide documentation of loop/proof) then configure STP / RSTP on all switches and ensure connectivity is restored.**

- **Spanning tree**
    - As we turn off the spanning tree and link the two switches with two links which creates a loop, the traffic from any PC does not pass through the switches. It has been shown in the figure below PC1 tries to ping server 1 but the request fails.
        
      ![image](https://github.com/user-attachments/assets/51ec35a0-093a-45bb-b725-cf1ce1599439)
        
    - The following command has been used to configure spanning tree on both the switches: **`spanning-tree vlan 1-5`**
        
        ![image](https://github.com/user-attachments/assets/6700f4c8-c095-43c9-9d3a-9b2b7c6006bd)

        - The spanning tree is needed to be created separately for every VLAN present on the switch therefore the VLANs are needed to be specified in this command.
        - As soon as we configure spanning trees on both the switches, PC1 successfully pings server 1 as shown in the figures below
            
            ![image](https://github.com/user-attachments/assets/179661da-71a7-43dc-aec7-1ac88b8ddad6)

---

### **Task: Disable all unused ports on all switches, add a hostname to all devices if not already done, configure all switch ports as access port aside from one port on each switch to be used as Trunk, assign all ports VLAN 1 and configure port security / mac filtering on at least one port.**

- **Ports Configuration**
    - The following figures show all unused ports on switch 1 and switch 2 are disabled
        
        ![image](https://github.com/user-attachments/assets/89a2f5d2-345c-4f5f-b471-e72d42e46017)
        
        ![image](https://github.com/user-attachments/assets/4342c1dc-edfd-48c9-a3f3-05a15c2b07fb)
        
- The following figures show that all the ports have been set to access mode with VLAN1 except for trunk ports on both the switches and the fourth port on switch 1 and the fifth port on switch 2 have been applied port securities in a way that the current devices connected to them are only authenticated with the port security sticky command. Switch 2 has access vlan of 3 and 5 for PC3 and PC5 accordingly. The commands used access Vlan and MAC filtering are
    
    ```
    switchport access vlan 1
    switchport port-security mac-address sticky
    ```
    
    - Switch 2 has access VLAN of 3 and 5 for PC3 and PC5 accordingly.
        
        ![image](https://github.com/user-attachments/assets/1ae932a3-49b0-41eb-91c9-bad3b0e15925)
        
        ![image](https://github.com/user-attachments/assets/157afc61-8fda-41fa-b282-16e6fe4e2b32)

---

### **Task: Properly label / add description to all ports, configure one port to utilize VLAN 5 on each switch and add one workstation to utilize VLAN 5 then ensure traffic can be passed from switch to switch via the trunk ports and to the workstation. Ensure the workstation on VLAN 5 is isolated from the rest of the network on VLAN 1**

- **Ports labelling and VLAN 5 traffic**
    - The following figures show all the ports on switch 1 and 2 labelled accordingly to the devices attached to them. The command used for ports labelling is: `description “Server 1”`
        - The above command is needed to be configured under every port configuration accordingly.
    
     ![image](https://github.com/user-attachments/assets/680c6540-06e6-4e32-b46f-07790dc51a57)

     ![image](https://github.com/user-attachments/assets/e495653e-4523-476a-b4eb-26317da2ceb2)

    
- The PC5 has been configured for vlan 5	having the ip address of 192.168.5.1. The following commands are used for configuration of Vlan 5 sub interface on the router
    
    ```
    Interface GigabitEthernet0/0/0.5
    Encapsulation dot1Q 5
    ip address 192.168.5.254 255.255.255.0
    ip helper-address 192.168.1.253
    ip access-group BLOCK-VLAN5 out
    ```
    
    ![image](https://github.com/user-attachments/assets/e56576c7-5bb5-4324-830b-7eb58f7e61d1)
    
- The following figure shows traffic from PC5 travelling in Vlan 5 over trunk port between the switches and then the trunk port between the switch 1 and router and all the way back for ping response from the router having ip address of 192.168.5.254. The encapsulation dot1Q 5 command means that the traffic with tagged vlan 5 will be received on this sub interface.
    
    ![image](https://github.com/user-attachments/assets/8450ea97-4b1e-4ca2-a1bf-3a605fc00574)

---

### **Task: Configure your router to send all traffic coming from PC1 to PC2**

- **PC1 to PC2 Traffic**
    - In order to send all traffic from PC1 to PC2 which are in different VLANs, we need to configure the router as the gateway for both these VLANs. The gateway IP address on the DHCP server for these VLANs is set as 192.168.1.254 and 192.168.2.254. So we need to create two sub interfaces on the router with these two IP addresses. The commands used for creating these two interfaces on the router are as follows:
        
        ```
        interface GigabitEthernet0/0/0.1
        encapsulation dot1Q 1 native
        ip address 192.168.1.254 255.255.255.0
        ip helper-address 192.168.1.253
        ```
        
        ```
        interface GigabitEthernet0/0/0.2
        encapsulation dot1Q 2
        ip address 192.168.2.254 255.255.255.0
        ip helper-address 192.168.1.253
        ```
        
        - The first command creates the interface. The second command tells the router that the traffic on this interface will arrive from this numbered Vlan. The third command sets the IP address of the interface which is the gateway IP address for each Vlan as set in the DHCP server. The last command is used to tell the sub interface about the DHCP IP address. After setting these interfaces on the router, the router knows the routes to both the PCs which are on these sub interfaces and thus can route all the traffic from PC1 to PC2.

---

### **Task:** **Configure Dynamic Routing Protocol**

- **Dynamic Routing Protocol Configuration**
    - Routing Information Protocol (RIP) has been selected to be configured as a dynamic routing protocol on the router. To configure RIP we need to create an instance of the protocol with the following command first: `router rip`
    - After entering this command we are then taken to RIP configuration mode where we need to state which subnets we have to share/advertise with other routers if any. In our case we have four subnets, three of which are local subnets (192.168.1.0, 192.168.3.0, 192.168.5.0) and one public (10.10.10.0).
    - As discussed above the PC5 in Vlan 5 having ip address of 192.168.5.0 only needs to communicate with local devices which means it does not need to communicate with public devices so the Vlan 5 will not be needed to advertise with any other router. In order to advertise the remaining subnets the following commands have been used
        
        ```
        network 10.0.0.0
        network 192.168.1.0
        network 192.168.3.0
        ```
        ![image](https://github.com/user-attachments/assets/89e19dc9-e478-44e2-b52f-b22c4a4cf884)        
        - In the above figure only three networks have been advertised in the RIP protocol. The PC5 in the subnet of 192.168.5.0 is not permitted to have any traffic from outside as per requirement therefore it has not been advertised in the protocol.
