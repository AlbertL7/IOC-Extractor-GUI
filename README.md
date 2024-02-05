# IOC-Extractor-GUI

There are a lot of IOC extractor programs out there but none that I could find that integrate a GUI that you do not have to pay for at least.

So I decided to make an IOC extractor myself that also integrates with virus total for easy analysis. I recently found myself using it at my job to not only analyse IOC's in Articles found on the internet but to comb through email headers and pick out the different email addresses and IP addresses associated to the email. Another main use for this application at work that I found helpful is extracting IOC's from Internet articles or CTI reports that come in and require review. It makes life a little bit easier. You can combine this with the Poor-Mans-Cyber-Threat-Feed applications I made to create a very cheap cyber threat feed. https://github.com/AlbertL7/The-PoorMans-Cyber-Threat-Feed

## Features
### IOC Parsing
- IPv4 Address Extraction: Identifies and extracts IPv4 addresses, supporting standard and defanged formats.
- Domain/Subdomain Extraction: Extracts domain and subdomain data, again supporting both standard and defanged formats.
- URL Detection: Identifies full URLs, catering to various schemes (http, https, ftp, etc.), and defanged formats.
- IP in URL Extraction: Extracts URLs containing IP addresses.
- Hash Extraction: Supports the identification of MD5, SHA1, and SHA256, SHA512, and SSDEEP hashes.
- CVE Extraction: Recognizes and extracts Common Vulnerabilities and Exposures (CVE) identifiers.
- File Name Extraction: Extracts file names based on a list of file extensions found inside quotes or outside of quotes.
- Email Address Extraction: Identifies and extracts email addresses, considering defanged formats.
- Registry Key Extraction: Extracts Windows registry keys.
- MAC Address Extraction: Identifies and extracts MAC addresses.
- Bitcoin Address Extraction: Extracts potential Bitcoin addresses.
- Dark Web identification of '.onion' addresses
- YARA Rule Extraction: Identifies and extracts YARA rules.
- Will also do IPv6 but is commented out because it matches on basically everything that has a colon in it. Uncomment to use if IPv6 addresses are present in droves.

### User Interface
- Interactive Text Input: Users can paste or input text for analysis.
- IOC Review: Extracted IOCs are displayed for review.
- Text Highlighting: Highlights the relevant IOCs that have been matched in the input text area for easy review.
- Regex match input text with find and replace capabilities.
  
### IOC Interaction
- Defanging: Converts standard IOCs into a 'defanged' format, making them non-clickable and safe for sharing.
- Saving Functionality: Allows IOCs to be saved either as a group or individually.
- IOC Modification: Users can add or remove IOCs manually.
  
### Integration with VirusTotal
- VirusTotal Analysis: Provides options to check URLs, file hashes, and IP addresses against VirusTotal's database.
- VirusTotal Submission: Allows users to submit URLs for scanning.
- VirusTotal Hash Retrieval: Retrieves various hash types for given samples. Mainly useed if you only have md5 or sha1 hashes and you need sha256 to conduct a threat hunt in your environment
- MITRE ATT&CK Information: Retrieves MITRE ATT&CK techniques associated with a particular file or URL

### Example Usage
- Grabbed an article online with IOC's copy and pasted the entire thing and parsed. Ran URL's / Subdomains through Virus Total API and came up with malicious hits.
![image](https://github.com/AlbertL7/IOC-Extractor-GUI/assets/71300144/62ac9909-d9b9-4e77-9dda-a2c215867c73)

## Possible Future Updates
- Create an SQL backend to query past saved IOC's easily.
- Integrate more VirusTotal API features (grab sigma rules based on file behavior)
- Integrate Rate limiting for VirusTotal API
- Possible make the output text interactive and remove "remove ioc" buttons

## Warning 
- There is no rate limiting for the VirusTotal API queries so if you are submitting a giant amount of hashes / URL's for analysis you may cause a DOS on VirusTotal and get your IP blocked.

## Testing / Help
- I really want to make this a great and daily use application, so any help / ideas to make this application better is appreciated, feel free to fork or request commits!

## Problems
- The buttons will overlap and change position based on OS and other factors, working to fix this.

Credits: Developed by AlbertL7 with help from ChatGPT4
