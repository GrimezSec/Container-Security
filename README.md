# Container-Security
Collection of workflows, tools and informations about Container Security

# Introduction
## What is a Container?
A container is an isolated environment for your code. This means that acontainer has no knowledge of your operating system, or your files. Containers have everything that your code needs in order to run, down to a base operating system. But containers and applications must configurated to working together.
![VM and Container Deployments](https://www.veritis.com/wp-content/uploads/2019/09/virtual-machine-and-container-deployments.jpg)
<p align="center">Differences between VM and Container Deployment </p>

![image](https://github.com/GrimezSec/Container-Security/assets/128565483/fd2bbc26-c6a6-4e49-9250-2bcc52b17313)
<p align="center">Container Technology Architecture Tiers and Components </p>

## What is Container Security?

Container security refers to measures and practices taken with the goal of ensuring the safety and integrity of containers. Container security comprises everything from the applications inside the containers to the infrastructure they run on. Base image security and quality are critical to ensure that any derivative images come from a trusted source. Build security in your container pipeline by gathering trusted images, managing access with the use of a private registry, integrating security testing and automating deployment, and continuously defending your infrastructure. Container hardening is the process of using container scanning tools to detect possible vulnerabilities and addressing them to minimize the risk of attack.
 
 Robust container security reduces the risk of deploying a container that contains a security flaw or malicious code into a production environme

## Levels of Container 

## Types of Container Security Solutions

## Core Threats
   1. Data Breaches: Container security often revolves around data protection. Data breaches occur when malicious users or processes gain unauthorized access to sensitive data stored within containers.
      
   2. Insecure Base Images: Using outdated or unpatched base images increases the risk of vulnerabilities being introduced into the container. This can potentially allow attackers to compromise the container's security.
  
   3. Untrusted Image Registries: When containers are pulled from untrusted registries, there is a risk that malicious images may be introduced into the container environment.

   4. Container Escape Vulnerabilities: Container escape vulnerabilities allow attackers to break out of the container and gain access to the host system.
      
   5. Misconfigurations: Containers often run with excessive privileges or weak security configurations. Misconfigurations in these areas can potentially allow attackers to compromise the container's security.
    
   6. Lack of Regulatory Compliance: Organizations must comply with various regulatory and compliance requirements. Non-compliance with these regulations can lead to security breaches and other consequences.
    
   7. Insider Threats: Containers often operate in highly privileged environments, making them particularly susceptible to insider threats. Unauthorized insiders with access to containers could potentially exploit vulnerabilities to compromise security.
    
   8. Third-Party Vulnerabilities: Third-party components integrated into containers can introduce vulnerabilities that attackers could exploit. These components often have a smaller user base compared to core components, increasing the risk of such vulnerabilities.
    
   9. Complexity: Containers can become complex, leading to a high risk of vulnerabilities being introduced into the system. The more complex a container environment becomes, the higher the risk of a security breach.
    
   10. Container Orchestration and Service Mesh: While these technologies help automate and manage container operations, they can introduce vulnerabilities and increase the risk of a security breach.




## Container Security Practices
• Use container-specific host OSs instead of general-purpose ones to reduce attack surfaces: A container-specific host OS is a minimalist OS designed to only run containers. Using these OSs greatly reduces attack surfaces, allowing fewer opportunities for your containers to be compromised.
Some of Container Specific Operating Systems:
-[CoreOS](https://fedoraproject.org/coreos/)
-[Flatcar](https://www.flatcar.org/)
-[K3OS](https://k3os.io/)
-[Bottlerocket](https://aws.amazon.com/bottlerocket/)
-[Talos Linux](https://www.talos.dev/)
-[Kairos](https://kairos.io/)


• Only group containers with the same purpose, sensitivity, and threat posture on a single host OS kernel to allow for additional in-depth defense: Segmenting containers provides additional defense in-depth. Grouping containers in this manner makes it more difficult for an attacker to expand potential compromises to other groups. It also increases the likelihood that compromises will be detected and contained.

• Adopt container-specific vulnerability management tools and processes for images to prevent compromises: Traditional tools make many assumptions that are misaligned with a containerized model, and are often unable to detect vulnerabilities within containers. Organizations should adopt tools and processes to validate and enforce compliance with secure configuration best practices for images – including centralized reporting, monitoring each image, and preventing non-compliant images from being run.

• Consider using hardware-based countermeasures to provide a basis for trusted computing: Extend security practices across all tiers of the container technology by basing security on a hardware root of trust, such as the Trusted Platform Module (TPM).

• Use container-aware runtime defense tools: Deploy and use a dedicated container security solution capable of monitoring the container environment and providing precise detection of anomalous and malicious activity within it.

## Container Security Architecture

# Container Security Checklist

## Secure the Build Pipeline

- [x] Verify the image source (registry)
- [x] Use official base images 
- [x] Lock down access to the image registry (who can push/pull) 
- [x] Scan container image layers for Common Vulnerabilities and Exposures (CVEs) 
- [x] Scan configuration files for security and compliance checks in continuous integration (CI)
- [x] Do a static analysis of the code and libraries used by the code to surface any vulnerabilities in the code and its dependencies
- [x] Tag and automatically prevent vulnerable images from running in certain clusters or prevent them from talking to other containers in the cluster 


## Secure the Host
- [x] Lock down the operating system (like Google’s Container Optimized OS (COS)) 
- [x] Use secure computing (seccomp) to restrict host system call (syscall) access from containers
- [x] Use Security-Enhanced Linux (SELinux) to further isolate containers 
- [x] Utilize container sandboxing projects like gVisor, Kata Containers, etc. to reduce the attack surface


## Secure the Container Runtimes and Configure Admission Control

- [x] Ensure security configurations span across container runtimes, especially if the environment has multiple container runtimes in the cluster (for example, different runtimes for the orchestrator control plane and workloads)
- [x] Use policies (for example, pod security policy in Kubernetes) to restrict which containers can run in the cluster including policies to restrict privileged containers, containers that don’t need write access to a specific volume, and containers that need certain syscalls
- [x] Restrict access to container runtime daemon/APIs


## Secure the Network 

- [x] Secure services that are exposed to the Internet using a firewall 
- [x] Lock down Layer 3 and 4 access for the services using network policy
- [x] Create granular Layer 7 policies using service mesh (such as Istio)
- [x] Use Mutual Transport Layer Security (mTLS) to mutually authenticate containerized workloads (for example, using Istio)
- [x] Segregate containerized workloads with a mix of host segregation and network isolation (for example, separate group of hosts for workload segregation and/or network policies to isolate different group of containerized workloads) 
- [x] Log unsuccessful connection attempts

## Secure the Orchestrator Configuration

- [x] Implement version control for orchestrator service definitions and configurations (using git) for auditing
- [x] Ensure cluster-level policies (such as security policies, network policies, and so on) go through your change request, review, and approval process
- [x] Implement orchestrator API access security using role-based access control (RBAC) and network policies
- [x] Be aware of which third-party plugins (such as Container Network Interfaces [CNIs], Container Storage Interface [CSIs], and Container Runtime Interfaces [CRIs]) are running (binary/DaemonSet/controller), what access they have, and whether they are running as privileged containers
- [x] Control access to the orchestrator control plane APIs from third-party plugins using RBAC and service accounts
- [x] Enable access logs for all API requests to the orchestrator control plane (for example, audit logs in Kubernetes)  
- [x] Scan orchestrator manifests for containerized apps (such as Kubernetes deployment manifests) for security best practices and applicable compliance standards in the CI phase 
- [x] If you have any sensitive configuration information in your cluster that needs to be accessed by containers at runtime make sure the configuration is encrypted (such as encrypted secrets in kubernetes)
- [x] Rorate encryption keys that are used for communication between orchestrator components (for example kubernetes API server and etcd)


## Secure the Cloud Environment

- [x] If you’re running your containers in a cloud, remember the default security configuration (for orchestrator, container runtime, and operating system) can be different for different cloud providers 
- [x] Understand the version of orchestrator and container runtime components your cloud provider is running by default, and whether those components are modified from their open source version
- [x] Scan environment deployment configurations (such as Terraform, Cloud Formation templates, and Azure ARM templates) for security best practices and compliance misalignments 


## Secure the Data

- [x] Use a proper filesystem encryption technology for container storage
- [x] Provide write/execute access only to the containers that need to modify the data in a specific host filesystem path
- [x] Reduce write/execute filesystem access for the host filesystem to a minimum using constructs like Pod Security Policy (for example, only allowing Read-only Root Filesystem access, listing allowed host filesystem paths to mount, and listing allowed Flex volume drivers) 
- [x] Automatically scan container images for sensitive data such as tokens, private keys, and so on, before pushing them to a container registry (can be done locally and in CI) 
- [x] Limit storage related syscalls and capabilities to prevent runtime privilege escalation 
- [x] Log all successful and unsuccessful attempts to access sensitive data


## Secure Workloads
## Application Testing (SCA - SAST - DAST - SBOM)
•SCA: Software Composition Analysis (SCA) is an application security methodology in which development teams can quickly track and analyze any open source component brought into a project. Simply put, SCA is used to scan your dependencies for security vulnerabilities.

•SAST: Static application security testing (SAST), or static analysis, is a testing methodology that analyzes source code to find security vulnerabilities that make your organization’s applications susceptible to attack. SAST scans an application before the code is compiled. It’s also known as white box testing.

•DAST: Dynamic application security testing (DAST) is a type of black-box testing that checks your application from the outside. Software systems rely on inputs and outputs to operate. A DAST tool uses these to check for security problems while the software is actually running

•SBOM: Software Bill of Materials (SBOM) is a list of all the components that are used in a software application. The SBOM helps identify any vulnerabilities and potential security risks in the software supply chain.

## Container Networking
## Common Mistakes to Avoid
## Dockerfile / Docker Container Testing

# Container Security Tools

| Name | URL | Description |
| :---------- | :---------- | :---------- |
| **Harbor** | [https://github.com/goharbor/harbor](https://github.com/goharbor/harbor) | Trusted cloud native registry project|
| **Anchore** | [https://github.com/anchore/anchore-engine](https://github.com/anchore/anchore-engine) | Centralized service for inspection, analysis, and certification of container images |
| **Clair** | [https://github.com/quay/clair](https://github.com/quay/clair) | Docker vulnerability scanner|![Clair](https://img.shields.io/github/stars/goharbor/harbor?style=for-the-badge) | 
| **Deepfence ThreatMapper** | [https://github.com/deepfence/ThreatMapper](https://github.com/deepfence/ThreatMapper) | Apache v2, powerful runtime vulnerability scanner for kubernetes, virtual machines and serverless. | 
| **Docker bench** | [https://github.com/docker/docker-bench-security ](https://github.com/docker/docker-bench-security ) | Docker benchmarking against CIS|
| **Falco** | [https://github.com/falcosecurity/falco](https://github.com/falcosecurity/falco) | Container runtime protection |
| **Trivy** | [https://github.com/aquasecurity/trivy](https://github.com/aquasecurity/trivy) | Comprehensive scanner for vulnerabilities in container images |
| **Notary** | [https://github.com/notaryproject/notary](https://github.com/notaryproject/notary) | Docker signing|
| **Cosign** | [https://github.com/sigstore/cosign](https://github.com/sigstore/cosign) | Container signing|
| **watchtower** | [https://github.com/containrrr/watchtower](https://github.com/containrrr/watchtower) | Updates the running version of your containerized app |
| **Grype** | [https://github.com/anchore/grype](https://github.com/anchore/grype) | Vulnerability scanner for container images (and also filesystems). 
# Integrating and Automating Container Security Workflows
