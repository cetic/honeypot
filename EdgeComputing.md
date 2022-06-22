# Edge computing : 
To understand edge computing, you have to understand cloud computing.

Cloud computing enables companies to provide IT services over the Internet. Users can benefit from various on-demand online services, such as access to software (SaaS), access to platforms (PaaS) and the provision of hardware resources (IaaS). The main objective of setting up cloud computing in companies is to minimize the costs of the IT infrastructure and to be able to adapt its resources according to its needs and the fluctuation of needs.

Beyond the companies themselves, cloud computing is also one of the essential elements for the advent of the Internet of Things.
Indeed, the use of IoT in conjunction with cloud computing technologies is now inseparable and linked to each other. The resulting Internet applications can be linked to the world of industry or business, but also for domestic applications. There are applications such as surveillance, virtual reality, traffic monitoring, home automation, smart cities, logistics, etc.
Every year, the number of connected objects increases significantly and could reach 50 billion by the end of 2022 [1]. With this increase and the growing use of cloud applications and services by these mobile devices, mobility-related issues have emerged that result in high latencies.

One of the concepts to solve these problems is edge computing[^2]. Edge Computing is an optimization concept that consists of processing data and the intelligence of its processing on the periphery of the data source. it makes it possible to meet the application requirements mentioned above by bringing the treatment to the periphery of the network.

![Basic Honeypot Exemple](/IMAGES/cloud-fog-edge_infographic.jpg)
<b> Fig.1 - Industrial IoT data precessing layer stack  </b> [^3]   

In practical terms, edge computing is an advanced version of cloud computing that reduces latency by bringing services closer to end users. It solves high latency and bottlenecks that are not properly managed in the cloud computing paradigm.
One of the major differences between edge computing and cloud computing is the location of servers. Edge computing services are located in the Edge network while cloud services are located on the Internet.

There is also the concept of Fog computing which is very similar to Edge computing.
The major difference is that the Edge computingtends to decentralize processing on devices at the periphery of networks, while Fog computing seeks to distribute processing on local network units using intermediate data aggregation strategies when necessary.

Other concepts have also been implemented by private companies such as "Open Nebula". It offers an even more detailed view of "Edge computing" by adding specific layers depending on the type of systems being connected. It also adds a notion of distance to categorize them. As shown in Figure 2, five categories emerge:
* The public cloud corresponds to resources located in Data Centers at more than 1000 Km, and having a latency of 20 ms.
* Public Edge, corresponding to national or private Data Centres, or on a company’s premises. In this case we are talking about distances ranging from 100 km to 1000 km and having a latency of 10 to 20 ms.
* 5G/ Near Edge, defining 5G and cellular antenna sites, aggregation nodes used in telecoms (operator’s cabin,...) and Utilitys Networks (gas, electricity, water cabin,...). These resources are between 1 km and 100 km, and have a latency of 2 to 5 ms.
* Even closer, the On-Premise Edge is, by definition, the resources that are nearby and stored "locally". For example, it is the computer systems of a hospital, a factory or a football stadium that are installed within these infrastructures. In this case, the resources are less than 1 km away and have a relatively low latency of 1 ms.
* Finally, the IoT Edge, or FAR Edge, represents all the connected objects of everyday life. These items are smartphones, bicycles, cameras, but also convenience services such as trains, kiosks, etc. These resources are considered "in range" and have very low latencies.

![Basic Honeypot Exemple](/IMAGES/DC-Edge_Continuum.png)
<b> Fig.2 - Representation of the different concepts related to edge computing  </b> [^4]   

The availability of cloud services on the Internet depends on the distance of multiple jumps between the end-user and the cloud servers. The significantly high distance between the mobile device and the cloud server induces high latency in cloud computing compared to low latency in edge computing.

Beyond performance issues, it is likely that the number of data attacks on the road is higher in cloud computing than in edge computing due to the longer path to servers.

However, security issues are just as important in the world of edge computing. Garner predicts that 75% of data created and processed by companies will be done outside of a traditional centralized data centre or cloud by 2025. In other words, the use of edge technologies is on the verge of enormous growth, and this growth is accompanied by new cybersecurity threats.

First, because the extension of peripheral computing exponentially increases the attack surface. Then, because one of the emerging providers aggravates this risk. Unsecured terminals are already used in distributed denial-of-service attacks or as entry points to core networks. [7]

Using honeypot in the different layers that make up edge computing can be a great way to study attackers, their tools, techniques and procedures, and how they would try to circumvent the actual security controls that make up these different layers.

One of the solutions proposed by Stolfo [^5] is to use decoy and honeypot techniques to limit the damage caused by stolen data by reducing the value of this stolen information. They postulate that cloud and edge computing services can be implemented by profiling user behavior and using lures.
Concretely, the behavior of the user is analyzed and if it turns out abnormal, luring information can be returned by the Cloud and delivered in such a way as to appear completely legitimate and normal. The use of this decoy information makes it possible to detect malicious activity, to create confusion for the attacker who will have to spend resources to distance the real from the false information, creating naturelement a deterrent effect. 

Other solutions are being considered.

## Glossary 
* SaaS : Software As A Service.
* PaaS : Platform As A Service.
* IaaS : Infrastructure As A Service.

## References
[^1]: 
[^2]: Khan, W. Z., Ahmed, E., Hakak, S., Yaqoob, I., & Ahmed, A. (2019). Edge computing: A survey. Future Generation Computer Systems, 97, 219-235. https://www.sciencedirect.com/science/article/pii/S0167739X18319903
[^3]: Stolfo, S. J., Salem, M. B., & Keromytis, A. D. (2012, May). Fog computing: Mitigating insider data theft attacks in the cloud. In 2012 IEEE symposium on security and privacy workshops (pp. 125-128). IEEE. https://ieeexplore.ieee.org/abstract/document/6227695/
[^4]: "Cloud, Fog and Edge Computing – What’s the Difference" https://www.winsystems.com/cloud-fog-and-edge-computing-whats-the-difference/
[^5]: "Building an Open Source Edge Computing Platform" https://opennebula.io/building-an-open-source-edge-computing-platform/