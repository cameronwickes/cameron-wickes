---
title: Federating Matrix User Directory Lookups Using MA1SD
subtitle: Allowing Matrix user directory searches to be recursively federated
  for corporate use
category:
  - Research
author: Cameron Wickes
date: 2022-04-23T14:23:59.571Z
featureImage: /uploads/ma1sd_extender.png
---
*MA1SD is a federated Matrix identity server that maps Matrix IDs to Third-Party Identifiers (3PIDs) which connects to existing on-premise identity stores such as Active Directory, LDAP, SQL Databases and Web Applications. It implements the Matrix Identity-Service API and is designed for self-hosted Synapse instances.*



### *MA1SD Directory Search*

The MA1SD identity server has a feature which allows you to search for existing and/or potential users that are present in it's configured identity stores. By enabling the feature, it allows you to search on a variety of configured attributes, such as Matrix ID, Display Name, 3PID, and allows you to search for users you have not been in contact with yet, which is important for corporate use. Unfortunately, this means that the MA1SD identity server has to have all configured users in Identity stores. This may not be possible if the organisation has multiple offices, all with internal LDAP servers that are not exposed to the Internet. 



### MA1SD-Extender

A better solution would be to utilise the federation servers Synapse has been configured to use to build a bigger federated corporate directory, that has all organisational users in. This is what the MA1SD-Extender API allows organisations to do. 



The API, built with Docker and FastAPI, allows Matrix user directory searches to be recursively federated for corporate use. It performs the following sequence of actions to do this:

* Checks the validity of API supplied credentials
* Checks the validity of a user specified authorisation token against all federation domains
* Returns previously cached responses for faster lookups
* Searches within local directory for users
* Recursively searches other federation domains for users
* Returns pooled responses masquerading as the local MA1SD server



To achieve this, the API needs to be running, and the Synapse NGINX/Apache Reverse Proxy should be configured to point requests to the URL `/_matrix/client/r0/user_directory/search` to the extender running on port 8060.



MA1SD-Extender is available in a range of formats. To learn more, click on one of the following links:

[Docker/Podman image on the Docker Hub](https://hub.docker.com/repository/docker/cameronwickes/ma1sd-extender)

[Raw Source Code on GitHub](https://github.com/cameronwickes/ma1sd-extender/)