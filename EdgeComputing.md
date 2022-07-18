# Edge computing 

In the Internet world, cloud computing allows businesses to provide IT services online. Users can benefit from various on-demand online services, such as access to software (SaaS), access to platforms (PaaS) and the provision of hardware resources (IaaS). The main objective of setting up cloud computing in companies is to minimize the costs of the IT infrastructure and to be able to adapt its resources according to its needs and the fluctuation of needs.

Beyond the companies themselves, cloud computing is also one of the essential elements for the advent of the Internet of Things.
Indeed, the use of IoT in conjunction with cloud computing technologies is now inseparable and linked to each other. The resulting Internet applications can be linked to the world of industry or business, but also for domestic applications. There are applications such as surveillance, virtual reality, traffic monitoring, home automation, smart cities, logistics, etc.

Every year, the number of connected objects increases significantly and could reach 50 billion by the end of 2022. With this increase and the growing use of cloud applications and services by these mobile devices, mobility-related issues have emerged, showing the limits of centralized computing that relies on hundreds or thousands of servers running applications in consolidated data centers

One of the concepts to solve these problems is edge computing[^1]. Edge Computing is an optimization concept that consists of processing data and the intelligence of its processing on the periphery of the data source. it makes it possible to meet the application requirements, but it also brings a new set of challenges [^6] to the network.

* **Network bandwidth** : The way network bandwidth is distributed is changing. Traditionally, the bandwidth allocated to data centers is higher than the bandwidth allocated to terminals. Edge computing drives the need for more network bandwidth.
* **Distributed computing** : The increase in distributed computing and east-west traffic is driving thinking about consolidated compute models and device placement based on use cases.The increase in distributed computing and east-west traffic is driving thinking about consolidated compute models and device placement based on use cases.
* **Latency** : The reduction in application latency and decision cost is reduced thanks to the proximity of computing resources to the edge. By limiting the effects of coming and going from the data center to the terminals, responses and actions are faster.
One of the major challenges is managing the replication of data from the data center and to the edge.
* **Security and accessibility** : the major issue of security is the management of the change of paradigm. Centralized data security enables the standardization of technical security and physical security. Edge computing requires thinking about network models, physical security, traffic models and above all the management of user access rights on a much larger number of devices.
* **Backup** : Business backup strategies are critically dependent on where the data resides. Network bandwidth requirements and storage support are equally critical in edge computing. However, network backups may not make sense depending on the application.
* **Data accumulation** : Data is a key business asset. Storing and accessing this data at the edge creates new challenges in the lifecycle of this data.
* **Control and management** :From company to company, the physical edge location differs. Enterprises need to use newer orchestration tools to consistently manage and control applications regardless of location.
* **Scale** : Edge computing requires increasing scalability across all computing disciplines: compute, networking, storage, management, security, licensing, and more. We must not be satisfied with increasing the number of servers, this challenge requires having a global reflection around the scalability of everything related to the edge.

![Basic Honeypot Exemple](/IMAGES/cloud-fog-edge_infographic.jpg)  
<b> Fig.1 - Industrial IoT data precessing layer stack  </b> [^2]   

In practical terms, edge computing is an advanced version of cloud computing that solves high latencies and bottlenecks that are not properly managed in the cloud computing paradigm.
It meets the requirements and challenges of the evolution of computer networks by bringing services closer to end users.
One of the main differences between edge computing and cloud computing is the location of the servers. Edge computing services are located in the edge network while cloud services are located on the internet.

There is also the concept of Fog computing which is very similar to Edge computing.
The major difference is that the Edge computingtends to decentralize processing on devices at the periphery of networks, while Fog computing seeks to distribute processing on local network units using intermediate data aggregation strategies when necessary[^8].

Other concepts have also been implemented by private companies such as "Open Nebula"[^3]. It offers an even more detailed view of "Edge computing" by adding specific layers depending on the type of systems being connected. It also adds a notion of distance to categorize them. As shown in Figure 2, five categories emerge:
* The **Public cloud** corresponds to resources located in Data Centers at more than 1000 Km, and having a latency of 20 ms.
* **Public Edge**, corresponding to national or private Data Centres, or on a company’s premises. In this case we are talking about distances ranging from 100 km to 1000 km and having a latency of 10 to 20 ms.
* **5G/ Near Edge**, defining 5G and cellular antenna sites, aggregation nodes used in telecoms (operator’s cabin,...) and Utilitys Networks (gas, electricity, water cabin,...). These resources are between 1 km and 100 km, and have a latency of 2 to 5 ms.
* Even closer, the **On-Premise Edge** is, by definition, the resources that are nearby and stored "locally". For example, it is the computer systems of a hospital, a factory or a football stadium that are installed within these infrastructures. In this case, the resources are less than 1 km away and have a relatively low latency of 1 ms.
* Finally, the **IoT Edge, or FAR Edge**, represents all the connected objects of everyday life. These items are smartphones, bicycles, cameras, but also convenience services such as trains, kiosks, etc. These resources are considered "in range" and have very low latencies.

