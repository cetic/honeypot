# State of the art : Honeypots

## Definition 
In the information technology world, attacks are constant and devices connected to the Internet are constantly scanned by hackers. Their goals are to find valuable data, critical applications and vulnerabilities in network infrastructures. The honeypot is by vocation, an information system, more or less artificial, whose main purpose is to be probed, attacked and possibly compromised in order to make a hacker believe that he has penetrated into the real network of the organization. Thanks to the honeypot, the hacker is removed from the real network and his activities and movements can be captured and monitored. The information collected on the hackers makes it possible to study their methods, their motivations and the attack techniques they use to penetrate or corrupt a system. The goal is to develop ways to improve system security and prevent attacks in the future.

The location of the honeypot largely depends on its sophistication, the traffic it aims to attract, and its proximity to sensitive resources within the organization's network. It can be placed inside the DMZ in the middle of the services (web, mail, ...) intended for the public (internet), on decoy servers. It can also be placed outside the external firewall to detect attempts to enter the internal network. Nevertheless, it will always be better to isolate it from the production environment.

There are several advantages of using a honeypot. The first is that it allows collecting data from real attacks, allowing to provide rich information to the cyber security manager. Then, it also helps to discover new attack patterns and new vulnerabilities in order to define countermeasure strategies. An interesting aspect is that it reduces the volume of false positives from alert systems, since no ordinary users are supposed to connect to them. We can also mention the fact that setting up a honeypot can be quite inexpensive in terms of investment and performance. Nevertheless, some complex systems require specific skills, which can reverse the trend of low implementation cost.

There are also some risks associated with implementing a honeypot that need to be considered. To function properly and produce information, the honeypot must be attacked. It is therefore limited to the analysis of the data collected and dependent on the attacks carried out on it. For the system to be attacked, it must be attractive to hackers. If they are experienced, they can easily recognize that they have a honeypot in front of them and therefore that they are not in the presence of a legitimate system.

Finally, the biggest risk is the compromise of the honeypot. If the attacker manages to take control of the honeypot, he can use it to his advantage and provide bad information to the administrator in order to divert his attention from the real objective. He can also use it to perform other attacks or to create his own honeypot. The experienced hacker could even use the honeypot as an entry point to the real system if a connection exists between the two (Logs, synchro, ...).

In order to prevent the hacker from discovering the deception, the honeypot must be functionally an easy target, but not be perceived as such.

A few clues allow a hacker to identify that he is communicating with a honeypot [^11]:
- The system has all its network ports open.
- The system has unusual ports open (systems connected to the Internet usually only have basic services available).
- The system is a site or a server that is too easy to hack.
- The system consists of directories with extremely literal names indicating something of value, like "social security numbers" or "credit card data".
- The system has very little software installed.
- The system has a lot of free space on the hard disk, which indicates that it is not a well-used production disk.

![Basic Honeypot Exemple](/IMAGES/honeypot-basic-diagram.png)

## Characteristics of honeypots 
The honeypots can be classied by means of different orthogonal features [^1]. 
In order to represent and understand the different characteristics of honeypots, a concrete example is used throughout this section. The example honeypot represents a wastewater treatment plant.

(TODO--> ADD Schem of wastewater treatment plant)

### Interaction Level
The interaction level of the honeypot indicates to what extent its functionality is exposed. Two values are used to define it [^3]:  
* Low-interaction : honeypot have low level of realism. The interaction between the Hacker and the system is short and limited. It is generally not a system per se, but rather an emulation of operating systems and services. This type of Honeypot  can simulate only specific systems services and uses basic techniques like identifying port scans [^6], generating attack signatures, analyzing trends and collecting malware informations. Low-interaction honeypots are particularly useful for monitoring less complex attacks, such as robots and malwares.
* High-interaction : honeypot provide the most realistic environment for the attackers because it use a variety of real services running on real operating systems. It imposes few restrictions inside the system, encouraging attackers to interact with it. High-interaction honeypots provide are often able to capture detailed information, making them better for monitoring more experienced hackers, as they look realistic and are likely to deceive them. This feature carries risks since it allows the attacker to point to root access, which constitutes a threat of hijacking.
* Hybride : A pot of honey offering a mix between low and high ineraction.

