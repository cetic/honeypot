# Edge computing : 
To understand edge computing, you have to understand cloud computing.

Cloud computing enables companies to provide IT services over the Internet. Users can benefit from various on-demand online services, such as access to software (SaaS), access to platforms (PaaS) and the provision of hardware resources (IaaS). The main objective of setting up cloud computing in companies is to minimize the costs of the IT infrastructure and to be able to adapt its resources according to its needs and the fluctuation of needs.

Beyond the companies themselves, cloud computing is also one of the essential elements for the advent of the Internet of Things.
Indeed, the use of IoT in conjunction with cloud computing technologies is now inseparable and linked to each other. The resulting Internet applications can be linked to the world of industry or business, but also for domestic applications. There are applications such as surveillance, virtual reality, traffic monitoring, home automation, smart cities, logistics, etc.
Every year, the number of connected objects increases significantly and could reach 50 billion by the end of 2022 [1]. With this increase and the growing use of cloud applications and services by these mobile devices, mobility-related issues have emerged that result in high latencies.

One of the concepts to solve these problems is edge computing[^2]. Edge Computing is an optimization concept that consists of processing data and the intelligence of its processing on the periphery of the data source. it makes it possible to meet the application requirements mentioned above by bringing the treatment to the periphery of the network.
In practical terms, edge computing is an advanced version of cloud computing that reduces latency by bringing services closer to end users. It solves high latency and bottlenecks that are not properly managed in the cloud computing paradigm.
One of the major differences between edge computing and cloud computing is the location of servers. Edge computing services are located in the Edge network while cloud services are located on the Internet.

There is also the concept of Fog computing which is very similar to Edge computing.
The major difference is that the Edge computingtends to decentralize processing on devices at the periphery of networks, while Fog computing seeks to distribute processing on local network units using intermediate data aggregation strategies when necessary.

![Basic Honeypot Exemple](/IMAGES/cloud-fog-edge_infographic.jpg)
<b> Fig.1 - Industrial IoT data precessing layer stack  </b> [^3]   

Indeed, the availability of cloud services on the Internet depends on the distance of multiple jumps between the end user and the cloud servers. The significantly high distance between the mobile device and the cloud server induces high latency in cloud computing compared to low latency in edge computing.
Beyond performance issues, it is likely that the number of on-road data attacks is higher in cloud computing than in edge computing due to the longer path to servers.

However, safety issues are just as important and the use of honeypot can be very useful.
One of the solutions proposed by Stolfo [^4] is to use decoy and honeypot techniques to limit the damage caused by stolen data by reducing the value of this stolen information. They postulate that cloud and edge computing services can be implemented by profiling user behavior and using lures.
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