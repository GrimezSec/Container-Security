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

## Levels of Container Security

## Types of Container Security Solutions

## Core Threats

## Container Security Practices
• Use container-specific host OSs instead of general-purpose ones to reduce attack surfaces: A container-specific host OS is a minimalist OS designed to only run containers. Using these OSs greatly reduces attack surfaces, allowing fewer opportunities for your containers to be compromised.
### Some of Container Specific Operating Systems
[CoreOS](https://fedoraproject.org/coreos/)
[Flatcar](https://www.flatcar.org/)
[K3OS](https://k3os.io/)


• Only group containers with the same purpose, sensitivity, and threat posture on a single host OS kernel to allow for additional in-depth defense: Segmenting containers provides additional defense in-depth. Grouping containers in this manner makes it more difficult for an attacker to expand potential compromises to other groups. It also increases the likelihood that compromises will be detected and contained.

• Adopt container-specific vulnerability management tools and processes for images to prevent compromises: Traditional tools make many assumptions that are misaligned with a containerized model, and are often unable to detect vulnerabilities within containers. Organizations should adopt tools and processes to validate and enforce compliance with secure configuration best practices for images – including centralized reporting, monitoring each image, and preventing non-compliant images from being run.

• Consider using hardware-based countermeasures to provide a basis for trusted computing: Extend security practices across all tiers of the container technology by basing security on a hardware root of trust, such as the Trusted Platform Module (TPM).

• Use container-aware runtime defense tools: Deploy and use a dedicated container security solution capable of monitoring the container environment and providing precise detection of anomalous and malicious activity within it.

## Container Security Architecture

# Container Security Checklist

## Secure Build
## Secure Container Registry
## Secure container Runtime
## Secure Workloads
## Application Testing (SCA - SAST - DAST - SBOM)
## Container Networking
## Common Mistakes to Avoid
## Dockerfile / Docker Container Testing

# Container Security Tools

# Integrating and Automating Container Security Workflows