In the case of the example, the low-interaction honeypot presents only a few possibilities of interaction, such as for example access to PLCs capable, in this case, only of giving status information. While the high-interaction, will allow to be able to interact with these PLCs and that the modifications made have an immediate impact on one of the other components of the honeypots, such as the monitoring and alert system. In the case of a hybrid, one could imagine a mixture between certain PLCs supposed to interact and others providing only a certain amount of defined information.

### Ressource level
The resource level used by the honeypot is determined by the replication realism of the system. There are three possibilities: 
* Real / Physique : is a replication of a target system.
* Virtual : use virtualization technology to reproduce a system. This solution is low-cost.
* Hybrid : include a mixture of real and virtual device. This solution is coste effective  

To better understand, let's take the example of the wastewater treatment plant. "Physical" would be a carbon copy of a processing wastewater plant in production. Requiring an identical infrastructure at all levels. If the real wastewater plant uses 20 PLCs, the honeypot will use 20 real PLCs. The virtual honeypot is a virtual copy of the wastewater plant. Hosted on a machine capable of virtualizing the layers and services of each component. Virtualization makes it possible to create the 20 PLCs in such a way that they perfectly imitate the behavior of the real components of the wastewater plant. In the case of hybrid, one could quite imagine that the network infrastructure is completely virtualized, but that the PLCs are real physical components.

### Communication interfaces
The communication interface is the characteristic that defines how the honeypot will be reached and through which interface one will be able to interact with it [^1]: 
* Network interface: the honeypot communicates directly through a network interface 
* Non-network hardware interface: the honeypot interfaces with hardware interfaces other than networks (PLC, USB, etc.) 
* API : the honeypot communicates via a software API  

There are a multitude of possibilities for implementing honeypots in a wastewater treatment plant. If it is decided to add a honeypot at the network level (a server, a switch, etc.) in a real wastewater treatment plant, and only at this location, the honeypot only has a "Network interface" as a communication interface. , because it is via this interface that hackers will communicate with. If it is a PLC or a sensor using the RS232 protocol, etc. then the communication interface of the honeypot is a "Non-network hardware interface". Finally, suppose that the honeypot is an API that is used by a real logging server and that it is allowed to return fictitious information, then we are in the case of an "API" interface

### Multi-tier architecture 
Honeypot can behave in 2 different ways when it comes to its interaction [^7]: 
* Server: honeypot acts as a server and passively waits for client requests 
* Client: honeypot acts as a client and actively initiates requests to servers  

Let's take the example of a honeypot representing a machine capable of performing orchestration tasks. In the wastewater treatment plant, 2 possibilities exist, the first is the client honeypot connects to servers in order to retrieve its tasks for the day. It will then execute a series of commands and retrieve information which will be analyzed in order to verify that none of these commands is illegal. The second is the reverse role, namely the honeypot server, which will provide tasks to its clients. It will also collect information that will be analyzed to verify that no client is trying to execute illegal commands and access unauthorized information.

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
Finally, if we decide that the honeypot of our wastewater treatment plant is intended to study the behavior of the hacker, we can decide to let it act with complete impunity and study its methodology. Then, it can be decided not to apply any containment strategy ("None").  

### Observability
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

To illustrate this characteristic, we can see the wastewater treatment plant processing unit as being a virtual high interaction honeypot identically imitating the behavior of a real central unit. Its deployment can be carried out in the context of research, we want to highlight the flaws that may exist on an existing system and know how to protect ourselves from attackers. In the case of a production, its goal is above all to protect the real system and we do not necessarily seek to collect data for study purposes, but rather to divert the attention of the attacker.

![Honeypot Characteristics](/IMAGES/Honeypot-Characteristics.drawio.png)

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

### Open-Source Honeypots solution -> 

https://github.com/aau-network-security/riotpot
https://github.com/paralax/awesome-honeypots
https://github.com/telekom-security/tpotce

 : +definition of characteristics specific to a use-case -
