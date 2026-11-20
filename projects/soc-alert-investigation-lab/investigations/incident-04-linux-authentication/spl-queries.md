

\# Incident 04 — Linux Authentication SPL Queries



\## 1. Search Linux Authentication Logs



Search for common Linux authentication messages.



```spl

index=\* ("Failed password" OR "authentication failure" OR "Invalid user" OR "Accepted password" OR "Accepted publickey")

```



\## 2. Review Authentication Event Details



Review timestamps, hosts, and authentication messages.



```spl

index=\* ("Failed password" OR "authentication failure" OR "Invalid user" OR "Accepted password" OR "Accepted publickey")

| table \_time host source sourcetype \_raw

| sort - \_time

```



\## 3. Search Failed SSH Logins



Identify failed SSH authentication attempts.



```spl

index=\* ("Failed password" OR "authentication failure" OR "Invalid user")

| table \_time host source sourcetype \_raw

| sort - \_time

```



\## 4. Search Successful SSH Logins



Identify successful SSH authentication events.



```spl

index=\* ("Accepted password" OR "Accepted publickey")

| table \_time host source sourcetype \_raw

| sort - \_time

```



\## 5. Search Invalid User Attempts



Identify authentication attempts involving invalid usernames.



```spl

index=\* "Invalid user"

| table \_time host source sourcetype \_raw

| sort - \_time

```



\## 6. Identify Repeated Authentication Failures



Review repeated failed authentication messages.



```spl

index=\* ("Failed password" OR "authentication failure" OR "Invalid user")

| stats count by host source sourcetype

| sort - count

```



\## 7. Review Authentication Activity by Host



Identify Linux hosts generating authentication events.



```spl

index=\* ("Failed password" OR "authentication failure" OR "Accepted password" OR "Accepted publickey")

| stats count by host

| sort - count

```



\## 8. Review Authentication Activity Timeline



Create a timeline of Linux authentication events.



```spl

index=\* ("Failed password" OR "authentication failure" OR "Accepted password" OR "Accepted publickey" OR "Invalid user")

| sort \_time

| table \_time host source sourcetype \_raw

```



\## 9. Investigation Workflow



1\. Identify Linux authentication events.

2\. Review timestamps.

3\. Identify usernames.

4\. Identify source addresses.

5\. Review authentication outcomes.

6\. Identify repeated failures.

7\. Check for successful logins following failures.

8\. Correlate related events.

9\. Determine the investigation verdict.



\## 10. Investigation Considerations



Repeated authentication failures may indicate password guessing or brute-force activity.



However, legitimate users may also generate failed logins due to incorrect credentials.



Successful authentication following repeated failures should be reviewed carefully.



The analyst should consider the source address, username, frequency, timestamps, and related activity before reaching a verdict.



\## 11. Limitations



Linux log formats vary depending on the operating system and authentication service.



The index, sourcetype, and extracted fields may differ depending on the Splunk configuration.



The searches in this document are generic searches and should be adjusted based on the actual Linux log data collected in the lab.



