
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

#### Logging into the cluster

```
mkdir .ssh
cd .ssh
ssh-keygen
ssh netid@nots.rice.edu
```

Upon logging into the cluster, your terminal should read:

#### File Systems in NOTS
The following figure, provided by the CRC’s NOTS [documentation](https://kb.rice.edu/page.php?id=108237), shows the characteristics of the different file systems in NOTS.

A good directory to start your NOTS work is: scratch 

To use Scratch to run a job you will need to move into the scratch directory and make a directory with your netid:

```
cd /scratch
mkdir netid
cd netid
```

Why are we using scratch?
Scratch is a file system designed specifically for lots of jobs going, and writing at same time.
This filesystem can handle the load for hundreds of users to be doing this work!!
Nfs filesystem does not perform as well as scratch
Bash command to see all of the file systems: 
```
df -hT
```

#### Virtual Environments Within NOTS
– why do we need these? –

Mac:
Create virtual environment:
```
python3 -m venv venv
activate venv
source venv/bin/activate
```

Windows:
```
source ./venv_example/
source ./venv_example/Scripts/
source ./venv_example/Scripts/activate
```


#### How to Submit Jobs on NOTS Using Own Computer
To bypass firewall(no VPN): 

```
ssh netid@gw.crc.rice.edu
```

**Reminder** Gateway servers have limited capacity. If you upload massive files, do it through VPN
Connect to NOTS through ssh

```
sbatch script.py 
```

To unload all environment variables:
```
module purge
```

#### Different Ways to Run Files (using parallel folding example)

Serial main.py
    - One argument
        - Number of vertices

Parallel main.py
    - Nice example because No input files
    - Don’t have to worry about multiple input files, indexing them, etc.
    - Three arguments
    - Number of vertices
    - Worker number
    - Number of workers

Taking the total amount of work
    - Runs by checkpoint 
    - Takes remaining work and splits in line 135 across 

#### Scavenger.slurm - Bash notes:
Slurm script → job script
Providing instructions on how to do job

**Embarrassing parallel (HPC)**

Problem you can break up into pieces with no required communication between chunks of the jobs
Can all run in parallel but no synchronization
Job scales linearly
    
**High throughput computing (HTC)**

When you solve the cluster problems with lots and lots of small problems
    
Lots of CPUs working at same time, synchronized
    
Work time will settle because there’s a minimum time for all serial components added together
    
Condor
    Open science grid
        
    Can submit job there ^ and job will run somewhere in the country
        
‘module load’ loads module

‘module spider GCC’ gets all the version of GCC that are installed on NOTs
    
‘srun’ will run the following thing eg ‘python3 main.py

**Crux of the slurm**

Taking the large job, splitting it across 50 jobs, so they’re all working on mini jobs in a **semi-parallel** way

Enables shorter wait times

#### What is Going on In NOTS?

Ssh into nots
```
s queue 
```
--> all the jobs that are running
Priority is jobs that are waiting
example:
    bc9…. is name of the server that is running on
    Room b, rack c9, shelf u19
    
Information keys:
    - r - running
    - pd - pending
    - ra47 - netID
    - TF99_S3_ name of the job
    
```
s info -p scavenge
```

Scavenge is the space available ~ Tells you what all of the nodes are using

Drain means not running job, taken offline

Resv means reserved (like for classes)

Mix means job is running on the node, but it is not all the way full and has some extra space

Alloc means completely full

Idle means idle
Depends on what kind of job you’re running
    Ex. if you want GPU, but servers dont have GPU, it would be idle…
    Maybe its idle because size, other servers empy, etc. i guess?

#### Run the Job from scratch in NOTS

```
pwd 
ls
cd scratch
dd netID
cp -R  /home/netID/parallel_folding_exmample/ .
ls, cd parallel
```

```
sbatch scavenger.slurm 10
```
→ submits job!!
```
squeue -netID
squeue -u netID
```
 → to see the job is going!






