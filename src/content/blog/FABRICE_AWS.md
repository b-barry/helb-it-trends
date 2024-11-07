---
title: Python Package "Fabrice" Steals AWS Credentials
pubDate: 2024-11-07 22:30
author: "EL BOUCHTILI Imaddine"
tags:  
  - Python
  - Security
  - AWS
  - Malware
imgUrl: '../../assets/python_logo.png'
description: A recent malware package on PyPI has been found stealing AWS credentials.
layout: '../../layouts/BlogPost.astro'
---

## Python Package "Fabrice" Steals AWS Credentials

### Overview

In a concerning development for the Python programming community, a malware package named **"Fabrice"** has been discovered on the Python Package Index (PyPI). This package contains malicious code that stealthily steals Amazon Web Services (AWS) credentials from unsuspecting users.

### Discovery of "Fabrice" Malware

Security researchers recently identified that "Fabrice" was uploaded to PyPI as a seemingly legitimate Python package. However, upon closer inspection, the package was found to contain harmful code designed to **exfiltrate sensitive AWS credentials** from any environment it was installed on. The credentials could then be used to gain unauthorized access to cloud resources, potentially leading to significant data breaches and financial costs for affected organizations.

### How It Works

The malicious code in "Fabrice" operates by searching for AWS credentials in the host environment. Once it finds these credentials, the malware attempts to send them to an external server controlled by the attackers. This kind of attack, known as **supply chain attack**, targets the software development lifecycle, exploiting the trust that developers place in popular package repositories like PyPI.

### Protecting Against Such Attacks

#### 1. Carefully Review Packages Before Installation
   - Verify the author, source, and version of any package before installing it.
   - Stick to well-known and widely-used libraries whenever possible.

#### 2. Use Credential Management Tools
   - Tools like AWS Secrets Manager or HashiCorp Vault securely store and manage sensitive information like AWS credentials.
   - Avoid storing credentials in plain text within your development environment.

#### 3. Regularly Monitor and Audit Installed Packages
   - Regularly check the packages installed in your projects to identify and remove any that may be potentially harmful.

#### 4. Employ Security Tools
   - Use dependency management tools that automatically detect and prevent the installation of packages with known vulnerabilities.
   - Consider using static code analysis tools to inspect the code of any third-party libraries you include.

### Conclusion

The "Fabrice" package is a reminder of the increasing sophistication of threats facing developers and businesses today. Ensuring robust security practices in the development pipeline, from credential management to package vetting, is essential to safeguard sensitive data and avoid costly breaches. For developers and organizations relying on cloud services like AWS, staying vigilant about the packages in use has never been more crucial.

--- 


Source : [Developer Tech - Python Package Fabrice](https://www.developer-tech.com/news/python-package-fabrice-steals-aws-credentials/)