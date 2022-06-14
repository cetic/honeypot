# State of the art : Honeypots

## Definition 
In common language, the "honeypot" in the figurative sense of the term, designates a tool used to attract wasps thanks to the smell of honey placed at the bottom of the pot. When the wasp enters it, its legs remain stuck to the honey and the insect is then trapped.
In the IT sense of the term, we must turn to Lance Spitzner [^18] who defines the honeypot as follows: *"A honeypot is an information system resource whose value lies in the unauthorized or illicit use of this resource"*.
This very general definition induces the notions of bait, lure and surveillance of intruders. 

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

![Basic Honeypot Example](/IMAGES/honeypot-basic-diagram.png)  
<b> Fig.1 - Basic diagram of an environment using honeypots </b> [^20]  

This figure (Fig.1) shows the extent to which IOT and production environments coexist with honeypots. On the one hand, "IOT"-type connected objects, which are found in everyday life and which are required to make life easier for users. On the other hand, the production environments of companies which allow their legitimate users to connect from the Internet in order to reach corporate resources.
By trying to access any potentially exploitable resource, attackers will also find themselves faced with honeypots.
These honeypots, depending on their characteristics, will adopt behaviors to study attackers' strategies, highlight vulnerabilities and protect legitimate systems.
By honeypot we mean a system capable of reproducing or simulating the behavior of a real component. For example, a honeypot phone will simulate the use of the SIP protocol and allow requests to be sent on port 5060.
A "database" type honeypot will simulate the behavior of a real database and may even contain decoy data that can be traced later.

## Characteristics of honeypots 
The honeypots can be classied by means of different orthogonal features [^1]. 

![Honeypot Characteristics](/IMAGES/Honeypot-Characteristics.drawio.png)  
<b> Fig.2 - Diagram of the different characteristics of a honeypot </b> [^22]   

In order to represent and understand the different characteristics of honeypots, a concrete example is used throughout this section. The example honeypot represents a wastewater treatment plant.

Here is a diagram:

![Basic Honeypot Exemple](/IMAGES/wastewater-treatment-plant-honeypot.png)  
<b> Fig.3 - Diagram of a wastewater treatment plant honeypot </b> [^21]  

The context used as the honeypot example represents the infrastructure of the wastewater treatment plant [^12]. Depending on the characteristics and according to the needs, we will consider either a part or the entire infrastructure as being the honeypot.
It consists of a firewall serving as a gateway to and from the outside. Within the network, we find the elements usually constituting this type of industry. There is a SCADA, the control and data acquisition system, but also a log server, allowing this data to be stored over time. These systems are directly connected to the PLCs. The PLCs make it possible, on the one hand, to recover information from the various sensors (water temperature, flow rates, etc.), and on the other hand, to send orders and commands to the various actuators (valves, bypass , ... ). If some of these components (sensors and actuators) are directly connected to a PLC, others can be located in relatively distant geographical positions. The RIOs (Remote Input/Output) are then used to make the link between the PLC and the components. Finally, all the components are visualized and checked by the engineers and technicians of the Man-Machine Interface. This interface is comparable to a traditional workstation.

### Interaction Level
The interaction level of the honeypot indicates to what extent its functionality is exposed. Two values are used to define it [^3]:  
* Low-interaction : honeypot have low level of realism. The interaction between the Hacker and the system is short and limited. It is generally not a system per se, but rather an emulation of operating systems and services. This type of Honeypot  can simulate only specific systems services and uses basic techniques like identifying port scans [^6], generating attack signatures, analyzing trends and collecting malware informations. Low-interaction honeypots are particularly useful for monitoring less complex attacks, such as robots and malwares.
* High-interaction : The honeypot provides the most realistic environment for attackers because it uses a variety of real services running on real operating systems. It imposes few restrictions inside the system, encouraging attackers to interact with it. High interaction honeypots collect information about all of the attacker's movements and actions, which is an advantage because the information collected is very faithful. Additionally, it makes them more effective at monitoring more experienced hackers, as they look realistic and are likely to deceive them. This type of honeypot is effective against automated attacks but involves risks of compromise, since it goes so far as to allow the attacker to obtain root access, giving him full power over the system.
* Medium-interaction : A pot of honey offering a mix between low and high ineraction.

