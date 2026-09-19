# Windows Log Analysis 🔎

A hands-on cybersecurity investigation project focused on analyzing simulated Windows Security Events and identifying a potentially suspicious authentication pattern.

The logs used in this project are fictional and were created for educational purposes.

The goal was to investigate authentication activity from a security analyst perspective, identify suspicious patterns, analyze post-authentication activity, build an incident timeline, and document recommended investigation steps.

## 🔎 What Did I Investigate?

The investigation focused on:

* Windows Security Event IDs
* Failed and successful authentication attempts
* Logon Types
* Source IP addresses
* Remote authentication activity
* Process creation events
* Parent-child process relationships
* Post-authentication activity
* Incident timelines
* Evidence-based investigation

## 🚨 Investigation Findings

The investigation identified a potentially suspicious authentication pattern involving the `administrator` account.

Five consecutive failed authentication attempts were recorded from:

`192.168.1.45`

The attempts occurred within approximately 33 seconds and were followed by a successful authentication from the same source IP.

The successful authentication used:

`Logon Type 10 (RemoteInteractive)`

Logon Type 10 is commonly associated with Remote Desktop Protocol (RDP).

Shortly after the successful authentication, several process creation events were recorded:

```text
powershell.exe → cmd.exe → net.exe
```

The `net.exe` utility is a legitimate Windows command-line tool used for various network and administrative functions. Its presence alone does not indicate malicious activity.

However, the combination of repeated authentication failures, successful remote authentication, and subsequent process creation activity warranted further investigation.

## 🧩 Events Observed

| Event ID | Meaning                   |
| -------- | ------------------------- |
| 4625     | Failed authentication     |
| 4624     | Successful authentication |
| 4688     | New process created       |

### Logon Types Observed

| Logon Type | Meaning                                          |
| ---------- | ------------------------------------------------ |
| 2          | Interactive                                      |
| 3          | Network                                          |
| 10         | RemoteInteractive / commonly associated with RDP |

## 🕒 Incident Timeline

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

## 🛡️ Recommended Investigation Steps

If this activity occurred in a real organization, further investigation would include:

1. Identify the device associated with `192.168.1.45`.
2. Determine who was using the device at the time.
3. Verify whether the RDP connection was authorized.
4. Obtain the command-line arguments used with `net.exe`.
5. Review additional Windows Security and endpoint logs.
6. Check for account creation or privilege changes.
7. Investigate activity occurring after the successful authentication.
8. Correlate the events with network and authentication logs.

## 🧠 What I Learned

This project helped me practice:

* Windows log analysis
* Authentication investigation
* Event ID analysis
* RDP-related logon analysis
* Process creation analysis
* Source IP investigation
* Timeline construction
* Incident investigation
* Evidence-based reasoning

One of the main lessons from this investigation was that a suspicious-looking event should not immediately be considered malicious.

Additional context, such as the owner of the source IP, the legitimacy of the account, and the activity performed after authentication, is necessary to properly assess an incident.

## 📁 Project Structure

```text
windows-log-analysis/
│
├── security_events.txt
├── investigation.md
└── README.md
```

### `security_events.txt`

The simulated Windows Security Events used during the investigation.

### `investigation.md`

The detailed investigation report containing the observations, authentication analysis, post-authentication activity, timeline, assessment, and recommended next steps.

### `README.md`

Project documentation and a summary of the investigation.

## ⚠️ Disclaimer

This project uses simulated Windows Security Events created for educational purposes.

No real security incident or compromised system was investigated.

---

# 🇧🇪 Nederlandse versie

# Windows Log Analysis 🔎

Een praktisch cybersecurityonderzoek gericht op het analyseren van gesimuleerde Windows Security Events en het identificeren van een mogelijk verdacht authenticatiepatroon.

De logs in dit project zijn fictief en werden gemaakt voor educatieve doeleinden.

Het doel was om authenticatieactiviteiten vanuit het perspectief van een securityanalist te onderzoeken, verdachte patronen te identificeren, activiteiten na authenticatie te analyseren, een incidenttijdlijn op te stellen en aanbevolen vervolgstappen te documenteren.

## 🔎 Wat heb ik onderzocht?

Het onderzoek richtte zich op:

* Windows Security Event IDs
* Mislukte en succesvolle authenticatiepogingen
* Logon Types
* Source IP-adressen
* Remote authenticatie
* Process creation events
* Relaties tussen parent- en child-processen
* Activiteiten na authenticatie
* Incidenttijdlijnen
* Evidence-based onderzoek

## 🚨 Bevindingen

