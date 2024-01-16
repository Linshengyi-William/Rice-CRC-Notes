
## Introduction 
In this document, we show Rice folks how to use various high-performance computing(HPC) and high-throughput computing(HTC) resources, including virtual machines, RDF, and NOTs.

## Using ssh Keys
You will have to use ssh-keygen to ensure secure connections to the following resources.  Use the following bash commands to make a directory for your ssh key(if you don't have one already), move into that directory, and then generate a key.

```
mkdir .ssh //if .ssh doesn't exist
cd .ssh
ssh-keygen
```

#### Types of ssh Keys:
- Public
    - Use for everything
- Private 
    - Longer… 
    - Do NOT show to anyone

## ORION and RDF
ORION (Owl Research Infrastructure Open Nebula) is a virtual machine pool on Rice’s campus.

Virtual machines come with more computing power than typical linux systems, but not as much as systems like NOTs. In order to receive access to ORION, you must apply via the CRC.

#### Logging onto Orion
Visit this link to log into Orion using netid and password:

orion.crc.rice.edu 

Ssh netid@(IP address for VM)Authtication with SSH

Settings > Auth > public ssh key
Trouble with adding ssh key? →  Tell bash where ssh is:

```
eval $(ssh-agent)
```

##### Login to VM

ssh netid@(IP address for VM)

#### Accessing the Research Data Facility [RDF](https://kb.rice.edu/page.php?id=108256)
The Research Data Facility (RDF) is a network that enables file sharing across Rice-connected servers.  Instructions for utilizing the RDF slightly differ based on Mac/Windows.

##### Mac:
1. Go to Finder
2. command+k to find server
3. smb://smb.rdf.rice.edu/research → server name
Netid, password to login

##### Mount:
The mount function is to get the VM and RDF to talk to each other. 

*When VM is up* 
```
mount/mnt
```

##### What does this all mean? 
The RDF and ORION are super powerful together

- RDF nearly infinite harddrive extended to computer
- ORION is step above laptop but below supercomputer 

## [NOTS](https://kb.rice.edu/page.php?id=108237)

For jobs that require larger computing resources, we show how to connect and utilize Rice’s supercomputing cluster, NOTs.

First, in order to access NOTS, you will need CRC access and must be connected to the Rice Owls WiFi.  Assuming these requirements are met, following are the bash commands to connect to NOTs and run jobs:

#### NOTS Architecture (via CRC documentation)

![somefillertext](https://kb.rice.edu/images/group273/108446/loginDiagram2.png)







