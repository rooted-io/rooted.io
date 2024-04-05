# Offensive Security Privacy

When conducting offensive security activities, it is often beneficial to employ stealth techniques to conceal our identity behind a veil of anonimity.  
One such method is leveraging the [*Tor network*](https://en.wikipedia.org/wiki/Tor_(network)) to mask the IP address from which we are initiating our actions.  

One can, for example, run a container that executes the Tor service and then launching enumeration and discovery tools using that container as a proxy (or running the tools directly from within the container):  
```yaml
FROM alpine:latest

RUN apk update && apk --no-cache add tor curl wget nmap jq # add other tools here

CDM tor
```  

<br>  

- [Back to main page](../../../index.md)  