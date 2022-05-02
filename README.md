# cis221_codepath

# Honeypot Assignment

**Time spent:** **X** hours spent in total

**Objective:** Create a honeynet using MHN-Admin. Present your findings as if you were requested to give a brief report of the current state of Internet security. Assume that your audience is a current employer who is questioning why the company should allocate anymore resources to the IT security team.

### MHN-Admin Deployment (Required)

**Summary:** How did you deploy it? Did you use GCP, AWS, Azure, Vagrant, VirtualBox, etc.?
1. Start new project in GCP.
2. Create wide-open firewalls rules to allow incoming traffic.
3. Create MHN-Admin VM.
4. Install MHN Admin application with GUI accessible via a web browser using the MHN-Admin ip address.
![mhn-admin deployment-gui](https://user-images.githubusercontent.com/98624766/166303962-8e4fa917-d101-4dab-8f5c-6d4fbccec66f.gif)

### Dionaea Honeypot Deployment (Required)

**Summary:** Briefly in your own words, what does dionaea do?
Dionaea is a decoy server that is used to attract would-be malicious actors into trying to exploit its vulnerable services and capture these findings.
1. Create honeypot VM in GCP
2. Install Dionaea by coping the wget script in mhn-admin gui.
3. Paste into honeypot-1 server
![dionaea](https://user-images.githubusercontent.com/98624766/166306537-b3ff4787-05d2-4159-980d-475d07ff1c1e.gif)

### Database Backup (Required) 

**Summary:** What is the RDBMS that MHN-Admin uses? What information does the exported JSON file record?

*Be sure to upload session.json directly to this GitHub repo/branch in order to get full credit.*

### Deploying Additional Honeypot(s) (Optional)

#### X Honeypot

**Summary:** What does this honeypot simulate and do for a security researcher?

<img src="x-honeypot.gif">

### Malware Capture and Identification (Optional)

#### X Malware

**Summary:** How did you find it? Which honeypot captured it? What does each malware do?

MD5 Hash: *Run `md5sum` on the file and record the hash here.*

SHA1 Hash: *Run `sha1sum` on the file and record the hash here.*

<img src="x-malware.gif">

## Notes

Describe any challenges encountered while doing the assignment.

Sometimes mhn gui would not load. 
mhn gui map never loaded.
GCP VMs would not start from suspend. Error mentioned not enough resources. Had to delete VMs and start a new cluster. 
