\# Enterprise File Server



Server:



storage-01



Internal IP:



10.10.10.20



\## Technology



Samba / SMB



\## Storage Structure



/srv/company/



finance

hr

engineering

management

shared



\## Linux Groups



finance

hr

engineering

management

company-shared



\## Permissions



Department directories use:



2770



This provides:



Owner: full access

Department group: full access

Others: no access



The setgid bit ensures new files inherit the department group.



\## Samba Shares



finance

hr

engineering

management

shared



\## Test Users



Sarah:

finance

company-shared



Adam:

hr

company-shared



Youssef:

engineering

company-shared



\## Security Tests



Sarah -> Finance:

PASS



Sarah -> Shared:

PASS



Sarah -> HR:

ACCESS DENIED



\## File Transfer Test



finance-report.txt was uploaded using SMB from infra-gateway to storage-01 while authenticated as Sarah.



The test proved:



\- Network connectivity

\- Samba authentication

\- Group authorization

\- File write access

\- Department isolation

