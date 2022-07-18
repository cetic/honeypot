# DevOps 

DevOps is a set of practices that aim to develop faster and more efficiently by reducing the life cycle of software development. It also aims to improve the quality of the code and thus the software while improving productivity and reducing costs in the long term.
It was born of a desire to use and globalize agile methods in development processes. On the other hand, it can be used to address organizational and collaboration issues between development and operational departments, which can have an impact on performance and quality.

"Dev" refers not only to developers but to the entire team involved in developing a software solution. It combines practices, people, tools, technologies and processes from different disciplines, such as planning, testing, quality assurance, etc. Similarly, "Ops" refers to all members of the operations team : system administrators, system engineers, database administrators, operating personnel, publishing engineers, etc. [^1]

DevOps to foster the automation and monitoring of each step of application creation, from development, integration, testing, delivery to deployment, operation and maintenance of systems in a continuous pipeline. 

Frameworks like CALMS can be used as a way to assess whether an organization is ready to adopt DevOps processes, or how an organization is progressing in its DevOps transformation. CALMS is based on five pillars:

* **C**culture: for the establishment of a collaborative culture.
* **A**utomation: for process automation throughout the DevOps lifecycle.
* **L**ean: for optimizing flows and eliminating waste.
* **M**easurement: for data collection that will help teams make decisions to understand capabilities and improvements that could be made
* **S**haring: for a culture of openness and sharing within and across teams to unify them and work towards the same goals.

![DevOps: Lifecycle](/IMAGES/DevOps.PNG)
<b> Fig.1 - DevOps lifecycle  </b> [^2]     

# DevSecOps

Security has long been considered an activity that begins after production and has sometimes never been considered until problems arise on the final product.

DevOps principles often do not integrate security teams into their CI/CD pipeline. Adding security to the pipeline translates into secure applications from the design stage (by design), which reduces the costs of its implementation, as the security problems and the financial and reputational damage they will cause are much reduced.

DevSecOps is therefore the answer to the integration of security in the early design and production phases as it aims to increase speed and reduce the frequency of bugs and security issues and their impact on production through continuous security (CS). 

To do this, we will use the principle of "Shift-left". This practice involves moving the tests, quality and performance evaluation at the beginning of the software development process, so the process of moving to the “left” side (Dev) of the DevSecOps lifecycle. Shift-left accelerates development efficiency and reduces costs by detecting and addressing software defects earlier in the development cycle before they reach production.

Concretely, DevSecOps solves these problems by placing security earlier in the application development lifecycle to reduce vulnerabilities and bring security closer to objectives through threat modeling, intrusion testing exercises and, to some extent, security monitoring, and the automation of incident responses when considering the IDS, SIEM and SOAR tools. [^3]

To this end, it is interesting to integrate a honeypot solution allowing to evaluate the security of the components during the life cycle of the development of an application. A Honeypot makes it possible to study both the behavior of attackers in terms of implemented security techniques, but also to highlight possible flaws and vulnerability.

![DevSecOps: Lifecycle](/IMAGES/DevSecOps.png)
<b> Fig.2 - DevOps lifecycle and details </b> [^2]     

In the DevSecOps lifecycle, the honeypot finds its place in 3 key stages, namely: "Operate", "Monitor" and "Plan".
* In the "**Operate**" phase, the honeypot is in operation and is under attack.
* In the "**Monitor**" phase, the honey pot collects safety data in a production environment, so that it can be analysed. The honey pot can also be coupled with other systems so that countermeasures are taken. Honeypot network traffic can be monitored by a NIDS that will be able to identify a potentially dangerous event. The honey pot can also have its own probes and send the collected data directly to a SIEM for comparison with a threat and vulnerability database. Finally, if an anomaly is discovered, a SOAR will allow the necessary countermeasures to be deployed depending on the type of threat. 
* Once this data has been collected, the "**Plan**" phase allows you to plan the integration of modifications and countermeasures in the next phases of the evolution of the life cycle.

# Glossary :
CI: Continuous Integration  
CD: Continuous Deployment
CS: Continuous Security : Extension of DevOps practices that integrates security into the CI/CD pipeline. Accelerates the delivery of features, while automating security requirements, leading to better governance and security. [^4]  
IDS : Intrusion Detection System  
NIDS : Network Intrusion Detection System  
SIEM : Security information and event management  
SOAR : Security Orchestration, Automation and Response  

# References
[^1]: A. Pathak (2022). Dive into the different phases of the DevOps lifecycle. https://geekflare.com/fr/devops-lifecycle/  
[^2]: S. Dupont, G.Ginis (2021). https://github.com/cetic/devsecops/blob/master/devsecops.svg  
[^3]: H. Benchrifa (2021). OPERATE - Penetration testing and SOAR. https://github.com/cetic/devsecops/blob/master/SOAR/Operate.md  
[^4]: Continuous security within DevSecOps. https://snyk.io/learn/what-is-ci-cd-pipeline-and-tools-explained/continuous-security/