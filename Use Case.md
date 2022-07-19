# Use Case
## Context
As part of the SPARTA [^4] project and the integration of security solutions into a DevSecOps pipeline, CETIC worked on a case based on the operation of a platoon of connected and autonomous vehicles using RoS (Robot Operating System )[^5].

The objective of this use case is to demonstrate the value of integrating a honeypot solution into an Edge Computing environment while promoting the value of continuous deployment, integration and security in the DevSecOps pipeline.

### Challenges
Autonomous vehicles are primarily computer systems consisting of an operating system, software and components necessary for decision-making[^6].
These vehicles are connected both to the other vehicles of the platoon, but also to a more global management system, using not always reliable communication protocols and with security vulnerabilities.

CETIC has demonstrated, using a test bench deployed in a DevSecOps lifecycle, that exploitable threats exist and that attacks can lead to disasters if these threats are not addressed.
To counter these threats, CETIC researchers have integrated IDS, SIEM and SOAR solutions into the DevSecOps lifecycle. They were also able to demonstrate that the integration of security solutions makes it possible to put in place countermeasures to the dangers of compromises.

Despite the fact that these security solutions have undeniable interests in countering these threats, they serve primarily to protect systems from known techniques and vulnerabilities.

It is therefore interesting to ask how to discover new security flaws, techniques and vulnerabilities without this taking place in a system in production and in order to limit the risks related to computer systems and cybersecurity. The solution lies in integrating a honeypot into the DevSecOps pipeline.

## Scenario
The attack scenario defined by CETIC describes the injection of a backdoor into a vehicle’s firewall via an update from the project repository.

![Backdoor attack scenario ](/IMAGES/Backdoorpng.png)  
<b> Fig.2 - Backdoor attack scenario </b> [^2]  

After discovering a vulnerability in the firewall, the attacker will exploit it using MSFVenom[^7]. It will inject a payload via a HelloBD[^8] file into the legitimate Debian package, iptables[^9]. This package contains the backdoor that will connect the vehicle to the attacker using reverse shell via MetaSploit[^10]. It will then be uploaded to the repository containing the firewall package.
The vehicle will then update its firewall to the new version of IpTable and install the malicious binary. Once installed, the victim vehicle will connect to the attacker’s console and provide him with administrator access rights (sudo).
The attacker then has his hand on the vehicle and can control it as he pleases.

![Backdoor attack demonstration with MetaSploit ](/IMAGES/MetaSploit.png)  
<b> Fig.3 - Backdoor attack demonstration with MetaSploit </b> [^11]  

## Integration of a honeypot

The integration of security tools (IDS, SIEM, SOAR) has been carried out in previous internships [^2] [^12]. The detection and analysis steps have been implemented so that an initial response to this vulnerability is given.
Indeed, the existing response allows downgrading the firewall of the target vehicle in order to return to a reliable version.
This work consists of adding an additional layer of security by adding a honeypot imitating as much as possible the behavior of a vehicle in production. The intention is to add a response from SOAR, which will communicate with a sandbox environment to deploy dummy vehicles.

Here is a diagram representing the structure integrating a honeypot:

![Structure of the use case integrating a honeypot](/IMAGES/UseCase-stucture.png)  
<b> Fig.4 - Structure of the use case integrating a honeypot </b> [^3]  

In order to understand step by step the operation from the attack to the response, here is a sequence diagram: 

![Sequence diagram of the use case](/IMAGES/UseCase-sequence.png)  
<b> Fig.5 - Sequence diagram of the use case </b> [^3]  

