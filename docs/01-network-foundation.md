\# Network Foundation



\## Private Corporate Network



Network:



10.10.10.0/24



Subnet mask:



255.255.255.0



\## Servers



| Host | Role | Internal IP |

|---|---|---|

| infra-gateway | Gateway / future VPN | 10.10.10.10 |

| storage-01 | File server | 10.10.10.20 |



\## VirtualBox Networking



Each VM currently has two interfaces.



\### Adapter 1



NAT



Used for:



\- Ubuntu updates

\- package installation

\- external Internet access



\### Adapter 2



Internal Network



Name:



corp-net



Used for communication between internal company servers.



\## Validation



storage-01 -> infra-gateway:



ping 10.10.10.10



Result:



4 packets transmitted

4 received

0% packet loss



infra-gateway -> storage-01:



ping 10.10.10.20



Result:



4 packets transmitted

4 received

0% packet loss



\## SSH



SSH is enabled on both servers.



Windows host access:



infra-gateway:



localhost:2222 -> VM port 22



storage-01:



localhost:2223 -> VM port 22



Private server-to-server SSH also works across corp-net.

