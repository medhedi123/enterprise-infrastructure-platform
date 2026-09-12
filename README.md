\# Enterprise Infrastructure Platform



A production-inspired enterprise infrastructure environment combining secure remote access, centralized storage, file sharing, access control, monitoring, print services, and a custom management platform.



The project is being built from the infrastructure layer upward, with real Linux services managed and observed through a future Spring Boot + React control plane.



\## Current Architecture



Windows Host

&#x20;   |

&#x20;   | VirtualBox

&#x20;   |

&#x20;   +-- infra-gateway

&#x20;   |     NAT:      10.0.2.15

&#x20;   |     corp-net: 10.10.10.10

&#x20;   |

&#x20;   +-- storage-01

&#x20;         NAT:      10.0.2.15

&#x20;         corp-net: 10.10.10.20



Private network:



10.10.10.0/24



\## Current Components



\### infra-gateway



Ubuntu Server 26.04.1 LTS



Responsibilities:



\- Corporate network gateway

\- SSH administration

\- Future WireGuard VPN gateway

\- Future firewall and routing

\- Future secure remote access



Internal address:



10.10.10.10



\### storage-01



Ubuntu Server 26.04.1 LTS



Responsibilities:



\- Centralized company file storage

\- Samba SMB file server

\- Department-based access control

\- Future storage quotas

\- Future backup and recovery

\- Future object storage



Internal address:



10.10.10.20



\## Department Storage



/srv/company/



\- finance

\- hr

\- engineering

\- management

\- shared



Linux groups:



\- finance

\- hr

\- engineering

\- management

\- company-shared



\## Test Users



Sarah

\- Finance

\- Shared



Adam

\- HR

\- Shared



Youssef

\- Engineering

\- Shared



\## Security Model



Department folders use Linux group ownership and restricted permissions.



Example:



Finance:

root:finance

2770



This allows Finance members to read/write while blocking users outside the Finance group.



Samba applies an additional authentication and authorization layer.



Example:



Sarah -> Finance: ALLOWED

Sarah -> Shared: ALLOWED

Sarah -> HR: DENIED



\## Completed Milestones



\- Ubuntu Server lab created

\- Private corporate network created

\- Static internal addressing configured

\- SSH remote administration configured

\- Server-to-server communication validated

\- Samba installed

\- Department folder structure created

\- Linux groups created

\- Department permissions configured

\- Samba users configured

\- Samba shares configured

\- SMB authentication validated

\- Unauthorized department access rejected

\- SMB file upload successfully tested



\## Planned Architecture



Internet

&#x20;  |

Firewall / VPN

&#x20;  |

infra-gateway

&#x20;  |

corp-net

&#x20;  |

&#x20;  +-- storage-01

&#x20;  +-- print-01

&#x20;  +-- application services

&#x20;  +-- monitoring



Management Platform:



React + TypeScript

&#x20;       |

Spring Boot REST API

&#x20;       |

PostgreSQL

&#x20;       |

Infrastructure services



\## Planned Technologies



Infrastructure:

\- Linux

\- WireGuard

\- Samba

\- MinIO

\- CUPS



Backend:

\- Java

\- Spring Boot

\- PostgreSQL



Frontend:

\- React

\- TypeScript



DevOps:

\- Docker

\- GitHub Actions

\- Prometheus

\- Grafana

\- Loki



Later:

\- Kubernetes

\- AWS

\- Terraform



\## Project Goal



Build a realistic enterprise infrastructure platform demonstrating:



\- Linux administration

\- Networking

\- Security

\- Storage engineering

\- Identity and access control

\- Backend engineering

\- REST APIs

\- Infrastructure automation

\- Observability

\- DevOps

\- Cloud-native architecture

