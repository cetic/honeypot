# State of the art : Honeypots
## Definition
The Honeypot is by vocation, a more or less artificial information system whose main purpose is to be probed, attacked and possibly compromised. When two or more honeypots are deployed in the same environment, they form a honeynet [^2]. Honeypots are used to lure attackers into believing they have access to real systems. They can be integrated with intrusion detection systems (IDS) and firewalls to form an intrusion protection system (IPS) [^3]. This is created to capture and use all information on Hackers to study their methods, their motivations and the attack techniques they use to break into or corrupt a system. The goal is to develop ways to improve system security and prevent attacks in the future. 

-> Talk about BLUE TEAM ! 

![Basic Honeypot Exemple](/IMAGES/honeypot-basic-diagram.png)

## Characteristics of honeypots 
The honeypots can be classied by means of different orthogonal features [^1]. 
In order to represent and understand the different characteristics of honeypots, a concrete example is used throughout this section. The example honeypot represents a used water central processing unit.

![Honeypot Characteristics](/IMAGES/Honeypot-Characteristics.drawio.png)

### Interaction Level
The interaction level of the honeypot indicates to what extent its functionality is exposed. Two values are used to define it [^3]:  
* Low-interaction : honeypot have low level of realism. The interaction between the Hacker and the system is short and limited. It is generally not a system per se, but rather an emulation of operating systems and services. This type of Honeypot  can simulate only specific systems services and uses basic techniques like identifying port scans [^6], generating attack signatures, analyzing trends and collecting malware informations. 
* High-interaction : honeypot provide the most realistic environment for the attackers because it use real services running on real operating systems.  
* Hybride : A pot of honey offering a mix between low and high ineraction.

In the case of the example, the low-interaction honeypot presents only a few possibilities of interaction, such as for example access to PLCs capable, in this case, only of giving status information. While the high-interaction, will allow to be able to interact with these PLCs and that the modifications made have an immediate impact on one of the other components of the honeypots, such as the monitoring and alert system. In the case of a hybrid, one could imagine a mixture between certain PLCs supposed to interact and others providing only a certain amount of defined information.

### Ressource level
The resource level used by the honeypot is determined by the replication realism of the system. There are three possibilities: 
* Real / Physique : is a replication of a target system.
* Virtual : use virtualization technology to reproduce a system. This solution is low-cost.
* Hybrid : include a mixture of real and virtual device. This solution is coste effective  

To better understand, let's take the example of the central. "Physical" would be a carbon copy of a processing central in production. Requiring an identical infrastructure at all levels. If the real central uses 20 PLCs, the honeypot will use 20 real PLCs. The virtual honeypot is a virtual copy of the central. Hosted on a machine capable of virtualizing the layers and services of each component. Virtualization makes it possible to create the 20 PLCs in such a way that they perfectly imitate the behavior of the real components of the central. In the case of hybrid, one could quite imagine that the network infrastructure is completely virtualized, but that the PLCs are real physical components.

### Communication interfaces
The communication interface is the characteristic that defines how the honeypot will be reached and through which interface one will be able to interact with it [^1]: 
* Network interface: the honeypot communicates directly through a network interface 
* Non-network hardware interface: the honeypot interfaces with hardware interfaces other than networks (PLC, USB, etc.) 
* API : the honeypot communicates via a software API  

There are a multitude of possibilities for implementing honeypots in a wastewater treatment plant. If it is decided to add a honeypot at the network level (a server, a switch, etc.) in a real central, and only at this location, the honeypot only has a "Network interface" as a communication interface. , because it is via this interface that hackers will communicate with. If it is a PLC or a sensor using the RS232 protocol, etc. then the communication interface of the honeypot is a "Non-network hardware interface". Finally, suppose that the honeypot is an API that is used by a real logging server and that it is allowed to return fictitious information, then we are in the case of an "API" interface

### Multi-tier architecture 
Honeypot can behave in 2 different ways when it comes to its interaction [^7]: 
* Server: honeypot acts as a server and passively waits for client requests 
* Client: honeypot acts as a client and actively initiates requests to servers  

