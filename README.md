# IOC-Extractor-GUI

There are a lot of IOC extractor programs out there but none that I could find that integrate a GUI that you do not have to pay for at least.

So I decided to make an IOC extractor myself that also integrates with VirusTotal for easy analysis and now includes integration with [jsluice](https://github.com/BishopFox/jsluice) and a general-purpose shell command executor.

I recently found myself using it at my job to not only analyse IOCs in Articles found on the internet but to comb through email headers and pick out the different email addresses and IP addresses associated to the email. Another main use for this application at work that I found helpful is extracting IOCs from Internet articles or CTI reports that come in and require review. It makes life a little bit easier. You can combine this with the Poor-Mans-Cyber-Threat-Feed applications I made to create a very cheap cyber threat feed. https://github.com/AlbertL7/The-PoorMans-Cyber-Threat-Feed

## Features

### IOC Parsing
* IPv4 Address Extraction: Identifies and extracts IPv4 addresses, supporting standard and defanged formats[cite: 3].
* Domain/Subdomain Extraction: Extracts domain and subdomain data, again supporting both standard and defanged formats[cite: 3].
* URL Detection: Identifies full URLs, catering to various schemes (http, https, ftp, etc.), and defanged formats[cite: 4].
* IP in URL Extraction: Extracts URLs containing IP addresses[cite: 4].
* Hash Extraction: Supports the identification of MD5, SHA1, SHA256, SHA512, and SSDEEP hashes[cite: 4].
* CVE Extraction: Recognizes and extracts Common Vulnerabilities and Exposures (CVE) identifiers[cite: 4].
* File Name Extraction: Extracts file names based on a list of file extensions found inside quotes or outside of quotes[cite: 4].
* Email Address Extraction: Identifies and extracts email addresses, considering defanged formats[cite: 5].
* Registry Key Extraction: Extracts Windows registry keys[cite: 5].
* MAC Address Extraction: Identifies and extracts MAC addresses[cite: 5].
* Bitcoin Address Extraction: Extracts potential Bitcoin addresses[cite: 5].
* Dark Web identification of '.onion' addresses[cite: 5].
* YARA Rule Extraction: Identifies and extracts YARA rules[cite: 5].
* (IPv6 is commented out by default due to potential noise but can be enabled)[cite: 3].

### Jsluice Integration ("Jsluice Analysis" Tab)
* Run `jsluice` commands directly against the text in the main input field[cite: 62, 205].
* Select `jsluice` modes (urls, secrets, etc.) from a dropdown menu[cite: 58, 207].
* Input custom command-line options for `jsluice`[cite: 60, 209].
* Toggle between formatted JSON output (attempted) and raw output using a checkbox[cite: 61, 214].
* Input text is saved to a persistent, timestamped temporary file (`jsluice_input_YYYYMMDD_HHMMSS.js`) in the system's temp directory [cite: Corrected `run_jsluice` function from previous interaction].
* The path to the created temporary file is displayed in the output, allowing reuse in the Shell Command tab [cite: Corrected `run_jsluice` function from previous interaction].
* Save Jsluice results to a file[cite: 68].
* Clear Jsluice results area[cite: 44].

### Shell Command Execution ("Shell Command" Tab)
* Execute arbitrary shell commands directly within the GUI[cite: 33, 234].
* Supports shell features like pipelines (`|`) and redirection (`<`, `>`)[cite: 236].
* Includes a configurable timeout to prevent the GUI from freezing on commands that hang or wait for input[cite: 235, 238].
* Useful for piping other commands to `jsluice` (e.g., `cat file.js | jsluice urls`) or using the persistent timestamped file (e.g., `jsluice secrets /tmp/jsluice_input_YYYYMMDD_HHMMSS.js`)[cite: 31].

### User Interface
* Interactive Text Input: Users can paste or input text for analysis[cite: 19].
* Tabbed Output: Organizes IOCs, VirusTotal results, Jsluice analysis, and Shell output into separate tabs[cite: 21, 276].
* IOC Review: Extracted IOCs from the main parsing function are displayed for review[cite: 22].
* Text Highlighting:
    * Highlights found search terms in the input area[cite: 13, 69].
    * Highlights parsed IOCs in the input area (orange background)[cite: 112, 115].
* Find & Replace: Includes find/replace functionality with regex support[cite: 16, 103].
* Placeholder Text: Input area shows placeholder text when empty[cite: 20, 101, 102].
* Clear Buttons: Dedicated buttons to clear each output area.

### IOC Interaction
* Defanging/Refanging: Converts standard IOCs into a 'defanged' format (and back) in the IOC Review tab[cite: 54, 55].
* Saving Functionality:
    * Save all parsed IOCs (from IOC Review tab) grouped by category to a single file[cite: 65].
    * Save parsed IOCs individually by category to separate files in a selected folder[cite: 66].
    * Save raw input text[cite: 17].
    * Save VirusTotal output[cite: 67].
    * Save Jsluice Analysis output[cite: 68].
* (Manual IOC modification is not a feature; users edit the input text directly).

### Integration with VirusTotal
* VirusTotal Analysis: Check selected IOCs (URLs, Hashes, IPs) from the 'IOC Review' or 'Jsluice Analysis' tabs against VirusTotal's database[cite: 46, 175].
* VirusTotal Submission: Submit selected URLs for scanning[cite: 47, 178].
* VirusTotal Hash Retrieval: Retrieves MD5, SHA1, and SHA256 hashes for selected file hashes[cite: 49, 188].
* MITRE ATT&CK Information: Retrieves MITRE ATT&CK techniques associated with selected file hashes[cite: 50, 199].
* API Key Handling: Prompts for API key when needed and stores it for the session[cite: 161].

### Example Usage
* Grabbed an article online with IOCs copy and pasted the entire thing and parsed. Ran URL's / Subdomains through Virus Total API and came up with malicious hits.
* Pasted JavaScript code into the input, ran `jsluice urls` via the "Jsluice Analysis" tab, then copied the resulting temp file path and used it in the "Shell Command" tab: `jsluice secrets <path_to_temp_file.js>`.
![image](https://github.com/AlbertL7/IOC-Extractor-GUI/assets/71300144/62ac9909-d9b9-4e77-9dda-a2c215867c73)

## Possible Future Updates
* Create an SQL backend to query past saved IOCs easily.
* Integrate more VirusTotal API features (grab sigma rules based on file behavior).
* Integrate Rate limiting for VirusTotal API.
* Option to clear persistent timestamped jsluice files.
* Make output text areas more interactive (e.g., clickable links).

## Warning
* There is no rate limiting for the VirusTotal API queries so if you are submitting a giant amount of hashes / URLs for analysis you may cause a DOS on VirusTotal and get your IP blocked.
* Timestamped `.js` files created by the "Run Jsluice" button are **not automatically deleted** and will accumulate in your system's temporary directory. Manual cleanup may be required periodically.

## Testing / Help
* I really want to make this a great and daily use application, so any help / ideas to make this application better is appreciated, feel free to fork or request commits!

## Problems
* The buttons might overlap or change position based on OS and screen resolution. Working to improve layout robustness.

Credits: Developed by AlbertL7 with help from ChatGPT4 and Google Gemini.
