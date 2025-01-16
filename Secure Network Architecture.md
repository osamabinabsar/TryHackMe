# Secure Network Architecture

## VLAN


VLANs (Virtual Local Area Networks) are used to logically segment network traffic on a single physical network infrastructure. The 802.1q (or dot1q) tagging mechanism is essential in identifying which VLAN a frame belongs to as it traverses the network. Here's a step-by-step explanation of how this works:

1. **VLAN Basics**: VLANs allow network traffic to be separated into different broadcast domains, improving security and performance. Each VLAN is identified by a numerical value.

2. **Frame Tagging with 802.1q**: The 802.1q standard specifies how switches tag Ethernet frames with a VLAN ID. This tag allows switches to know which VLAN the frame belongs to.

3. **Structure of the 802.1q Tag**:
   - The 802.1q tag is a 4-byte field inserted into the Ethernet frame.
   - It consists of:
     - **TPID (Tag Protocol Identifier)**: A 2-byte value (0x8100) that indicates the presence of a VLAN tag.
     - **TCI (Tag Control Information)**: Another 2 bytes, containing:
       - **Priority Code Point (PCP)**: 3 bits for priority tagging (CoS).
       - **Canonical Format Indicator (CFI)**: 1 bit, usually set to 0 in Ethernet.
       - **VLAN ID**: 12 bits, representing the VLAN number (ranging from 1 to 4094).

4. **Tagging Process**:
   - When a frame enters a switch through a port assigned to a VLAN, the switch adds the 802.1q tag with the corresponding VLAN ID.
   - This tagged frame is then forwarded out of trunk ports that connect to other switches, allowing those switches to identify the frame's VLAN.

5. **Trunk vs. Access Ports**:
   - **Trunk Ports**: These carry traffic for multiple VLANs and transmit tagged frames.
   - **Access Ports**: These belong to a single VLAN and typically transmit untagged frames. The switch removes the tag before sending the frame out an access port.

6. **Reception and Forwarding**:
   - Upon receiving a tagged frame, a switch checks the VLAN ID and uses its forwarding table to determine where to send the frame.
   - Frames are only sent to ports that are part of the destination VLAN, ensuring traffic remains segregated.

7. **Native VLAN**:
   - Trunk ports can have a native VLAN that carries untagged traffic. Frames belonging to the native VLAN are transmitted without a tag.

8. **Frame Size Impact**:
   - Adding the 4-byte tag slightly increases the Ethernet frame size, but this does not typically cause issues in modern networks.

In summary, the 802.1q tag allows switches to manage and forward traffic across multiple VLANs by identifying the VLAN a frame belongs to, enabling efficient and secure network segmentation.


## Demonstration of how to configure tags on the interfaces of a switch.

- open vSwitch