Tijdens het onderzoek werd een mogelijk verdacht authenticatiepatroon vastgesteld rond het `administrator`-account.

Er werden vijf opeenvolgende mislukte authenticatiepogingen geregistreerd vanaf:

`192.168.1.45`

De pogingen vonden plaats binnen ongeveer 33 seconden en werden gevolgd door een succesvolle authenticatie vanaf hetzelfde IP-adres.

De succesvolle authenticatie gebruikte:

`Logon Type 10 (RemoteInteractive)`

Logon Type 10 wordt vaak geassocieerd met Remote Desktop Protocol (RDP).

Kort na de succesvolle authenticatie werden verschillende process creation events geregistreerd:

```text
powershell.exe → cmd.exe → net.exe
```

De `net.exe`-tool is een legitiem Windows-commandlineprogramma dat wordt gebruikt voor verschillende netwerk- en beheertaken. De aanwezigheid ervan betekent op zichzelf niet dat er sprake is van kwaadaardige activiteit.

De combinatie van meerdere mislukte authenticatiepogingen, een succesvolle remote authenticatie en daaropvolgende process creation-activiteiten was echter voldoende reden voor verder onderzoek.

## 🧩 Geobserveerde Events

| Event ID | Betekenis                 |
| -------- | ------------------------- |
| 4625     | Mislukte authenticatie    |
| 4624     | Succesvolle authenticatie |
| 4688     | Nieuw proces aangemaakt   |

### Geobserveerde Logon Types

| Logon Type | Betekenis                                     |
| ---------- | --------------------------------------------- |
| 2          | Interactive                                   |
| 3          | Network                                       |
| 10         | RemoteInteractive / vaak geassocieerd met RDP |

## 🕒 Incidenttijdlijn

```text
08:41:12  Mislukte authenticatie — administrator
08:41:18  Mislukte authenticatie — administrator
08:41:24  Mislukte authenticatie — administrator
08:41:31  Mislukte authenticatie — administrator
08:41:38  Mislukte authenticatie — administrator
08:41:45  Succesvolle authenticatie — administrator / Logon Type 10

08:42:17  powershell.exe aangemaakt
08:42:31  cmd.exe aangemaakt door PowerShell
08:42:47  net.exe aangemaakt door CMD
```

## 🛡️ Aanbevolen vervolgstappen

Als deze activiteit in een echte organisatie zou plaatsvinden, zouden de volgende stappen verder onderzocht worden:

1. Identificeer het apparaat dat gekoppeld is aan `192.168.1.45`.
2. Bepaal wie het apparaat op dat moment gebruikte.
3. Controleer of de RDP-verbinding geautoriseerd was.
4. Verkrijg de command-line arguments die met `net.exe` werden gebruikt.
5. Analyseer aanvullende Windows Security- en endpointlogs.
6. Controleer op het aanmaken van accounts of wijzigingen in privileges.
7. Onderzoek welke activiteiten plaatsvonden na de succesvolle authenticatie.
8. Correlleer de events met netwerk- en authenticatielogs.

## 🧠 Wat heb ik geleerd?

Met dit project heb ik geoefend met:

* Windows-loganalyse
* Onderzoek van authenticatie
* Analyse van Event IDs
* Analyse van RDP-gerelateerde logons
* Analyse van process creation
* Onderzoek van Source IP-adressen
* Het opstellen van incidenttijdlijnen
* Incidentonderzoek
* Evidence-based reasoning

Een van de belangrijkste lessen uit dit onderzoek was dat een verdacht uitziend event niet automatisch als kwaadaardig moet worden beschouwd.

Aanvullende context, zoals de eigenaar van het source IP-adres, de legitimiteit van het account en de activiteiten na authenticatie, is nodig om een incident goed te kunnen beoordelen.

## 📁 Projectstructuur

```text
windows-log-analysis/
│
├── security_events.txt
├── investigation.md
└── README.md
```

### `security_events.txt`

De gesimuleerde Windows Security Events die tijdens het onderzoek werden gebruikt.

### `investigation.md`

Het gedetailleerde onderzoeksrapport met de observaties, authenticatieanalyse, activiteiten na authenticatie, tijdlijn, beoordeling en aanbevolen vervolgstappen.

### `README.md`

De projectdocumentatie en een samenvatting van het onderzoek.

## ⚠️ Disclaimer

Dit project gebruikt gesimuleerde Windows Security Events die voor educatieve doeleinden zijn gemaakt.

Er werd geen echt securityincident of gecompromitteerd systeem onderzocht.


