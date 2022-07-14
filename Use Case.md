# Use Case
## Context
As part of the SPARTA project and the integration of security solutions in a DevSecOps pipeline, CETIC to study a case based on the operation of a platoon of connected and autonomous vehicles using RoS (Robot Operating System).

### Autonomous car and platoon 
The platoon technique is an automated highway system that allows the vehicle to communicate with each other in order to perform common and coordinated actions, such as accelerating or braking in unison. The aim of this technique is to reduce the risk of collision accidents, reduce fuel consumption by limiting air resistance and reduce traffic congestion by reducing road surface area and reducing traffic flow.
A platoon consists of a leading vehicle, followed by vehicles, followers. Each vehicle consists of sensors and sensors for decision-making. The leader’s decisions are sent to the followers who will then execute. For example, when the leading vehicle encounters an obstacle, its sensors inform it of a danger and the leading car will slow down, resulting in a slowdown of the peloton, and therefore of any car following.
![A platoon of connected vehicles](/IMAGES/platoon-of-connected-vehicles.png)  
<b> Fig.1 - A platoon of connected vehicles </b> [^1]  

The objective of this use case is to demonstrate the value of continuous deployment, integration and safety in the DevSecOps pipeline, only one vehicle will be implemented.
The creation of a complete platoon and the study of the attacks of this platoon may be part of a future work.

### Challenges
Autonomous vehicles are primarily computer systems consisting of an operating system, software and components necessary for decision-making.
These vehicles are connected both to the other vehicles of the platoon, but also to a more global management system, using not always reliable communication protocols and with security vulnerabilities.

CETIC has demonstrated, using a test bench deployed in a DevSecOps lifecycle, that exploitable threats exist and that attacks can lead to disasters if these threats are not addressed.
To counter these threats, CETIC researchers have integrated IDS, SIEM and SOAR solutions into the DevSecOps lifecycle. They were also able to demonstrate that the integration of security solutions makes it possible to put in place countermeasures to the dangers of compromises.

Despite the fact that these solutions have definite interests in countering these threats, they serve primarily to protect systems from known techniques and vulnerabilities.

It is therefore interesting to ask how to discover new faults, new techniques and vulnerabilities without it taking place in a production system and in order to prevent all disasters. The solution lies in the integration of a honeypot into the DevSecOps pipeline.

## Scenario
The attack scenario defined by CETIC describes the injection of a backdoor into a vehicle’s firewall via an update from the project repository.

![Backdoor attack scenario ](/IMAGES/Backdoorpng.png)  
<b> Fig.2 - Backdoor attack scenario </b> [^2]  

After discovering a vulnerability in the firewall, the attacker will exploit it using MSFVenom. It will inject a payload via a HelloBD file into the legitimate Debian package, IpTable. This package contains the backdoor that will connect the vehicle to the attacker using reverse shell via MetaSploit. It will then be uploaded to the repository containing the project code.
The vehicle will then update its firewall to the new version of IpTable and install the malicious binary. Once installed, the victim vehicle will connect to the attacker’s console and provide him with administrator access rights (sudo).
The attacker then has his hand on the vehicle and can control it as he pleases.

## Integration of a honeypot

The integration of security tools (IDS, SIEM, SOAR) has been carried out in previous stages. The detection and analysis steps have been implemented so that an initial response to this vulnerability is given.
Indeed, the existing response allows downgrading the firewall of the target vehicle in order to return to a reliable version.
This work consists of adding an additional layer of security by adding a honeypot imitating as much as possible the behavior of a vehicle in production. The intention is to add a response from SOAR, which will communicate with a sandbox environment to deploy dummy vehicles.

Here is a diagram representing the structure integrating a honeypot:

![Structure of the use case integrating a honeypot](/IMAGES/UseCase-stucture.png)  
<b> Fig.3 - Structure of the use case integrating a honeypot </b> [^3]  

In order to understand step by step the operation from the attack to the response, here is a sequence diagram: 

![Sequence diagram of the use case](/IMAGES/UseCase-sequence.png)  
<b> Fig.4 - Sequence diagram of the use case </b> [^3]  

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
- 10 : / 11. The SOAR retrieves the configuration from the configuration manager;
- 12 : SOAR sends the honeypot creation order to the sandbox infrastructure;
- 13 : / 14. The infected vehicle is downgraded and disconnected from the attacker;
- 15 : The Honeypot car is created and deployed;
- 16 : The Honeypot car mimics the behavior of a legitimate vehicle and connects to the attacker via the reverse Shell;
- 17 : The attacker launches a series of attacks (for example reconnaissance);
- 18 : / 19. Events and artifacts (network traffic and payload) are collected and sent to IDS and SIEM.

## Functional specification

In order to determine a solution that can be integrated into the DevSecOps pipeline and with features specific to edge computing and in this case meeting the requirements of the use case, we have determined selection criteria.
Existing solutions will then be confronted with these criteria in order to determine which is most appropriate.

From a functional point of view, the honeypot must be able to:
* Capture the commands typed by the attacker
* Record and/or transmit collected data
* Interfacing with SIEM
* Interfacing with SOAR

From a non-functional perspective, honeypot must:
* Be in open source licenses
* Have a vibrant community
* Be easy to install and take in hand
* Provide documentation
* Meet these characteristics as a minimum:
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


# References 
[^1]: R. Passerone et al., "A Methodology for the Design of Safety-Compliant and Secure Communication of Autonomous Vehicles," in IEEE Access, vol. 7, pp. 125022-125037, 2019, doi: 10.1109/ACCESS.2019.2937453.
[^2]: G.Ginis (2021). https://github.com/cetic/devsecops/blob/master/IDS-SIEM/IDS.md
[^3]: Use Case Diagrams by Abdel-Malek Bouhou. honeypot\IMAGES\UseCase-Diagrams.drawio