![image](https://github.com/user-attachments/assets/fdeb4f79-9793-4955-970c-a0b74064e801)

The native VLAN is a fundamental concept in VLAN trunking and plays a crucial role in how switches handle untagged traffic. Here is a comprehensive explanation:

1. **Definition**: The native VLAN is the VLAN associated with untagged traffic on a trunk port. Frames without a VLAN tag are assigned to this VLAN.

2. **Purpose**: It is used to support devices that do not understand VLAN tagging, ensuring that untagged frames are handled correctly.

3. **Configuration**: The native VLAN is configured on trunk ports, and it is essential that both ends of a trunk agree on the native VLAN to avoid misrouting and security issues.

4. **Security Considerations**: 
   - The native VLAN can be a security risk if not properly configured, as untagged frames could be exploited in attacks like VLAN hopping.
   - Best practices recommend changing the native VLAN from the default (usually VLAN 1) to a non-default VLAN for security reasons.

5. **Interaction with Other VLANs**: 
   - Tagged frames carry their VLAN ID and are handled based on this information.
   - Untagged frames are assigned to the native VLAN, emphasizing the importance of consistent native VLAN configuration across trunks.

6. **Default Settings**: 
   - By default, the native VLAN is often VLAN 1, but it should be changed to enhance security.

7. **Protocol Considerations**: 
   - In the context of 802.1Q, the native VLAN handles untagged frames, and care must be taken to avoid mismatches in native VLAN configurations between switches.

8. **Best Practices**: 
   - Ensure consistent native VLAN configurations across all trunk links.
   - Be cautious with protocols like Dynamic Trunking Protocol (DTP) that can automatically negotiate trunk settings, as they may pose security risks.

In summary, the native VLAN is essential for managing untagged traffic in VLAN trunking, requiring careful configuration and consideration of security implications to maintain network integrity and performance.

![image](https://github.com/user-attachments/assets/e1f90016-0a5d-48e2-9390-59dd14612262)

## Zones

Depending on whom you speak to, every network architect may have a different approach/opinion to the language or requirements surrounding security zones. In this task, we will immerse you in the most commonly accepted security zone standards, keeping a minimalist approach to segmentation.
![image](https://github.com/user-attachments/assets/9002d0c3-2d51-4ba3-a02b-56341911308c)


## Traffic filtering, Network Security Policy


![image](https://github.com/user-attachments/assets/f06bdf82-d8ff-4eae-a889-73e0f93129cd)
![image](https://github.com/user-attachments/assets/a6c8dabe-2e76-4c1b-b4d1-4e6b06b7bee4)


## 


![image](https://github.com/user-attachments/assets/cd1aac93-775b-47ec-9874-574aea433be9)


### SSL/TLS Inspection

SSL/TLS inspection uses an SSL proxy to intercept protocols, including HTTP, POP3, SMTP, or other SSL/TLS encrypted traffic. Once intercepted, the proxy will decrypt the traffic and send it to be processed by a UTM (Unified Threat Management) platform. UTM solutions will employ deep SSL inspection, feeding the decrypted traffic from the proxy into other UTM services, including but not limited to web filters or IPS (Intrusion Prevention System), to process the information.

This solution may seem ideal, but what are the downsides? Some of you may have already noted that this requires an SSL proxy or MitM (Man-in-the-Middle). Even if a firewall or vendor has already implemented the solution, it will still act as a MiTM between your devices and the outside world; what if it intercepts potentially plain-text passwords? A corporation must assess the pros and cons of this solution, dependent on its calculated risk. You could allow all applications that you know are safer to prevent potential cons, but this solution will still have disadvantages. For example, an advanced threat actor could route their traffic through a cloud provider or a trusted domain.


## Common Attacks

**DHCP Snooping: A Comprehensive Overview**

**Definition and Purpose:**
- DHCP Snooping is a security feature that acts as a firewall between untrusted hosts and trusted DHCP servers. It is designed to prevent rogue DHCP servers from disrupting network operations by validating and rate-limiting DHCP traffic.

**Key Features:**
1. **Rogue DHCP Server Prevention:**
   - DHCP Snooping detects and blocks unauthorized DHCP servers that could distribute incorrect IP configurations or pose security threats.

2. **Validation and Rate-Limiting:**
   - It validates DHCP packets to ensure they are legitimate and rate-limits DHCP traffic to prevent flooding attacks.

3. **Layer Two Operation:**
   - Despite DHCP being a layer three protocol, DHCP Snooping operates at layer two, inspecting DHCP packets in Ethernet frames.

4. **DHCP Binding Database:**
   - The switch maintains a database of untrusted hosts and their leased IP addresses, used to validate traffic and integrate with other security protocols like Dynamic ARP Inspection.

**Conditions for Dropping DHCP Packets:**
1. **External DHCP Traffic:**
   - DHCP packets received from outside the network are dropped.

2. **Mismatched MAC Addresses:**
   - Packets where the source MAC address and DHCP client hardware address do not match are discarded.

3. **Unmatched DHCPRELEASE/DECLINE:**
   - These packets are dropped if they are received on an untrusted interface without a corresponding registered source address.

4. **Invalid Relay Agent Address:**
   - Packets with a relay agent address that is not 0.0.0.0 are dropped if not expected.

**Standardization and Vendor Implementation:**
- Although recognized in research papers, DHCP Snooping is not standardized by IEEE. However, it is generally consistent across vendors, unlike other protocols with vendor-specific implementations.

**Configuration and Considerations:**
- Enabling DHCP Snooping involves designating trusted and untrusted interfaces and managing the binding database.
- It is crucial to configure it carefully to avoid blocking legitimate traffic and to integrate it with other security features.

**Impact and Benefits:**
- Enhances network security by preventing unauthorized DHCP activity.
- Requires careful planning and testing to ensure it does not disrupt network operations.

**Integration with Network Security:**
- DHCP Snooping works seamlessly with VLANs and integrates with other security measures like IDS and firewalls to provide multi-layered protection.

**Monitoring and Logging:**
- The switch generates logs for invalid DHCP packets, which are valuable for security analysis and incident response.

**Conclusion:**
DHCP Snooping is a vital security mechanism for networks using DHCP for IP address assignment. Understanding its operation, configuration, and integration with other security solutions is essential for maintaining a secure and reliable network infrastructure.


**Dynamic ARP Inspection (DAI): A Crucial Security Mechanism**

Dynamic ARP Inspection (DAI) is a vital security feature designed to protect networks from ARP spoofing attacks. It operates by validating ARP packets against a trusted source, typically a binding table created by DHCP Snooping. Here's a comprehensive explanation of how DAI works and its importance in network security:

### Key Concepts and Operation:

1. **ARP Protocol Overview:**
   - ARP (Address Resolution Protocol) maps IP addresses to MAC addresses, enabling communication between devices on the same network.
   - ARP is vulnerable to spoofing attacks, where a malicious device can impersonate another device's MAC address.

2. **DHCP Snooping and Binding Table:**
   - DHCP Snooping is a prerequisite for DAI, as it creates a binding table that records legitimate IP to MAC address mappings.
   - This table is populated by monitoring DHCP transactions and recording the IP addresses assigned to each MAC address.

3. **Dynamic ARP Inspection Functionality:**
   - DAI validates incoming ARP packets against the DHCP Snooping binding table.
   - If an ARP packet claims an IP address that doesn't match the corresponding MAC address in the binding table, the packet is dropped.
   - This prevents ARP spoofing by ensuring that only legitimate ARP packets are allowed on the network.

4. **Configuration and Implementation:**
   - DAI is typically configured on switches and is enabled per VLAN, as each VLAN is a separate broadcast domain.
   - The configuration process involves enabling DHCP Snooping first to establish the binding table, followed by enabling DAI on the relevant switch interfaces.

5. **Handling Static IP Configurations:**
   - For devices with static IP configurations, switches can be configured to accept static entries in the binding table.
   - This ensures that legitimate static IP assignments are not blocked by DAI.

6. **Interaction with Other Security Features:**
   - DAI works in conjunction with other security features like Port Security and IP Source Guard to create a layered security approach.
   - Together, these features enhance network security by providing multiple layers of protection against various types of attacks.

### Example Scenario:

- A DHCP server assigns an IP address to a user's PC, and DHCP Snooping records this assignment in the binding table.
- When the PC sends an ARP request, the switch validates the ARP packet against the binding table.
- If a malicious device tries to send an ARP packet claiming to have the IP of the gateway with an incorrect MAC address, the switch drops the packet, preventing the attack.

### Considerations:

- **Security of the DHCP Server:**
  - It is crucial to secure the DHCP server to prevent it from being compromised and providing incorrect IP to MAC mappings.

- **Performance Implications:**
  - Modern switches efficiently handle the validation process, but in very large networks, performance should be monitored to ensure optimal operation.

### Conclusion:

Dynamic ARP Inspection is an essential security feature that leverages the binding table created by DHCP Snooping to validate ARP packets. By preventing ARP spoofing and related attacks, DAI plays a critical role in maintaining network integrity and security, particularly in enterprise environments.

![image](https://github.com/user-attachments/assets/00b8631d-c77b-4e35-9fd3-0e352285b1b7)
