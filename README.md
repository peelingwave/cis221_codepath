# cis221_codepath

# Honeypot Assignment

**Time spent:** **X** hours spent in total

**Objective:** Create a honeynet using MHN-Admin. Present your findings as if you were requested to give a brief report of the current state of Internet security. Assume that your audience is a current employer who is questioning why the company should allocate anymore resources to the IT security team.

### MHN-Admin Deployment (Required)

**Summary:** How did you deploy it? Did you use GCP, AWS, Azure, Vagrant, VirtualBox, etc.?

The following are summary steps I used to deploy MHN-Admin VM in GCP (I used the installation scripts provided by codepath as seen in gif below):
1. Start new project in GCP.
2. Create wide-open firewalls rules to allow incoming traffic. 
3. Create MHN-Admin VM.
4. Install MHN Admin application with GUI accessible via a web browser using the MHN-Admin ip address.
![mhn-admin deployment-gui](https://user-images.githubusercontent.com/98624766/166303962-8e4fa917-d101-4dab-8f5c-6d4fbccec66f.gif)

### Dionaea Honeypot Deployment (Required)

**Summary:** Briefly in your own words, what does dionaea do?

Dionaea is a decoy server that is used to attract would-be malicious actors into trying to exploit its vulnerable services and capture these findings.

The following are summary steps to deploy the honeypot VM:
1. Create honeypot VM in GCP
2. Install Dionaea by coping the wget script in mhn-admin gui.
3. Paste into honeypot-1 server
![dionaea](https://user-images.githubusercontent.com/98624766/166306537-b3ff4787-05d2-4159-980d-475d07ff1c1e.gif)

### Database Backup (Required) 

**Summary:** What is the RDBMS that MHN-Admin uses? What information does the exported JSON file record?

MHN-Admin uses mongoDb as its RDBMS. The JSON file records information from attacks on my honeypot servers, ie timestamps, source ip, source port, destination port, which honeypot it attacked, and the protocol type of the attack. 

### Deploying Additional Honeypot(s) (Optional)

#### Honeypot Suricata

**Summary:** What does this honeypot simulate and do for a security researcher?

Suricata is described as a Intrusion Detection System (IDS), Intrusion Prevention System (IPS), and a Network System monitor (NSM). Security researchers and analysts use this tool to detect, identify, and prevent malicious breaches into a network. 
![mhn gui suricata](https://user-images.githubusercontent.com/98624766/166341451-468292f9-be69-4dc0-b3f4-687bcc1bc9d7.gif)

#### Honeypot Snort
Snort is a also an Intrusion Prevention System (IPS). Security researchers use this tool to prevent network breaches from malicious actors. 
![mhn gui snort](https://user-images.githubusercontent.com/98624766/166341875-8f1a54ba-41e0-4001-af0b-c750a236ee58.gif)


### Malware Capture and Identification (Optional)

#### Wannacry 

**Summary:** How did you find it? Which honeypot captured it? What does each malware do?
I found it in the payloads section in the MHN-Admin GUI. I copied the MD5 hash and searched on Virustotal.com. There the community had writeups explaining the severity of the attack as well as a description. 


MD5 Hash: *Run `md5sum` on the file and record the hash here.* C27ecb1de9ca748605af567237eeed4f 
SHA1 Hash: *Run `sha1sum` on the file and record the hash here.* f3b0fed4b1ba6da067663fed061d1ba03c883ab4
<img src="x-malware.gif">

Screenshot of GCP VMs and MHN-Admin
![GCP_screenshot](https://user-images.githubusercontent.com/98624766/166342877-57bd588c-3ad4-42ab-b481-c5691f80d4f1.png)

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