In the case of the proposed example, if the attacker tries to break into a PLC, he will want to retrieve the list of TCP ports open on it. The **low interaction** honeypot will then return a list of ports and give information about the status of it. For example, when the attacker wants to try to connect and authenticate on the SSH port of the PLC, the response from the honeypot will be simulated by a script and will send back a defined message. This type of honeypot is effective against automated attacks.
While the **high interaction** honeypot allows the attacker to be able to interact with open ports and, for example, login via SSH port using low credential. The connected attackers then have free rein and can retrieve information from the sensors or modify the state of the actuators, as a real PLC would do.
In the case of a **Medium-interaction** honeypot, one can imagine on the one hand, that certain components are "high interaction", for example for the network part and the connection to the PLC via the SSH port, as explained above. On the other hand, components simulated by scripts which are able to return fictitious information from sensors or to simulate the open/closed position of an actuator.

### Ressource level
The resource level used by the honeypot is determined by the replication realism of the system. There are three possibilities: 
* Real / Physical : is a replication of a target system.
* Virtual : use virtualization technology to reproduce a system. This solution is low-cost.
* Hybrid : include a mixture of real and virtual device. This solution is cost effective.

To better understand, let's take the example of the wastewater treatment plant. **Physical** would be a carbon copy of a processing wastewater plant in production. Requiring an identical infrastructure at all levels. If the *real* wastewater plant uses 20 PLCs, the honeypot will use 20 real PLCs. One can very easily imagine the difficulty and the costs generated by such a deployment. To provide additional information, if we decided to limit ourselves to the creation of a honeypot consisting essentially of servers, then the so-called "physical" honeypot would be an exact replication of all of these servers.
The **virtual** honeypot is a virtual copy of the wastewater plant. Hosted on a machine capable of virtualizing the layers and services of each component. Virtualization makes it possible to create the 20 PLCs in such a way that they perfectly imitate the behavior of the real components of the wastewater plant. In the case of **hybrid**, one could quite imagine that the network infrastructure is completely virtualized, but that the PLCs are real physical components.

### Communication interfaces
Communication interfaces are the characteristics that define how the honey pot will be reached and through which interface one will be able to interact with it [ 1]. In order to illustrate the different communication interface possibilities of a honeypot, we can use the TCP/IP model as a reference and comparison model.
Each interface can be considered as a gateway to a system for attackers. The interest of defining the layers in which these interfaces are located makes it possible to specifically categorize honeypot entrance doors. Indeed, attackers can specifically target a protocol or an application and this model allows to have a better overview. A honeypot can have several exposed interfaces and each one belongs to one of these characteristics:
* Application: layer specifying the applications used by the honeypot and which will be exposed (HTTP, SMTP, SSH, DNS, ...)
* Transport: layer specifying how end-to-end communications are managed between processes (TCP, UDP, SCTP,...) and possible
* Network: layer specifying the packet routing method (IP, ICMP, IGMP, IPSec, ...)
* Network access: layer specifying the physical means (cable, radio, ...) and connection (WiFi, Ethernet, ...) used to communicate with the honeypot.
* Non-network Hardware Interface: Honey Pot interfaces with Non Network Hardware Interfaces (PLC, USB, etc.).

As an example in the treatment plant, we can take the case of a honeypot imitating the behavior of a server providing to clients different resource shares (files and printers) via the SMB (Server Message Block) protocol. The honeypot will receive the "**Application**: protocol SMB" feature as it is the only "exposed" interface by the honeypot. If we decide to expose flaws on other layers of the model,then we can also add these layers by specifying more precisely the protocol or technology used:
-- **Application**: SMB protocol
-- **Transport**: TCP protocol
-- **Network**: IP v4
-- **Physical**: Cable via Ethernet
We can also take an example of honeypot disconnected from the network. Let’s imagine that each USB key introduced in the building must be first connected to the honeypot (sandbox) before being used on a legitimate computer. The goal is to verify that the key does not have malware capable of infecting a system and propagating to other systems. In this case, the honetpot will receive the characteristic of **Off-network hardware interface**.

### Multi-tier architecture 
Honeypot can behave in 2 different ways when it comes to its interaction [^7]: 
* Server: honeypot acts as a server and passively waits for client requests 
* Client: honeypot acts as a client and actively initiates requests to servers  

To illustrate the use of a client honeypot, let's imagine that the legitimate workstations of the treatment plant must connect to external resources in order to send water quality analysis data. The implementation of the **client** honeypot consists of the deployment of a robot capable of visiting a list of URLs in order to verify their reliability and legitimacy. The honeypot will send http/https requests to this URL and the responses from the remote servers will be analyzed. Servers containing malware will be considered dangerous and will be listed as such. Thus avoiding a connection from the workstations of the station.