![Different concepts related to edge computing](/IMAGES/DC-Edge_Continuum.png)  
<b> Fig.2 - Representation of the different concepts related to edge computing  </b> [^3]   

The availability of cloud services on the Internet depends on the distance of multiple jumps between the end-user and the cloud servers. The significantly high distance between the mobile device and the cloud server induces high latency in cloud computing compared to low latency in edge computing.

Beyond performance issues, it is likely that the number of data attacks on the road is higher in cloud computing than in edge computing due to the longer path to servers.

However, security issues are just as important in the world of edge computing. Garner predicts that 75% of data created and processed by companies will be done outside of a traditional centralized data centre or cloud by 2025. In other words, the use of edge technologies is on the verge of enormous growth, and this growth is accompanied by new cybersecurity threats.

First because extending the footprint of entreprises using edge computing exponentially increases the surface area for attacks. Then, because a nascent vendor landscape compounds this risk. Unsecure endpoints are already used in distributed denial-of-service attacks or as entry points to core networks[^4].

## Honeypot and Edge computing
Using honeypot in the different layers that make up edge computing can be a great way to study attackers, their tools, techniques and procedures, and how they would try to circumvent the actual security controls that make up these different layers.

One of the solutions proposed by Stolfo [^5] is to use decoy and honeypot techniques to limit the damage caused by stolen data by reducing the value of this stolen information. They postulate that cloud and edge computing services can be implemented by profiling user behavior and using lures.

Concretely, the behavior of the user is analyzed and if it turns out abnormal, luring information can be returned by the Cloud and delivered in such a way as to appear completely legitimate and normal. The use of this decoy information makes it possible to detect malicious activity, to create confusion for the attacker who will have to spend resources to distance the real from the false information, naturally creating a deterrent effect. 

This solution could be extended for each of the edge computing layers. Indeed and for example, at the "IoT Edge" layer, using client honeypots imitating smartphone behavior and accessing resources from the "On-Premoise Edge" layer. Or, by using server-type honeypots, providing WebApps-type services and returning decoy informations in the event of positive profiling.

Other solutions are being considered.

## Glossary 
* SaaS : Software As A Service.
* PaaS : Platform As A Service.
* IaaS : Infrastructure As A Service.
* Est-West traffic : Describes the transfer of data packets from one server to another within a data center

## References
[^1]: Khan, W. Z., Ahmed, E., Hakak, S., Yaqoob, I., & Ahmed, A. (2019). Edge computing: A survey. Future Generation Computer Systems, 97, 219-235. https://www.sciencedirect.com/science/article/pii/S0167739X18319903  
[^2]: "Cloud, Fog and Edge Computing – What’s the Difference" https://www.winsystems.com/cloud-fog-and-edge-computing-whats-the-difference/  
[^3]: "Building an Open Source Edge Computing Platform" https://opennebula.io/building-an-open-source-edge-computing-platform/.  
[^4]: R. van der Meulen 2018. What Edge Computing Means for Infrastructure and Operations Leaders. https://www.gartner.com/smarterwithgartner/  what-edge-computing-means-for-infrastructure-and-operations-leaders   
[^5]: Stolfo, S. J., Salem, M. B., & Keromytis, A. D. (2012, May). Fog computing: Mitigating insider data theft attacks in the cloud. In 2012 IEEE symposium on security and privacy workshops (pp. 125-128). IEEE. https://ieeexplore.ieee.org/abstract/document/6227695/  
[^6]: J. Fruehe, Edge computing challenges and ways to address them. (2020) https://www.techtarget.com/searchnetworking/answer/What-are-edge-computing-challenges-for-the-network  
[^7]: J. English, east-west traffic  https://www.techtarget.com/searchnetworking/definition/east-west-traffic  
[^8]: Khan, W. Z., Ahmed, E., Hakak, S., Yaqoob, I., & Ahmed, A. (2019). Edge computing: A survey. Future Generation Computer Systems, 97, 219-235. https://doi.org/10.1016/j.future.2019.02.050   