Let's take the example of a honeypot representing a machine capable of performing orchestration tasks. In the central, 2 possibilities exist, the first is the client honeypot connects to servers in order to retrieve its tasks for the day. It will then execute a series of commands and retrieve information which will be analyzed in order to verify that none of these commands is illegal. The second is the reverse role, namely the honeypot server, which will provide tasks to its clients. It will also collect information that will be analyzed to verify that no client is trying to execute illegal commands and access unauthorized information.

### Distribution (Appearance?)
The appearance of the honeypot is that it appears to be, or is, composed of a single system, or if it appears to be, or is composed of several independent systems:
* Distributed : honeypot is or appears to be composed of multiple systems 
* Stand-Alone : honeypot is or appears to be a system, even if it is composed of several systems but appears to be only one 

* MESH : -> 
* Centralized : 



### Containment
The containment strategy defines the ability of a honeypot to defend itself against attacks, other malicious activities spreading from it. A honeypot can use several of these strategies [^1]:
* Block : attacker is identified and blocked, he never reaches his target
* Defuse : attacker reaches his target, but his attacks are defused; he is manipulated way to fail 
* Slow down : attacker is slowed down throughout his attacking process, the goal being to discourage him 
* None : no action is taken to prevent the attacker (Profiling?)   

To illustrate this characteristic, one can imagine that a hacker has entered a control sub-network of the wastewater treatment plant and tries to modify the position of a valve. From this observation, several reaction strategies are possible. In the case of a "Block", one can imagine that as soon as the honeypot has detected and identified the hacker, it is automatically black listed and the connection is interrupted.
In the case of a "Defuse", the hacker has already achieved his goal and the command to modify the position of the valve has been sent. From this moment, the honeypot is able to detect unauthorized activity and the attack is defused.
In the case of a "Slow down", everything is done to slow it down and discourage it. When he thinks he has sent the command to modify the position of the valve, his identity is verified and he is faced with a new pitfall.
Finally, if we decide that the honeypot of our central is intended to study the behavior of the hacker, we can decide to let it act with complete impunity and study its methodology. Then, it can be decided not to apply any containment strategy ("None").  

### Data capturing 
This characteristic does not directly concern the technical aspects, but rather its ability to capture types of data [^1]: 
* Event : an event has occurred -> Status change .
* Attacks : collects activities threatening the security policy.
* Intrusions : collects policy-threatening activities that lead to a security breach.
* None : no data collection.  

Returning to the example case, if there is an unexpected event capable of being detected by the honeypot, such as the unwanted opening of a valve, then it will receive the "Event" data capture characteristic. . If, on the other hand, the honeypot is able to capture the unsuccessful attempts of a hacker trying to modify the position of the valve, then it will receive the "Attack" data capture characteristic. If the honeypot can capture the events produced by an attack resulting in an intrusion, then it will be decorated with the "intrusions" feature. Finally, if the honeypot is not intended to capture information, as is the case for a decoy intended to imprison hackers to prevent them from acting. They can be assigned the characteristic of "None".

### Detection
Several mechanisms can be used by the honeypot for the analysis: 
* Abuse: Data is analyzed and associated with a large database.
* Anomaly: The networks are analyzed and anomalies are identified. It can be related to traffic load, packets and protocols.  

To give a concrete example of a detection mechanism, one can imagine the implementation of a SCADA within the honeypot of the plant. In the case of an "Abuse", the communication network data is processed and compared in real time by the SCADA which will compare it to an attack signature database and detect if there is a match. In the case of an "Anomaly", The honeypot uses an IDS, which filters the packets circulating on the communication networks and is able to identify the anomalies.

### Scalability:
Scalability determines the ability of a honeypot to evolve. By this we mean its ability to be modified in order to increase the number of decoys and services it offers [^3]:
* Scalable: can increase the number of services and lures offered
* Not Scalable: Only has a set number of services and cannot be changed at that level.  

Let's take the example of the PLCs present in the structure of the wastewater treatment plant. If PLCs can easily be added, then it is considered scalable. On the other hand, if it is impossible to add more, then it is considered non-scalable.

### Context 
This characteristic is used to define in which context the honeypot is used and what is the purpose of its implementation [^3]:
* Research : is used to lure attackers and study their behaviours and the tools they use to develop better protection against these attacks.
* Production : is used to defend and prevent attack on real systems and to protect it.  

