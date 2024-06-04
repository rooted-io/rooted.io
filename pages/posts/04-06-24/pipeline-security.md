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