The steps shown in this diagram are:
- 1 : The attacker injects a backdoor into the application repository by modifying IpTable;
- 2 : The repository informs the legitimate car that an update is available;
- 3 : The legitimate vehicle downloads the new update containing the payload and backdoor;
- 4 : The IDS analyses the traffic of the legitimate vehicle;
- 5 : The legitimate vehicle connects to the attacker via Reverse Shell;
- 6 : The attacker launches a series of attacks;
- 7 : The IDS detects an event and sends it to SIEM;
- 8 : SIEM analyzes events and detects an anomaly;
- 9 : SIEM sends an alert to SOAR to address the vulnerability;
- 10 / 11 : The SOAR retrieves the configuration from the configuration manager;
- 12 : SOAR sends the honeypot creation order to the sandbox infrastructure;
- 13 / 14 : The infected vehicle is downgraded and disconnected from the attacker. The autonomous vehicle is quarantined ;
- 15 : The Honeypot car is created and deployed;
- 16 : The Honeypot car mimics the behavior of a legitimate vehicle and connects to the attacker via the reverse Shell;
- 17 : The attacker launches a series of attacks (for example reconnaissance);
- 18 / 19 / 20 :. Events and artifacts (network traffic and payload) are collected and sent to SIEM to bring to light new security flaws, techniques and vulnerabilities.

## Functional specification

In order to determine a solution that can be integrated into the DevSecOps pipeline and with features specific to edge computing and in this case meeting the requirements of the use case, selection criteria have been defined.
The existing solutions will then be compared to these criteria in order to determine which is the most appropriate.

From a functional point of view, the honeypot must be able to:
* Capture the commands typed by the attacker
* Record and/or transmit collected data
* Interfacing with SIEM
* Interfacing with SOAR

From a non-functional perspective, honeypot must:
* Provide an open source license
* Have a vibrant community
* Be easy to install and take in hand
* Provide documentation
* Meet these characteristics [^13] as a minimum:
    * Interaction Level: High/Medium Interaction
    * Resource level: Hybrid
    * Communication interface: Reverse shell
    * Multi-tier architecture: Server & Client
    * Topology: N/A
    * Containment: None
    * Data Capture: None
    * Scalability: Scalable
    * Context: Research & Protection


## Technical specification

## Implementation in a PoC

# Glossary
* Reverse shell : Computer technique that allows attackers to open ports to target machines, forcing communication and allowing complete control of the target machine.

# References 
[^1]: R. Passerone et al., "A Methodology for the Design of Safety-Compliant and Secure Communication of Autonomous Vehicles," in IEEE Access, vol. 7, pp. 125022-125037, 2019, doi: 10.1109/ACCESS.2019.2937453.  
[^2]: H. Amraoui IDS and SIEM - Intrusion detection system and Security Information and Event Management (2021).  https://github.com/cetic/devsecops/blob/master/IDS-SIEM 
[^3]: Use Case Diagrams by Abdel-Malek Bouhou. honeypot\IMAGES\UseCase-Diagrams.drawio  
[^4]: S. Dupont. SPARTA - CAPE program - D5.1: Assessment specifications and roadmap. (2019). https://www.sparta.eu/assets/deliverables/SPARTA-D5.1-Assessment-specifications-and-roadmap-PU-M12.pdf  
[^5]: ROS - Robot Operating System. https://www.ros.org/  
[^6]: Jo, K., Kim, J., Kim, D., Jang, C., & Sunwoo, M. (2014). Development of Autonomous Car—Part I: Distributed System Architecture and Development Process. IEEE Transactions on Industrial Electronics, 61(12), 7131–7140. doi:10.1109/tie.2014.2321342 
[^7]: "MSFvenom is a combination of Msfpayload and Msfencode" https://www.offensive-security.com/metasploit-unleashed/msfvenom/
[^8]: "NoSQL backend solution" http://hellodb.ai/
[^9]: "free Linux userspace software through which the system administrator can configure chains and rules in the kernel space firewall" https://fr.wikipedia.org/wiki/Iptables
[^10]: "Penetration testing framework" https://www.metasploit.com/
[^11]: S.Dupont, G. Ginis, P. Massonet. "Securing platoon firewall updates" CETIC.be / sparta.eu
[^12]: H.Benchrifa - SOAR https://github.com/cetic/devsecops/blob/master/SOAR/Operate.md
[^13]: A-M. Bouhou. Honeypot - State Of Art - Characteristics of honeypots. honeypot\State Ot Art.md