To illustrate this characteristic, we can see the central processing unit as being a virtual high interaction honeypot identically imitating the behavior of a real central unit. Its deployment can be carried out in the context of research, we want to highlight the flaws that may exist on an existing system and know how to protect ourselves from attackers. In the case of a production, its goal is above all to protect the real system and we do not necessarily seek to collect data for study purposes, but rather to divert the attention of the attacker.

## Strength and weakness of characteristics

|  Characteristic   | Strength                                                          | Weakness                                          |
|-------------------|---------------------------------------------------------------    |---------------------------------------------------|
| Low-Interaction   | - Low resource Consumption \\ - Limited risk of compromise        | - Easily detectable \\ - Simulation limit         |
| High-Interaction  | - Easy to implement \\ - High rate of realism                     | - High risk of comprimise if poorly protected \\ lower scalability due to their complexity  |
|-------------------|---------------------------------------------------------------    |---------------------------------------------------|
| Real / Physique   | - Perfectly mimics the behavior of a real system                  | - Cost relative to the reproduced system          |
| Virtual           | - Low implementation cost \\ - Easily deployable                  | - May lack realism                                |
| Hybrid            | - Overall cost effective \\ - Meets the need                      |                                                   |
|-------------------|---------------------------------------------------------------    |---------------------------------------------------|
| Distributed       |                                                                   |                                                   |
| Stand-Alone       |                                                                   |                                                   |
|-------------------|---------------------------------------------------------------    |---------------------------------------------------|
| Block             |                                                                   |                                                   |
| Defuse            |                                                                   |                                                   |
| Slow down         |                                                                   |                                                   |
| None              |                                                                   |                                                   |
|-------------------|---------------------------------------------------------------    |---------------------------------------------------|
| Event             |                                                                   |                                                   |
| Attacks           |                                                                   |                                                   |
| Intrusions        |                                                                   |                                                   |
| None              |                                                                   |                                                   |
|-------------------|---------------------------------------------------------------    |---------------------------------------------------|
| Abuse             |                                                                   |                                                   |
| Anomaly-Alone     |                                                                   |                                                   |
|-------------------|---------------------------------------------------------------    |---------------------------------------------------|
| Research          |                                                                   |                                                   |
| Production        |                                                                   |                                                   |



## Measures of Effectiveness


## Honeynet 
The capabilities of a single honeypot are limited to its characteristics. Today, many honeypot systems focus on combining different types of honeypot to achieve an optimized solution. 
A honeynet is an extension of the honeypot concept respecting a certain topology. 

In his article, Wenjun's Fan [^2] proposes a honey network taxonomy that facilitates their classification and study. 
It is composed of 3 main features:
Data control: Set of measures aimed at reducing the risk that a honeypot will be compromised and used to attack other systems. Outbound attacks must be controlled to protect non-honeypot systems