The second is the reverse role, namely the honeypot **server**, which will allow clients (PLCs, Workstations, control systems) to connect so that they use a service provided by the server. Clients will, for example, connect via the SSH protocol to the server in order to send analysis data. The server honeypot will then behave like a legitimate machine and send the corresponding responses to the requests initiated by the clients. Customer activity data is collected and analyzed to verify that no customer attempts to execute illegal commands and access unauthorized information.

### Topology
The topology of a honeypot determines its physical, software or logical architecture. It is generally represented with nodes connected to each other and defining a structure[^15]:

* Centralized: Centralized honeypots use a client/server architecture where one or more client components (client nodes) are directly connected to a central server (central node).

* Decentralized: Decentralized honeypots also use a client/server architecture, with the difference that the honeypot consists of several servers (central nodes) communicating with each other. These central nodes also communicate with client components (client nodes) which are specific to them.

* Distributed: Distributed honeypots do not work with a client/server architecture, so there are no client nodes and central nodes (even if some nodes have coordination and arbitration roles). It is a mesh architecture where each node is connected with several other nodes. These nodes work together to form a honeypot.

Within the wastewater treatment plant and to illustrate a **Centralized** topology, one can imagine a virtual honeypot, made up of a virtual machine acting as a central server and containing a RedHat operating system and making it possible to simulate the behavior of a SCADA. Along with this, the central server contains the logging system and can also simulate the behavior of a workstation. The client components (PLCs, RIOs, ...) are on other virtual machines and communicate directly with the central server. Client nodes synchronize with the node and retrieve configuration information (NTP, routines, commands, etc.) or send data for analysis. Concretely, all communications pass through the central nodes, if this were to be out of service, the client nodes would become an orphan, resulting in a total failure of the system, which constitutes a Single point of failure.

To explain the Decentralized honeypot, just take the example above and imagine that we duplicate the virtual honeypot 3 times, while keeping the components and simply modifying their configurations so that they have the appearance to be on another treatment plant site. We get 4 honeypots. Now let's add a connection between these 4 honeypots and a totally independent logging server. The honeypot now has a **Decentralized** topology. Each of the central nodes is completely independent. If one of the nodes were to go out of service, the other central nodes would continue to operate and communicate with each other, causing a partial failure of the system.

The **Distributed** topology of a honeypot can be explained by imagining that a network of honeypots has been created consisting of workstations within the treatment plant. Each workstation is a honeypot in its own right, intended to be compromised and for which we will analyze incoming and outgoing traffic. Each of these workstations is independent and aims to report information. If one of them is compromised, the entire infrastructure continues to operate, without degrading the integrity of the system. This type of honeypot is for example used to counter DDoS attacks [^16].

### Containment
The containment strategy defines the ability of a honeypot to defend itself against attacks, other malicious activities spreading from it. A honeypot can use several of these strategies [^1]:
* Block : attacker is identified and blocked, he never reaches his target
* Defuse : attacker reaches his target, but his attacks are defused; he is manipulated way to fail 
* Slow down: The attacker is slowed down throughout their attack process and the benefits of parallel automated attacks are reduced. He will consume resources and will end up getting discouraged [^17]
* None : No action is taken to prevent the attacker, the aim being to study all his actions.

To illustrate this characteristic, one can imagine that a hacker has entered an HMI of the wastewater treatment plant and tries to modify the position of a valve (actuator). Based on this observation, several reaction strategies are possible. In the case of a **Block**, one can imagine that as soon as the honeypot has detected and identified the pirate, it is automatically blacklisted and the connection is interrupted.
In the case of a **Defuse**, the pirate has already achieved his objective and the command to modify the position of the valve has been sent. From this moment, the honeypot is able to detect unauthorized activity. The attack is defused and the valve has returned to its normal state.
In the case of a **Slow down**, everything is done to slow down and discourage the attacker. When he thinks he has sent the command to modify the position of the valve, another verification is requested, the process is slowed down or does not succeed. Concretely, he is faced with new pitfalls and his objective is never achieved.
Finally, if we decide that the honeypot of our treatment plant is intended to study the behavior of the hacker, we can decide to let him act with impunity and study his methodology. The attacker can reach his target with or without difficulty, depending on the implementation of the honeypot. In this case, no containment policy (**None**) is applied.

### Observability
This characteristic does not directly concern the technical aspects, but rather its ability to capture types of data [^1]: 
* Event : collects data related to an abnormal event that has occurred or linked to a change in the state of a system or a component.
* Attacks : collects activities threatening the security policy.
* Intrusions : collects policy-threatening activities that lead to a security breach.
* None : no data collection.  

