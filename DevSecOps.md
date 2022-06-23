# DevOps 

DevOps is a modern philosophy that emerged in 2007 that consists in reducing the life cycles of software development. It was born on the one hand of a desire to use and globalize agile methods in development processes. On the other hand, it helps to address organisational and collaborative problems between development and operational departments which may have repercussions on performance and quality.

"Dev" refers not only to developers but to the entire team involved in developing a software solution. It combines practices, people, tools, technologies and processes from different disciplines, such as planning, testing, quality assurance, etc. Similarly, "Ops" refers to all members of the operations team : system administrators, system engineers, database administrators, operating personnel, publishing engineers, etc. [^1]

DevOps to promote the automation and monitoring of each step of application creation, from development, integration, testing, delivery to deployment, operation and maintenance of systems in a continuous pipeline. 

![DevOps: Lifecycle](/IMAGES/DevOps.PNG)
<b> Fig.1 - DevOps lifecycle  </b> [^2]     

# DevSecOps

Safety has long been considered an activity that begins after production and has sometimes never been considered until problems arise on the final product.

DevOps principles often do not integrate safety teams into their CI/CD pipeline. Adding security to the pipeline translates into secure applications from the design stage (by design), which reduces the costs of its implementation, as the safety problems and the financial and reputational damage they will cause are much less.

DevSecOps is therefore the answer to the integration of security in the early design and production phases as it aims to increase speed and reduce the frequency of bugs and security issues and their impact on production. 

Concretely, DevSecOps solves these problems by placing security earlier in the application development lifecycle to reduce vulnerabilities and bring security closer to objectives through threat modeling, intrusion testing exercises and, to some extent, security monitoring, and the automation of incident responses when considering the SIEM/IDS and SOAR tools. [^3]

To this end, it is interesting to integrate a honeypot soltuion allowing to evaluate the safety of the components during the life cycle of the development of an application. A Honeypot makes it possible to study both the behavior of attackers in terms of implemented security techniques, but also to highlight possible fail and vulnerability.

![DevSecOps: Lifecycle](/IMAGES/DevSecOps.jpg)
<b> Fig.2 - DevOps lifecycle and details </b> [^2]     

In the DevSecOps lifecycle, the honeypot finds its place in 2 key steps, namely "monitoring" and "plan". The honeypot, coupled with an IDS and SIEM system, allows the collection of security-related data in a production environment. Once this data is collected, it allows you to plan the changes made during the programming and deployment phase (at the infrastructure level). 


# Glossary :
CI: Continuous Integration
CD: Continuous Deployment

## References
[^1]: A. Pathak (2022). Dive into the different phases of the DevOps lifecycle. https://geekflare.com/fr/devops-lifecycle/
[^2]: S. Dupont, G.Ginis (2021). https://github.com/cetic/devsecops/blob/master/devsecops.svg
[^3]: S. Dupont, G.Ginis (2021). OPERATE - Penetration testing and SOAR. https://github.com/cetic/devsecops/blob/master/SOAR/Operate.md