Data capture: Its purpose is to capture and record and collect the activities of attackers in order to be exploited later. 3 critical data capture layers have been identified:
* The layer related to incoming and outgoing connections stored in the firewall logs.
* The traffic analysis layer, which checks packets and their payloads as they enter and leave the honeynet.
* The layer related to activity on the system (system calls, modified files, attacker's keystroke, etc).

Data collection: Means necessary and used to guarantee the safe transfer of data collected by honeypots to a centralized point 


## Type of attacks 

### Mitre 
MITRE is an American non-profit organization whose objective is to work for the public interest. His fields of intervention are systems engineering, information technology, operational concepts, and business modernization. Their slogan is that they solve problems for a safer world.  
MITRE has become a reference in terms of sharing information around cybercrime and its 2 essential platforms are MITRE ATT&CK® and MITRE CVE.  
MITRE ATT&CK® [^8]is an open and freely accessible reference knowledge base, known in the world of computer security, as it provides a list of tactics and techniques used by cybercriminals. It describes the adversary behaviors specific to the different environments (Windows, Linux, Mac, cloud, mobiles, etc.). Organizations tap into this knowledge base to develop offensive and defensive measures to strengthen their security. ATT&CK® can help cyber defense managers better understand attacker behavior and assess risk to a society by classifying attacks. There is even a knowledge base dedicated to Industrial Control Systems, ATT&CK® ICS [^10].    

MITRE CVE [^9] is a public dictionary that records all vulnerabilities and security flaws that have been discovered. CVE identifiers are notably used by IDSs and IPSs.

The use of these 2 sources of information by a honeypot can be interesting insofar as they provide interesting techniques to feed the attacker's killchain. 
TODO->

*Usage of Mitre (Honeypot dapted to certain threats) ? 


###  Lockheed-Martin Killchain
*confront MITRE

## Honeypot solutions referances
reference in terms of honeypot in the private and open-source market

### Paid Honeypots solution -> 
 : 

### Open-Source Honeypots solution -> 
 : +definition of characteristics specific to a use-case





# Honeypot and DevSecOps 

## DevSecOps 

## Criteria for selecting a honeypot






## Concepts

* honeyfarm
* honey-patching
* honey-trapping

## Glossary 
* IoT : Internet of Things  
* IIoT : Industrial Internet of Things  
* CPS : Cyber-physical system - Cyber-physical system: Computing environment composed of deeply intertwined physical and software elements. Networks of devices composed of: sensor, actuator, PLC, RTU, IED, Monitoring, ICS, etc.  
* PLC : Programmable Logic Controllers - Programmable digital electronic device for controlling industrial processes by sequential processing. Exemple : Input cards for connecting sensors, push buttons, actuators, indicators, valves, etc.  
* RTU : Remote Terminal Units - Electronic device controlled by microprocessor which connects the objects of the physical world to a distributed control system or to a SCADA  
* ICS : Industrial Control Systems is a Control systems and associated instrumentation, which include the devices, systems, networks, and controls used to operate and/or automate industrial processes.  Exemple : Smart Grid and other smart infrastructures : water, gas, building automation, medical devices, smart cars, etc.  
* System : Set of elements that make up a pot of honey. A system may consist of several subsystems determining the intrinsic characteristics of the honyepot.
* CVE : Common Vulnerabilities and Exposures

## References
* [^1] Seifert, C., Welch, I., & Komisarczuk, P. (2006). Taxonomy of honeypots. http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.61.5339
* [^2] Fan, W., Du, Z., & Fernández, D. (2015, November). Taxonomy of honeynet solutions. In 2015 SAI Intelligent Systems Conference (IntelliSys) (pp. 1002-1009). IEEE. https://ieeexplore.ieee.org/abstract/document/7361266/
* [^3] Franco, J., Aris, A., Canberk, B., & Uluagac, A. S. (2021). A survey of honeypots and honeynets for internet of things, industrial internet of things, and cyber-physical systems. IEEE Communications Surveys & Tutorials, 23(4), 2351-2383. https://ieeexplore.ieee.org/abstract/document/9520645/
* [^4] Antonioli, Daniele & Agrawal, Anand & Tippenhauer, Nils Ole. (2016). Towards High-Interaction Virtual ICS Honeypots-in-a-Box. 13-22. 10.1145/2994487.2994493. https://dl.acm.org/doi/abs/10.1145/2994487.2994493 
* [^5] Mairh, Abhishek and Barik, Debabrat and Verma, Kanchan and Jena, Debasish. (2011). Honeypot in Network Security: A Survey. https://dl.acm.org/doi/10.1145/1947940.1948065
* [^6] Ahn, Seonggwan, Thummin Lee, and Keecheon Kim. "A study on improving security of ICS through honeypot and ARP spoofing." (2019) International Conference on Information and Communication Technology Convergence (ICTC). IEEE, https://ieeexplore.ieee.org/abstract/document/8939925/
* [^7] Mohammadzadeh, H., Mansoori, M., & Honarbakhsh, R. "Taxonomy of Hybrid Honeypots". (2011). https://www.semanticscholar.org/paper/Taxonomy-of-Hybrid-Honeypots-Mohammadzadeh-Mansoori/711bf1e19078df842f6388869388e9c128cf1024
[^8] MITRE ATT&CK® https://attack.mitre.org/
[^9] MITRE ATT&CK® for ICS https://collaborate.mitre.org/attackics/index.php/Main_Page
[^10] MITRE CVE (Common Vulnerabilities and Exposures) https://cve.mitre.org/