Returning to the example case, if there is an unexpected event capable of being detected by the honeypot, such as the unwanted opening of a valve, then it will receive the **Event** data capture characteristic. . If, on the other hand, the honeypot is able to capture the unsuccessful attempts of a hacker trying to modify the position of the valve, then it will receive the **Attack** data capture characteristic. If the honeypot can capture the events produced by an attack resulting in an intrusion, then it will be assigned the **intrusions** data capture characteristic. Finally, if the honeypot is not intended to capture information, as is the case for a decoy intended to imprison hackers to prevent them from acting. They can be assigned the characteristic of **None**.

### Scalability:
Scalability determines the ability of a honeypot to evolve. By this we mean its ability to be modified in order to increase the number of decoys and services it offers [^3]:
* Scalable: can increase the number of services and lures offered
* Not Scalable: Only has a set number of services and cannot be changed at that level.  

Let's take the example of the PLCs present in the structure of the honeypot of the wastewater treatment plant. If PLCs can be added, then the honeypot is considered **scalable**. On the other hand, if it is impossible to add more, then it is considered as **non-scalable**.

### Context 
This characteristic is used to define in which context the honeypot is used and what is the purpose of its implementation [^3]:
* Research : is used to lure attackers and study their behaviours and the tools they use to develop better protection against these attacks.
* Production : is used to defend and prevent attack on real systems and to protect it.  
It is important to note that a honeypot can serve both as a means of protection, while collecting data allowing research, therefore, a honeypot can be assigned both values of this characteristic.

To illustrate this characteristic, one can imagine the existence of a virtual honeypot with high interaction identically imitating the behavior of a real wastewater treatment plant in production.
Its deployment can be carried out within the framework of **research**, we want to highlight the flaws that may exist in the existing system and know how to protect ourselves from attackers.
In the case of a **production**, its purpose is above all to protect the real system and one does not necessarily seek to collect data for study purposes, but rather to divert the attention of the attacker.

## Strength and weakness of characteristics

<b> Fig.4 - Table of strengths and weaknesses of honeypots characteristics </b> [^19]     
it will be uploaded after review and validation.  
Follow the link to view the latest version -> [^13]

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

Data collection: Means necessary and used to guarantee the safe transfer of data collected by honeypots to a centralized point.

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
* IoT : Internet of Things.
* IIoT : Industrial Internet of Things.
* CPS : Cyber-physical system - Cyber-physical system: Computing environment composed of deeply intertwined physical and software elements. Networks of devices composed of: sensor, actuator, PLC, RTU, IED, Monitoring, ICS, etc.  
* RTU : Remote Terminal Units - Electronic device controlled by microprocessor which connects the objects of the physical world to a distributed control system or to a SCADA  .
* ICS : Industrial Control Systems is a Control systems and associated instrumentation, which include the devices, systems, networks, and controls used to operate and/or automate industrial processes.  Exemple : Smart Grid and other smart infrastructures : water, gas, building automation, medical devices, smart cars, etc.  
* System : Set of elements that make up a pot of honey. A system may consist of several subsystems determining the intrinsic characteristics of the honyepot.
* CVE : Common Vulnerabilities and Exposures.
* SCADA : For "Supervisory Control and Data Acquisition". Industrial supervision system that processes a large number of measurements in real time and remotely controls installations.
* Logging server: Data archiving system designed to collect, store, and retrieve time-based information.
* PLC : Programmable Logic Controllers - Programmable digital electronic device for controlling industrial processes by sequential processing. Exemple : Input cards for connecting sensors, push buttons, actuators, indicators, valves, etc.  
* Remote Input/Output (RIO) : Remote I/O device for sending or receiving I/O signs from a PLC. (Also call "Distributed Input/Output").
* Sensor : Device for measuring the state of a system and transmitting it to a data acquisition system.
* Actuator : Device for modifying the state of a system.
* Human Machine Interface (HMI) : Means and tools implemented so that a human can control and communicate with a machine.
* Application Programming Interface (API) : Standardized set of classes, methods, functions, and constants that serves as a front through which software provides services to other software through a software library or web service.

