\# Windows Log Analysis 🔎



A small cybersecurity investigation project focused on analyzing simulated Windows Security Events and identifying a potentially suspicious authentication pattern.



The logs used in this project are fictional and were created for educational purposes.



The goal was to investigate authentication activity from a security analyst perspective, identify suspicious patterns, analyze post-authentication activity, build an incident timeline, and document recommended investigation steps.



\## 🔎 What did I investigate?



The investigation focused on:



\* Windows Security Event IDs

\* Failed and successful authentication attempts

\* Logon Types

\* Source IP addresses

\* Remote authentication activity

\* Process creation events

\* Parent-child process relationships

\* Post-authentication activity

\* Incident timelines

\* Evidence-based investigation



\## 🚨 Investigation Findings



The investigation identified a potentially suspicious authentication pattern involving the `administrator` account.



Five consecutive failed authentication attempts were recorded from:



`192.168.1.45`



These attempts occurred within approximately 33 seconds and were followed by a successful authentication from the same source IP.



The successful authentication used:



`Logon Type 10 (RemoteInteractive)`



This is commonly associated with Remote Desktop Protocol (RDP).



Shortly after the successful authentication, several process creation events were recorded:



```text

powershell.exe → cmd.exe → net.exe

```



The `net.exe` utility is a legitimate Windows command-line tool used for various network and administrative functions. Its presence alone does not indicate malicious activity.



However, the combination of repeated authentication failures, successful remote authentication, and subsequent process creation activity warranted further investigation.



\## 🧩 Events Observed



| Event ID | Meaning                   |

| -------- | ------------------------- |

| 4625     | Failed authentication     |

| 4624     | Successful authentication |

| 4688     | New process created       |



\### Logon Types Observed



| Logon Type | Meaning                                          |

| ---------- | ------------------------------------------------ |

| 2          | Interactive                                      |

| 3          | Network                                          |

| 10         | RemoteInteractive / commonly associated with RDP |



\## 🕒 Incident Timeline



```text

08:41:12  Failed authentication — administrator

08:41:18  Failed authentication — administrator

08:41:24  Failed authentication — administrator

08:41:31  Failed authentication — administrator

08:41:38  Failed authentication — administrator

08:41:45  Successful authentication — administrator / Logon Type 10



08:42:17  powershell.exe created

08:42:31  cmd.exe created by PowerShell

08:42:47  net.exe created by CMD

```



\## 🛡️ Recommended Investigation Steps



If this activity occurred in a real organization, further investigation would include:



1\. Identify the device associated with `192.168.1.45`.

2\. Determine who was using the device at the time.

3\. Verify whether the RDP connection was authorized.

4\. Obtain the command-line arguments used with `net.exe`.

5\. Review additional Windows security and endpoint logs.

6\. Check for account creation or privilege changes.

7\. Investigate activity occurring after the successful authentication.

8\. Correlate the events with network and authentication logs.



\## 🧠 What I Learned



This project helped me practice:



\* Windows log analysis

\* Authentication investigation

\* Event ID analysis

\* RDP-related logon analysis

\* Process creation analysis

\* Source IP investigation

\* Timeline construction

\* Incident investigation

\* Evidence-based reasoning



One of the main lessons from this investigation was that a suspicious-looking event should not immediately be considered malicious.



Additional context, such as the owner of the source IP, the legitimacy of the account, and the activity performed after authentication, is necessary to properly assess an incident.



\## 📁 Project Structure



```text

windows-log-analysis/

│

├── security\_events.txt

├── investigation.md

└── README.md

```



\### `security\_events.txt`



The simulated Windows Security Events used during the investigation.



\### `investigation.md`



The detailed investigation report containing the observations, authentication analysis, post-authentication activity, timeline, assessment, and recommended next steps.



\### `README.md`



Project documentation and a summary of the investigation.



\## ⚠️ Disclaimer



This project uses simulated Windows Security Events created for educational purposes.



No real security incident or compromised system was investigated.



