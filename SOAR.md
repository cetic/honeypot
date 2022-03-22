# State of the art : Honeypots
The Honeypot is by vocation, a more or less artificial information system whose main purpose is to be attacked in order to exploit any information on the Hackers, their methods, their motivations and the attack techniques to which they resort to break into or corrupt a system.
TODO

## Honeynet 
A honeynet is a network of honeypots respecting a certain topology.
TODO
### Features
It is composed of 3 main features:
Data control: Set of measures aimed at reducing the risk that a honeypot will be compromised and used to attack other systems. Outbound attacks must be controlled to protect non-honeypot systems

Data capture: Its purpose is to capture and record and collect the activities of attackers in order to be exploited later. 3 critical data capture layers have been identified:
* The layer related to incoming and outgoing connections stored in the firewall logs.
* The traffic analysis layer, which checks packets and their payloads as they enter and leave the honeynet.
* The layer related to activity on the system (system calls, modified files, attacker's keystroke, etc).

Data collection: Means necessary and used to guarantee the safe transfer of data collected by honeypots to a centralized point 

### Classification 
(IMAGE) --> best practice to import ?
TODO
* Resource Level
 * Physical
 * Virtual
  * Self-contained virtual honeynet
  * Hybrid virtual honeynet
 * Mixed
* Adaptability Level
 * Static
 * Dynamic
* IP Network Scope
 * Stand-Alone
 * Distributed
* Physical Placement 
 * Local
 * Remote
* Logical Deployment
 * Minefield
 * Shield



## Characteristics of honeypots 
The honeypots can be classied by means of different orthogonal features. 

### Interaction Level
* Low-interaction : honeypot have low level of realism. The interaction between the Hacker and the system is short and limited. It is generally not a system per se, but rather an emulation of operating systems and services. This type of Honeypot  can simulate only specific systems services and uses basic techniques like identifying port scans, generating attack signatures, analyzing trends and collecting malware informations. 
* A High-interaction : honeypot provide the most realistic environment for the attackers because it use real services running on real operating systems. 

### Ressource level
* Real : is a replication of a target system. This solution is expensive.
* Virtual : use virtualization technology to reproduce a system. This solution is low-cost.
* Hybrid : include a mixture of real and virtual device. This solution is coste effective

### Communication interfaces
* Network interface: the honeypot communicates directly through a network interface 
* Non-network hardware interface: the honeypot interfaces with hardware interfaces other than networks (PLC, USB, etc.) 
* API : the honeypot communicates via a software API 

### Multi-tier architecture 
* Server: honeypot acts as a server and passively waits for client requests 
* Client: honeypot acts as a client and actively initiates requests to servers 

### Distribution
* Distributed : honeypot is or appears to be composed of multiple systems 
* Autonomous : honeypot is or appears to be a system, even if it is composed of several systems but appears to be only one 

### Confinement
* Block : attacker is identified and blocked, he never reaches his target
* Defuse : attacker reaches his target, but his attacks are defused; he is manipulated way to fail 
* Slow down : attacker is slowed down throughout his attacking process, the goal being to discourage him 
* None : no action is taken to prevent the attacker (Profiling?) 

### Data capturing 
* Event : an event has occurred -> Status change .
* Attacks : collects activities threatening the security policy.
* Intrusions : collects policy-threatening activities that lead to a security breach.
* None: no data collection.

### Detection
* Abuse: Data is analyzed and associated with a large database.
* Anomaly: The networks are analyzed and anomalies are identified. It can be related to traffic load, packets and protocols.

### Context 
* Research : is used to lure attackers and study their behaviours and the tools they use.
* Production : is used to prevent attack on real systems and to protect it.


## Honeypot vs IDS vs IPS
TODO


## Strength and weakness of characteristics

|  Characteristic   | Strength                                                          | Weakness                                          |
|-------------------|---------------------------------------------------------------    |---------------------------------------------------|
| Low-Interaction   | - Low resource Consumption \\ - Limited risk of compromise        | - Easily detectable                               |
| High-Interaction  | - Easy to implement                                               | - High risk of comprimise if poorly protected     |
|                   |                                                                   |                                                   |
|                   |                                                                   |                                                   |
|                   |                                                                   |                                                   |
|                   |                                                                   |                                                   |
|                   |                                                                   |                                                   |
|                   |                                                                   |                                                   |
|                   |                                                                   |                                                   |

## Measures of Effectiveness



## Type of attacks 
* Distributed / Denial of- Service
* Man-in-the-Middle
* Phishing
* Drive-by- Download
* Password
* SQL Injection
* Cross-Site Scripting (XSS)
* Eavesdropping (/ snooping attacks / spying attacks)
* Birthday
* Malware

## Open-Source Honeypots
 : 

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

## References
* [1] Seifert, C., Welch, I., & Komisarczuk, P. (2006). Taxonomy of honeypots. http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.61.5339
* [2] Fan, W., Du, Z., & Fernández, D. (2015, November). Taxonomy of honeynet solutions. In 2015 SAI Intelligent Systems Conference (IntelliSys) (pp. 1002-1009). IEEE. https://ieeexplore.ieee.org/abstract/document/7361266/
* [3] Franco, J., Aris, A., Canberk, B., & Uluagac, A. S. (2021). A survey of honeypots and honeynets for internet of things, industrial internet of things, and cyber-physical systems. IEEE Communications Surveys & Tutorials, 23(4), 2351-2383. https://ieeexplore.ieee.org/abstract/document/9520645/
* [4] Antonioli, Daniele & Agrawal, Anand & Tippenhauer, Nils Ole. (2016). Towards High-Interaction Virtual ICS Honeypots-in-a-Box. 13-22. 10.1145/2994487.2994493. https://dl.acm.org/doi/abs/10.1145/2994487.2994493 
