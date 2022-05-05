# cis221_codepath

# Honeypot Assignment

**Time spent:** **20** hours spent in total

**Objective:** Create a honeynet using MHN-Admin. Present your findings as if you were requested to give a brief report of the current state of Internet security. Assume that your audience is a current employer who is questioning why the company should allocate anymore resources to the IT security team.

### MHN-Admin Deployment (Required)

**Summary:** How did you deploy it? Did you use GCP, AWS, Azure, Vagrant, VirtualBox, etc.?

The following are summary steps I used to deploy MHN-Admin VM in GCP (I used the installation scripts provided by codepath as seen in gif below):
1. Start a new project in Google Cloud Project (GCP).
2. Create firewalls rules to allow incoming traffic on ports. 
3. Create MHN-Admin VM via GCP cloudshell.
4. Install MHN Admin application with GUI accessible via a web browser using the MHN-Admin ip address.

Note: I used the tool Peek to record the gif, for some reason my pointer did not show up in the recordings.
![mhn-admin deployment-gui](https://user-images.githubusercontent.com/98624766/166303962-8e4fa917-d101-4dab-8f5c-6d4fbccec66f.gif)

### Dionaea Honeypot Deployment (Required)

**Summary:** Briefly in your own words, what does dionaea do?

Dionaea is a decoy server that is used to attract would-be mthreat actors into trying to exploit its vulnerable services and capture these findings.The firewall rules I created in GCP allow it to seem like an easy target from threat actors. 

The following are summary steps to deploy the honeypot VM (I used the installation scripts provided by codepath as seen in gif below):
1. Create honeypot VM in GCP cloudshell (not in the MHN-admin console).
2. Install Dionaea by copying the wget script in the mhn-admin gui under Deploy > Dionaea.
3. SSH into honeypot-1 console and paste the wget install script and run the command. 
![dionaea](https://user-images.githubusercontent.com/98624766/166306537-b3ff4787-05d2-4159-980d-475d07ff1c1e.gif)

### Database Backup (Required) 

**Summary:** What is the RDBMS that MHN-Admin uses? What information does the exported JSON file record?

MHN-Admin uses mongoDb as its RDBMS. The JSON file records information from attacks on my honeypot servers, ie timestamps, source ip, source port, destination port, which honeypot it attacked, and the protocol of the attack. 

### Deploying Additional Honeypot(s) (Optional)

#### Honeypot Suricata

**Summary:** What does this honeypot simulate and do for a security researcher?

Suricata is described as a Intrusion Detection System (IDS), Intrusion Prevention System (IPS), and a Network System monitor (NSM). Security researchers and analysts use this tool to detect, identify, and prevent malicious breaches into a network. Suricata was able to detect suspicious activity in my honeypot.
![mhn gui suricata](https://user-images.githubusercontent.com/98624766/166341451-468292f9-be69-4dc0-b3f4-687bcc1bc9d7.gif)

#### Honeypot Snort
Snort is a also an Intrusion Prevention System (IPS). Security researchers use this tool to prevent network breaches from malicious actors. 
![mhn gui snort](https://user-images.githubusercontent.com/98624766/166341875-8f1a54ba-41e0-4001-af0b-c750a236ee58.gif)

#### Honeypot Cowrie

Cowrie is a Telnet honeypot that logs bruteforce attacks and the shell interaction. It can emulate either a Unix system or as an ssh proxy. In MHN GUI I was able to see the attacks, including the attackers ip address and the credentials they attempted to use (username/password) to access priveleged accounts. 
![cowrie graphs](https://user-images.githubusercontent.com/98624766/166400313-628e9ed1-bceb-4cae-86d0-acb8113785ae.png)


### Malware Capture and Identification (Optional)

1.#### Wannacry

**Summary:** How did you find it? Which honeypot captured it? What does each malware do?

I found them in the payloads section in the MHN-Admin GUI. I copied the MD5 hashes and searched on Virustotal.com. There the community had writeups explaining the severity of the attack as well as a description. Wannacry is a type of ransomeware that attacks and exploits Windows and encrypts data on the computer in return for bitcoin. 

MD5 Hash: *Run `md5sum` on the file and record the hash here.* 

C27ecb1de9ca748605af567237eeed4f 

SHA1 Hash: *Run `sha1sum` on the file and record the hash here.* 

f3b0fed4b1ba6da067663fed061d1ba03c883ab4

https://www.joesandbox.com/analysis/573201/0/html

<img src="x-malware.gif">


Screenshot of GCP VMs and MHN-Admin
![GCP_screenshot](https://user-images.githubusercontent.com/98624766/166342877-57bd588c-3ad4-42ab-b481-c5691f80d4f1.png)
Screenshot of sensors in MHN GUI
![sensors](https://user-images.githubusercontent.com/98624766/166850684-8e2152e2-af76-41a8-83b5-03951e547bee.png)

Screenshot of Cowrie graphs in MHN-GUI
![cowrie_more](https://user-images.githubusercontent.com/98624766/166850712-7579ccf1-1a35-4665-8d26-4f0c846ec001.png)


## Notes

Describe any challenges encountered while doing the assignment.

Sometimes mhn gui would not load. 
mhn gui map never loaded.
GCP VMs would not start from suspend, an error mentioned not enough resources. I had to delete VMs and create new mhn admin and honeypots. 

Suricata honeypot would not install using deploy script. 
I ran into errors trying to deploy Suricata from the MHN GUI. I found this workaround to deploy it. https://github.com/pwnlandia/mhn/issues/798
1. Go to your MHN GUI > Deploy > Select Script > select Ubuntu - Suricata.
2. Cut the script below and paste into a text editor.
3. You need to add  "sed -i 's/-2.0/-5.0.0/g' Makefile.am" between lines 72 and 73. 
4. Paste the script back into the MHN GUI Deploy and press "update"
5. Copy the WGET and run in your MHN-admin console. 
Glastopf honeypot would not install. I was able to drill down and update the code but I came against an error that I could not overcome complaining about needing python a current version even though I was at the current version.
