---
title: "FoxHunter: Extracting Firefox Artifacts For Forensic Purposes"
subtitle: Extracting, analysing, attacking, and dumping Firefox browser
  artifacts on Linux platforms for forensic purposes
category:
  - Tools
author: Cameron Wickes
date: 2022-04-16T17:22:42.045Z
featureImage: /uploads/new-project-1-.png
---
*The Internet is one of the most ubiquitous technologies in use today, with over 4.95 billion users and 1,167,715,133 websites as of January 2022. To access this vast web of Internet content in circulation, consumers must use a web browser. Which browser a consumer chooses to utilise is often a personal preference. Still, the most popular options are Chrome, Safari, and Firefox on Windows, macOS, and Linux platforms, with most modern Linux distributions shipping with Mozilla Firefox as the default.* 

### Forensic Analysis of Web Browsers

When performing forensic analysis on hard drives, browsers are often gold mines of information containing information that is pertinent to a legal case. Through close inspection of a user's downloads, bookmarks, browsing history, and passwords, the source of incidents and infections can be traced down.

Web browser artifacts are all stored inside specific folders in the user's file system. These artifacts are stored in various formats, including SQL databases, LZ4 compressed files, and JSON formats. On Linux distributions running Firefox, the following artifacts can be found in the `~/.mozilla/firefox/` directory:

* Browsing History: Contains information about sites a user has visited.
* Bookmarks: Pages the user has chosen to favourite.
* Extensions and Addons: Any additional codebases users choose to install.
* Logins: Any login information for sites a user has chosen to save.
* Downloads: A list of filenames and sources for user downloaded files.
* Form History Data: Anything typed inside web forms that the user commonly enters.
* Cookies: Any cookies that identify the user's computer to a website.
* Certificates: Any installed files that validate a specific website's identity.

When doing some research into this, I found there were no open-source tools for extracting and analysing this type of data. Popular commercial tools like Magnet AXIOM and Autopsy only analysed a few of these artifacts, and specifically developed open-source tools like FirefoxDecrypt only tackled individual artifacts. 

### FoxHunter

In response to this, I have developed FoxHunter, a tool for extracting, analysing, attacking, and dumping Firefox browser artifacts on Linux platforms for forensic purposes.  

*FoxHunter extracts and dumps (into machine parseable formats):*

* Addons
* Bookmarks (Active & Deleted)
* Browsing History
* Browsing History Searches
* Certificates (x509)
* Cookies
* Downloads
* Extensions
* Form History
* Saved Logins (Encrypted)

*FoxHunter additionally allows users to decrypt extracted logins through:*

* Anonymous Authentication (Blank Password)
* Password Authentication (Known Factor)
* Brute Force Authentication (Wordlist/Dictionary Attack)

*Finally, FoxHunter performs analysis on gathered artifacts:*

* Identifies addons not installed through Mozilla store.
* Identifies addons with low download rates and/or ratings.
* Identifies out-of-date addons - potential security risks.
* Identifies extensions with interesting/abnormal permissions.
* Identifies certificates from relatively unknown issuers.
* Identifies certificates with weak/unrecommended encryption standards.
* Identifies deleted bookmarks.
* Identifies possible malware downloads by file name.
* Identifies common file download websites.
* Categorises downloads by file type.
* Produces graphs of user downloads over extended periods of time.
* Identifies interesting form history fields containing PII.
* Identifies commonly used form fields.
* Identifies commonly used login usernames and passwords.
* Identifies potential patterns within usernames or passwords.
* Identifies cookies with interesting values (Base64, Hex, GA Cookies).
* Identifies the most common browsing history searches.
* Identifies common browsing history searches.
* Identifies commonly used search engines.
* Identifies commonly used social media sites.
* Identifies times of the day when the user is most active.
* Identifies days of the week when the user is most active.

The tool is available on GitHub and can be found [here](https://github.com/cameronwickes/foxhunter).