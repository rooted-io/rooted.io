# CI/CD Security: PPE

CI/CD environments are arguably among the most critical systems from a security perspective, as they run software builds and also contain tons of secrets, passwords, and tokens.  
Nevertheless, the culture of hardening these environments is still dangerously inadequate.  

*Pipeline Poisoned Execution (PPE)* is a security vulnerability in Continuous Integration/Continuous Deployment pipelines.  
It occurs when an attacker injects malicious code or configurations into the pipeline, leading to the execution of unintended or harmful actions during the build, test, or deployment stages.  
This can compromise the integrity and security of the software being developed and deployed. PPE exploits can lead to unauthorized access, data leaks, and manipulation of the software supply chain.  
<br/>
In the video below we demonstrate a live exfiltration of secrets, via remote code execution, from a GitHub Action vulnerable to PPE:  

<video width="850" controls>
  <source src="media/ppe.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>  

<br/>

As a bonus point here is one of many examples of a query that we can input directly into *GitHub Search* to find potential sensitive information related to AWS accounts by inspecting the action's logs:  

```console
"𝐚𝐰𝐬 𝐥𝐚𝐦𝐛𝐝𝐚" 𝐀𝐍𝐃 (𝐩𝐚𝐭𝐡:.𝐠𝐢𝐭𝐡𝐮𝐛/𝐰𝐨𝐫𝐤𝐟𝐥𝐨𝐰𝐬) 𝐀𝐍𝐃 ("𝐩𝐮𝐛𝐥𝐢𝐬𝐡-𝐯𝐞𝐫𝐬𝐢𝐨𝐧" 𝐎𝐑 "𝐮𝐩𝐝𝐚𝐭𝐞-𝐟𝐮𝐧𝐜𝐭𝐢𝐨𝐧-𝐜𝐨𝐧𝐟𝐢𝐠𝐮𝐫𝐚𝐭𝐢𝐨𝐧" 𝐎𝐑 "𝐮𝐩𝐝𝐚𝐭𝐞-𝐟𝐮𝐧𝐜𝐭𝐢𝐨𝐧-𝐜𝐨𝐝𝐞")
```  
