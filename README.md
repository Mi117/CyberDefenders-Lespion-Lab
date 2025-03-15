# CyberDefenders.org - Lespion Lab Walkthrough

INTRO:

L'Espion, a challenge hosted on CyberDefenders.org, presents investigators with a scenario involving potential corporate espionage. The challenge tasks participants with analyzing digital evidence from a suspect's device and using OSINT techniques to uncover connections, activities, and potential data exfiltration.

TOOLS USED:

- SHERLOCK (https://github.com/sherlock-project/sherlock): powerful OSINT software that gathers usernames from all the popular social media platforms, forums, etc.
- CYBERCHEF (https://gchq.github.io/CyberChef/): open source and freeware HEX editor.
- GOOGLE MAPS
- GOOGLE IMAGE SEARCH 

SCENARIO:

You have been tasked by a client whose network was compromised and brought offline to investigate the incident and determine the attacker's identity.

Incident responders and digital forensic investigators are currently on the scene and have conducted a preliminary investigation. Their findings show that the attack originated from a single user account, probably, an insider. Investigate the incident, find the insider, and uncover the attack actions.


Link to the challenge: https://cyberdefenders.org/blueteam-ctf-challenges/lespion/

WALKTHROUGH:

Q1) File -> Github.txt: What API key did the insider add to his GitHub repositories?

To investigate the insider activity, we begin by analyzing the user's GitHub repository. The GitHub profile in question belongs to the user EMarseille99, who is described as a backend programmer for a software consulting company. Among the repositories there is one which is particularly striking as is project written in Javascript and publicly accessible which raises concerns about its contents.

![q1](https://github.com/user-attachments/assets/570fccee-dfe2-4d73-b723-944d46b3deee)

Analysing the repo we can see the file "Login Page.js" and upon opening it we can find all the details for the API key.

![q1-1](https://github.com/user-attachments/assets/0f66cbab-cde0-412e-ac12-3cdc36ec55a6)

That's a case of HARDCODED API KEYS, which refer to sensitive authentication credentials that are directly embedded within the source code of an application, making them easily accessible to anyone who gains access to the source code.


Q2) File -> Github.txt: What is the plaintext password the insider added to his GitHub repositories?

This file seems to be responsible for handling the user login functionality, with the handling of the passwords.
Further examination of the file in the target repo showcase the username and password [UGljYXNzb0JhZ3VldHRlOTk] which is encoded with Base64 encoding, a method of encoding binary data as text.

![q2](https://github.com/user-attachments/assets/4d2ce793-3c4f-48a2-89f4-5ad59f6d0830)

We can use tools like CyberChef to decode the text into plain readable text (see below):

![q2-2](https://github.com/user-attachments/assets/f5afba27-d560-4d58-a83c-9615d389c737)

Q3) File -> Github.txt: What cryptocurrency mining tool did the insider use?

Cryptocurrency mining is the process of validating and adding transactions to a blockchain network through complex computational algorithms. Mining often requires significant computational resources, and attackers sometimes exploit compromised systems to deploy mining software, effectively hijacking resources without authorization. This malicious practice is referred to as cryptojacking and can lead to performance degradation, increased power consumption, and financial losses for the victim.
Starting to analysing the repositories, we come across "xmrig" repository, which is a powerful cyptocurrency miner, and its presence in the attacker repositories solidifies the theory that he/she leveraged the compromized network to perpetrate malicious activities (such as cryptomining).

![q3](https://github.com/user-attachments/assets/d47312c1-72dd-434e-b12d-a5a98f65b31c)

Q4) On which gaming website did the insider have an account?

Here's where comes the fun. We leverage Open Source software, part of the Open Source Intelligence (OSINT) techniques. The software used is SHERLOCK, a powerful tool that allows us to search for usernames across a variety of platforms.
Jumping on our machine termina, we start the search by simply calling the software and input the username (in our case: sherlock EMarseille99) to eventually find the that the attacker has several profiles with multiple platforms (photo below).

![q4](https://github.com/user-attachments/assets/15b69279-6da3-4a7f-aa3d-bc556885c380)

Q5) What is the link to the insider Instagram profile?

This information can also be found in Sherlock, https://www.instagram.com/EMarseille99/.

![2025-03-15 12_58_14-kali-linux-2024 4-vmware-amd64 - VMware Workstation pngq5](https://github.com/user-attachments/assets/bbe55c64-e00a-4622-bffe-74817a727b73)

Q6) Where did the insider go on the holiday? (Country only)

We can see that on the target Instagram page, the asnwer is Singapore.

![q6-1](https://github.com/user-attachments/assets/024ac559-92db-41ce-960b-8724b66d7bec)
![q6-2](https://github.com/user-attachments/assets/fcc55309-9902-48a1-a7ed-8e3b71ab5138)

Q7) Where is the insider family live? (City only)

Also this information is contained within the target Instagram profile as shown below.

![q7](https://github.com/user-attachments/assets/a20dd62a-bea0-44fc-8361-4ede34745f5d)
![q7-2](https://github.com/user-attachments/assets/03c2ec1a-0c15-41aa-aef3-0e88f51e3439)

The answer is Dubai.

Q8) File -> office.jpg: You have been provided with a picture of the building in which the company has an office. Which city is the company located in?

Now we have to investigate the picture in the downloaded forder, and starting to analise the details and information contained. 

![office](https://github.com/user-attachments/assets/fc3012ad-595a-445a-ab5b-e1a60384adb4)

We can either use a Google Search (or your preferred browser) or utilize the convenient tool provided by Google to search photos online.

![q6](https://github.com/user-attachments/assets/4be95b68-afe8-44b9-b57c-4a0c56e31cda)

The answer is Birmingham.

Q9) File -> Webcam.png: With the intel, you have provided, our ground surveillance unit is now overlooking the person of interest suspected address. They saw them leaving their apartment and followed them to the airport. Their plane took off and has landed in another country. Our intelligence team spotted the target with this IP camera. Which state is this camera in?

We use the same method in question 8, to find out that the IP camera il located at Notre Dame University, in the state of Indiana.

![q9](https://github.com/user-attachments/assets/62ab26ff-ccdd-4c86-8607-e91e55146a0f)


CONCLUSIONS

In conclusion, the Lespion challenge effectively demonstrates the critical role of Open Source Intelligence (OSINT) in modern cybersecurity investigations. By leveraging tools like Sherlock and Reverse Image Search, we were able to uncover valuabel information about the target that greatly aided our investigation.
This exercise highlights the importance of mastering OSINT techniques for blue teams, as the ability to gather and analyze publicly available information can significantly enhance incident response, threat hunting, and overall security posture. Furthermore, the challenge underscores the necessity of organizations to be aware of their digital footprint and implement robust security measures to minimize their exposure to potential OSINT-driven attacks. Ultimately, Lespion reinforces the idea that in today's interconnected world, effective cybersecurity relies not only on technical defenses but also on a deep understanding of the information landscape.

I want to thank the team of CyberDefenders.org and the challenge creators for a concise, yet insightful Lab as the practical application of concepts made this far more valuable than theoretical learning alone. I appreciate the time and effort put into creating such a valuable resource for the cybersecurity community. Thank you for contributing to my growth as a blue team analyst!

I hope you found this walkthrough insightful as well! If you found this content helpful, please consider giving it a clap! Your feedback is invaluable and motivates me to continue supporting your journey in the cybersecurity community. Remember, LET'S ALL BE MORE SECURE TOGETHER! For more insights and updates on cybersecurity analysis, follow me on Substack! [https://substack.com/@atlasprotect?r=1f5xo4&utm_campaign=profile&utm_medium=profile-page]