## References
[^1]: Seifert, C., Welch, I., & Komisarczuk, P. (2006). Taxonomy of honeypots. http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.61.5339
[^2]: Fan, W., Du, Z., & Fernández, D. (2015, November). Taxonomy of honeynet solutions. In 2015 SAI Intelligent Systems Conference (IntelliSys) (pp. 1002-1009). IEEE. https://ieeexplore.ieee.org/abstract/document/7361266/
[^3]: Franco, J., Aris, A., Canberk, B., & Uluagac, A. S. (2021). A survey of honeypots and honeynets for internet of things, industrial internet of things, and cyber-physical systems. IEEE Communications Surveys & Tutorials, 23(4), 2351-2383. https://ieeexplore.ieee.org/abstract/document/9520645/
[^4]: Antonioli, Daniele & Agrawal, Anand & Tippenhauer, Nils Ole. (2016). Towards High-Interaction Virtual ICS Honeypots-in-a-Box. 13-22. 10.1145/2994487.2994493. https://dl.acm.org/doi/abs/10.1145/2994487.2994493 
[^5]: Mairh, Abhishek and Barik, Debabrat and Verma, Kanchan and Jena, Debasish. (2011). Honeypot in Network Security: A Survey. https://dl.acm.org/doi/10.1145/1947940.1948065
[^6]: Ahn, Seonggwan, Thummin Lee, and Keecheon Kim. "A study on improving security of ICS through honeypot and ARP spoofing." (2019) International Conference on Information and Communication Technology Convergence (ICTC). IEEE, https://ieeexplore.ieee.org/abstract/document/8939925/
[^7]: Mohammadzadeh, H., Mansoori, M., & Honarbakhsh, R. "Taxonomy of Hybrid Honeypots". (2011). https://www.semanticscholar.org/paper/Taxonomy-of-Hybrid-Honeypots-Mohammadzadeh-Mansoori/711bf1e19078df842f6388869388e9c128cf1024
[^8]: MITRE ATT&CK® https://attack.mitre.org/
[^9]: MITRE ATT&CK® for ICS https://collaborate.mitre.org/attackics/index.php/Main_Page
[^10]: MITRE CVE (Common Vulnerabilities and Exposures) https://cve.mitre.org/
[^11]: Ben Lutkevich. (2021). "How to build a honeypot to increase network security"https://www.techtarget.com/searchsecurity/definition/honey-pot
[^12]: Daniele Antonioli, Anand Agrawal, and Nils Ole Tippenhauer. 2016. Towards High-Interaction Virtual ICS Honeypots-in-a-Box. In Proceedings of the 2nd ACM Workshop on Cyber-Physical Systems Security and Privacy (CPS-SPC '16). Association for Computing Machinery, New York, NY, USA, 13–22. DOI:https://doi.org/10.1145/2994487.2994493
[^13]: Strength and weakness of characteristics by Abdel-Malek Bouhou https://docs.google.com/spreadsheets/d/e/2PACX-1vQIh2CTBfqDZfc2udGiV6FrjzKUtCasVX8TiVj5VKKvuYEOTsKZUEyHIBR0Yaiqiu7e75yGc7UK4Nni/pubhtml
[^14]: Falliere, N., Murchu, L. O., & Chien, E. (2011). W32. stuxnet dossier. White paper, symantec corp., security response, 5(6), 29. https://pax0r.com/hh/stuxnet/Symantec-Stuxnet-Update-Feb-2011.pdf
[^15]: "Comparison – Centralized, Decentralized and Distributed Systems"https://docs.google.com/spreadsheets/d/161CdK2RIelx0XPv9ubSTCAu8D_C_jPPSj2D-2Jy2kI8/edit?usp=sharing
[^16]: Deshpande, Hrishikesh. (2015). HoneyMesh: Preventing Distributed Denial of Service Attacks using Virtualized Honeypots. International Journal of Engineering Research and. V4. 10.17577/IJERTV4IS080325. : https://www.researchgate.net/publication/281144265_HoneyMesh_Preventing_Distributed_Denial_of_Service_Attacks_using_Virtualized_Honeypots
[^17]: Ponemon Institute, Sponsored by Palo Alto Networks. "Flipping the Economics of Attacks" .2016. https://www.ponemon.org/news-updates/blog/security/flipping-the-economics-of-attacks.html
[^18]: L. Spitzner, "Honeypots: catching the insider threat," 19th Annual Computer Security Applications Conference, 2003. Proceedings., 2003, pp. 170-179, doi: 10.1109/CSAC.2003.1254322. : https://ieeexplore.ieee.org/abstract/document/1254322
[^19]: honeypot/IMAGES/Honeypot-Characteristics-Strength-Weaknes-tab.drawio
[^20]: honeypot/IMAGES/honeypot-basic-diagram.drawio
[^21]: honeypot/IMAGES/wastewater-treatment-plant-honeypot.drawio
[^22]: honeypot/IMAGES/Honeypot-Characteristics.drawio.drawio
