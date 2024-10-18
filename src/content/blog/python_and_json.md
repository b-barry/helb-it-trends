---
title: How to work with JSON Data in Python ? 
pubDate: 12/10/2024 19h20
author: "Bagci Izla"
tags:
  - JSON
  - Python
description: Using JSON with Python.
layout: '../../layouts/BlogPost.astro'
---

# How to work with JSON Data in Python? 

Do you know what JSON means? JSON is for: JavaScript Object Notation. This format is used to share informations thanks to its minimalistic and efficient format.

This natural format facilitates sharing information between applications. The shared informations are between a web client and server.
JSON is human-friendly and machine-readable, thank's to the both format, parsing, generating and understanding the file is easy.

Moreover, JSON is: 
- Lightweight: the file is not that heavy and it's suitable for transmitting data over networks.
- Text-based: it's a plain-text format with readable symbols and characters, and this is language independent and compatible with a majority of modern programming languages.
- Structured data: representation of data as "key-value"

  
JSON performance: 
- API interaction: mostly, applications coded in Python use JSON to send and receive response.
- Data Storage: is utilized to store and exchange data both within various components of a system and between different systems. Examples include configuration files and logs.
- Serialization and Deserialization: converion of data structures into string format, this process is called "serialization". Afther this process, JSON deserializes the data, this is reconstructing data into their original form.
This two step process facilitates data sharing and interchange.


Concerning Python, to use JSON, you just need to import json like this: *"import json"* and therefore you have access to all json methods.

1. Loads data: *"json.loads()"* 
   
2. Access to nested data : nested data means that the dictionaries or list is included into the data. These lists or dicitonnaries can contains multiple dictionaries and lists.
3. Read and Write into a JSON data : with *"json.dumps()"* converts Python objects into a **JSON-formatted string**. The data is serialized, written into a file or transmitted over network.
4. Pretty printing : when using the *"json.dumps()"*, it's possible to add a second parameter which is the ident. This allows to use an indentation of 2 or 4 which are the most used.


To end, JSON is used by many developers with many programming languages due to its format which is: light, human readable and machine readable.

To have demonstration, you can click here: [working with JSON Data in Python](https://thenewstack.io/working-with-json-data-in-python/)