* SSH honeypots : 
    - Kippo : https://github.com/desaster/kippo : 
    This SSH honeypot written in Python has been designed to detect and log brute force attacks and, most importantly, the complete shell history performed by the attacker. It’s available for most modern Linux distros, and offers both cli-command management and configuration, as well as web-based interface. Kippo offers a fake file system and the ability to offer fake content to attackers (such as user password files, etc.), as well as a powerful statistics system called Kippo Graph.
    - Cowrite : https://github.com/micheloosterhof/cowrie-dev
    This medium interaction SSH honeypot works by emulating a shell. It offers a fake file system based on Debian 5.0, letting you add and remove files as you wish. This application also saves all the downloaded and uploaded files in a secure and quarantined area, so you can perform later analysis if needed. Apart from the SSH emulated shell, it can be used as an SSH and Telnet proxy, and allows you to forward SMTP connections to another SMTP honeypot.

* HTTP honeypots 
    - Glastopf : https://github.com/mushorg/glastopf
    This HTTP-based honeypot lets you detect web-application attacks effectively. Written in Python, Glastopf can emulate several types of vulnerabilities, including local and remote file insertion as well as SQL Injection (SQLi) and using a centralized logging system with HPFeeds.
    - Nodepot : https://github.com/schmalle/Nodepot
    This web-app honeypot is focused on Node.js, and even lets you run it in limited hardware such as Raspberry Pi / Cubietruck. If you’re running a Node.js app and are lookingto get valuable information about incoming attacks and discover how vulnerable you are, then this is one of the most relevant honeypots for you. Available on most modern Linux distros, running it depends on only a few requirements.
    -Google Hack Honeypot : http://ghh.sourceforge.net/   
    Commonly known as GHH, this honeypot emulates a vulnerable web app that can be indexed by web crawlers but remains hidden from direct browser requests. The transparent link used for this purpose reduces false positives and prevents the honeypot from being detected. This lets you test your app against ever-so-popular Google dorks. GHH offers an easy configuration file, as well some nice logging capabilities for getting critical attacker information such as IP, user agent and other header details.  

* IOT honeypots : 
    - HoneyThing : https://github.com/omererdem/honeything  
    Created for the Internet of TR-069 enabled services, this honeypot works by acting as a full modem/router running the RomPager web server and supports TR-069 (CWMP) protocol. This IOT honeypot is capable of emulating popular vulnerabilities for Rom-0, Misfortune Cookie, RomPager and more. It offers support for TR-069 protocol, including most of its popular CPE commands such as GetRPCMethods, Get/Set parameter values, Download, etc. Unlike others, this honeypot offers an easy and polished web-based interface. Finally, all the critical data is logged in a file called honeything.log  
    - kako : https://github.com/darkarnium/kako  
    The default config will run a number of service simulations in order to capture attacking information from all incoming requests, including the full body. It includes Telnet, HTTP and HTTPS servers. Kako requires the following Python packages to work properly: Click, Boto3, Requests and Cerberus. Once you’re covered with the required packages, you can configure this IOT honeypot by using a simple YAML file called kako.yaml. All the data is recorded and is exported into AWS SNS, and flat-file JSON format.    



# Honeypot and DevSecOps 

## DevSecOps 

## Criteria for selecting a honeypot
### Definition of a strategy:
- What vulnerabilities (Expose a list of credentials, expose a service with low credentials, expose an MQTT vulnerability, ...)
- What types of attacks to cover ?
- What events to monitor (connection attempts, file modifications, ...)?
- Define a location ?
- Define services and applications (MQTT) ?
- Define decoy data (interesting for the hacker) ?
- Define the desired characteristics of the honeypot ?
- Define the rules of the FW (so as to direct the hacker to the network where the honeypot is and not the internal network)?
- Set logging strategy (out of attacker's reach, so they don't compromise log files -> Stix and Taxii )?
- Define the response strategy?
- Define the test strategy:
    - Use port scanners and penetration tools (Be careful that the IDS is not an obstacle that could scare hackers away)?
    - Create monitored activities/events
    - Check logging

### Implementation steps:
- Choose a honeypot
- Prepare the infrastructure (network? FW? VM? ...)
- Installation (Certain measures should be taken to avoid unintentional exposure:
    - Use dedicated honeypot credentials (different from production servers)
    - Use decoy data (never real data)
    - Isolate the honeypot from the private network and production systems)
- Configure firewall rules and logging defined in policy
- Configure the honeypot according to the strategy (port, service, application, vulnerabilities, link with logging ...)
- Test the honeypot
- Going live






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
[^11] Ben Lutkevich. (2021). "How to build a honeypot to increase network security"https://www.techtarget.com/searchsecurity/definition/honey-pot