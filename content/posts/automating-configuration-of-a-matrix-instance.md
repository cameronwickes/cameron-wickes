---
title: Automating Synapse & Matrix Instances
subtitle: Creating secure organisational communication channels within existing
  business infrastructure
category:
  - Research
author: Cameron Wickes
date: 2022-04-23T13:32:46.271Z
featureImage: /uploads/matrix.png
---
*The Matrix project has attracted a lot of attention in recent years, as it allows decentralised and federated communications to occur across a range of devices including Web, iOS, and Android platforms. It has support for a variety of features including end-to-end encrypted messaging, video calling and VoIP, leading to mass adoption within the United States Armed Forces and German Military.*

### *The Matrix Project*

Unfortunately, a vast number of companies in operation today use consumer-focused communication applications  to relay business-facing messages. Apps like WhatsApp and Messenger are widely used within the industry, and neither are ideal. Both are Meta-owned, and created to collect personal data relating to hundreds of users. Some businesses made the switch to apps like Signal, which have support for end to end encryption, however these channels are simply not suitable for large scale use. Alternatively, companies can utilise business-focused platforms like Slack to relay information. This is better than most settings, as it is designed for large scale use. However, some organisations are still unsure as it results in company data being stored on external servers. The Matrix project was set up to solve these problems. It provides a protocol standard for federated and decentralised communication, supporting a range of communication methods. It uses JSON over REST to transmit messages over business owned HTTPS channels. 

When performing a bit of research on this topic, I found there was not a suitable solution for automating the setup of the software required to create a business-facing solution. The closest I could find was [matrix-docker-ansible-deploy](https://github.com/spantaleev/matrix-docker-ansible-deploy), which automates the provisioning of a range of Matrix services over Ansible and Docker. This was unsuitable for a few reasons:

* It uses Docker to run Matrix services - Since Docker needs unrestricted root access to the system to run containers, this is not ideal.
* It separates NGINX and Let's Encrypt, making it harder to configure.
* MA1SD configuration doesn't recursively perform directory lookups, making it harder to find organisational users.
* Complex to setup correctly, and has relatively little inflexibility when it comes to adding to configuration files.

### Matrix-Automation

To solve the aforementioned problems, I've developed Matrix-Automation, an Ansible role for automating the installation and configuration of a Synapse deployment along with PostgreSQL databases, MA1SD Identity Servers and an NGINX proxy using Podman for organisational use.

It creates a functioning Synapse homeserver by configuring five rootless Podman containers:

* A PostgreSQL Database - To store Synapse data
* A Synapse Homeserver - To implement the Matrix protocol
* A MA1SD Identity Server - To handle third party ID mappings
* A MA1SD Extender API - To handle recursive directory lookups for MA1SD
* A Reverse Proxy - To direct traffic to the other containers as necessary

It supports LDAP and SSO integrations for login and user search, and can federate with other Synapse homeservers and identity servers.



If you're interested and would like to try it for yourself, visit the following links:

[Ansible-Galaxy Role](https://galaxy.ansible.com/cameronwickes/matrix_automation)

[GitHub Page](https://github.com/cameronwickes/matrix-automation)