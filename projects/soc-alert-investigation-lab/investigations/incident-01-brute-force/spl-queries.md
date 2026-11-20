\# Incident 01 — Windows Failed Logon SPL Queries



\## 1. Search Failed Authentication Events



Search for Windows Security Event ID 4625.



```spl

index=wineventlog sourcetype="WinEventLog:Security" EventCode=4625

