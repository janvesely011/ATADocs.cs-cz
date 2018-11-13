---
title: Referenční informace k protokolům Azure ATP SIEM | Dokumentace Microsoftu
description: Obsahuje ukázky protokolů podezřelých aktivit odeslaných ze služby Azure ATP do vašeho systému SIEM.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: fcbeb18c3841799aad068c8eedd45af71660925e
ms.sourcegitcommit: 2afc1486b40431f442d51a53df06e289796de87e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/12/2018
ms.locfileid: "51560758"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="azure-atp-siem-log-reference"></a>Referenční informace k protokolům Azure ATP SIEM

Ochrana ATP v programu Azure můžete dál zabezpečení výstrahy a monitorování výstrahy události do vašeho systému SIEM. Výstrahy a události jsou ve formátu CEF. Tento referenční článek obsahuje ukázky protokolů odeslané do vašeho systému SIEM.

## <a name="sample-azure-atp-security-alerts-in-cef-format"></a>Ukázka služby Azure ATP výstrah zabezpečení ve formátu CEF
Do systému SIEM se předávají následující pole a jejich hodnoty:

|Podrobnosti|Vysvětlení|
|---------|---------------|
|Spuštění|Počáteční čas výstrahy|
|suser|účet (obvykle uživatelský účet) účastnící se upozornění|
|shost|účet (obvykle uživatelský účet) účastnící se upozornění|
|Výsledek|Pokud je to relevantní, úspěch nebo neúspěch podezřelých aktivit ve výstraze|
|msg|popis výstrahy|
|CNT|pro výstrahy, které mají počet, kolikrát, aktivity, ke kterým došlo (například útok hrubou silou má určité množství uhodnutí hesel)|
|Aplikace |protokol použitý ve výstraze|
|externalId|Typ události ID Azure ATP zapíše do protokolu událostí, která odpovídá pro každý typ výstrahy|
|cs #label|řetězce zákazníků, které jsou povoleny ve formátu CEF, kde cs #label je název nového pole |
|cs #|povolené ve formátu CEF, kde cs # je hodnota řetězce zákazníků.|
|
- Například: cs1Label = url cs1 =https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
<br> Cs1 pole je adresa URL výstrahy. 

- Příklad: cs2Label = aktivační událost cs2 = nový
<br> Pole cs2 identifikuje, pokud je výstraha nové nebo aktualizované.


> [!NOTE]
> Pokud budete chtít vytvořit automatizace nebo skriptů pro protokolů SIEM ochrany ATP v programu Azure, doporučujeme použít **externalId** pole k identifikaci typu výstrahy místo názvu upozornění pro tento účel. Upozornění názvy mohou být občas upravit, zatímco **externalId** jednotlivých výstrah je trvalá.  

|Upozornění Azure ATP|ExternalId jedinečný|
|---------|---------|
|Útok hrubou silou pomocí jednoduché vazby LDAP.|2004|
|Šifrování downgrade aktivity Skeleton key|2011|
|Aktivita snížení úrovně šifrování (možný útok overpass-the-hash)|2008|
|Aktivita snížení úrovně šifrování (potenciální útok metodou golden ticket)|2009|
|Aktivita snížení úrovně šifrování (potenciální útoku typu skeleton key)|2010|
|Aktivita Honeytokenu|2014|
|Krádež identity pomocí útoku Pass-the-Hash|2017|
|Krádež identity pomocí útoku Pass-the-Ticket|2018|
|Lístek protokolu Kerberos golden – čas anomálií|2022|
|Protokol Kerberos Golden Ticket - neexistující účet|2027|
|Škodlivá žádost o soukromé informace přes Data Protection|2020|
|Škodlivá replikace adresářových služeb|2006|
|Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace|2013|
|Rekognoskace pomocí výčtu účtů|2003|
|Rekognoskace pomocí DNS|2007|
|Rekognoskace pomocí výčtu relací SMB|2012|
|Rekognoskace pomocí dotazů na adresářové služby|2021|
|Pokus o spuštění vzdáleného kódu|2019|
|Podezřelé chyby ověřování|2023|
|Žádost o replikaci řadiče domény podezřelé (možný útok DCShadow)|2029|
|Povýšení řadiče domény podezřelé (možný útok DCShadow)|2028|
|Podezřelá komunikace prostřednictvím DNS|2031|
|Podezřelé úprava citlivých skupin|2024|
|Podezřelé vytvoření služby|2026|
|Podezřelé připojení k síti VPN|2025|
|Neobvyklá implementace protokolu (možný útok ransomwarem WannaCry) *|2002|
|Neobvyklá implementace protokolu (potenciální použití škodlivých nástrojů, jako je Hydra) *|2002|
|Neobvyklá implementace protokolu (potenciální použijte Metasploit hacking nástroje) *|2002|
|Neobvyklý protokol Kerberos protokol implementace (možný útok overpass-the-hash) *|2002|
|*Neobvyklá implementace protokolu* výstrahy aktuálně sdílet externalId. ExternalId pro každý typ tyto výstrahy se změní v budoucích vydáních na jedinečné externalId|****|

## <a name="sample-logs"></a>Ukázky protokolů

Příklady protokolu v souladu s RFC 5242 ale ochrany ATP v programu Azure podporuje také RFC 3164.

Priority:

- 3 = nízká
- 5 = střední
- 10 = vysoká

### <a name="brute-force-attack-using-ldap-simple-bind"></a>Útok hrubou silou pomocí jednoduché vazby LDAP.
02 – 21 – 2018 16:20:21 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:06.156238 + 00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | LdapBruteForceSecurityAlert | Útok hrubou silou pomocí jednoduché vazby LDAP | 5 | start = 2018-02-21T14:19:41.7422810Z app = Ldap suser Wofford Thurston shost = = CLIENT1 msg = na Wofford Thurston (softwarový inženýr) pomocí protokolu Ldap protokolu došlo k pokusu o útok hrubou silou z počítače CLIENT1 (100 odhad pokusy o). CNT = 100 externalId = 2004 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a cs2Label = aktivační událost cs2 = aktualizace

### <a name="encryption-downgrade-activity---golden-ticket"></a>Aktivita související s oslabením šifrování - zlatý lístek
10 – 29 – 2018 11:25:07 Auth.Warning 192.168.0.202 1 2018-10-29T09:25:01.007701 + 00:00 DC3 CEF 3908 GoldenTicketEncryptionDowngradeS ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | GoldenTicketEncryptionDowngradeSecurityAlert | Aktivita snížení úrovně šifrování (potenciální útok metodou golden ticket) | 5 | start = 2018-10-29T09:37:49.0849130Z aplikace = Kerberos msg = W10. 000007 okruh používá slabší metodu šifrování (RC4), v žádosti o službu pomocí protokolu Kerberos (TGS_REQ), z W10-000007 – nástroje pro přístup k Host/domain1.test.Local. externalId = 2009 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f01f8403-88b2-437e-b4ad-d72485fe05ac cs2Label = aktivační událost cs2 = nový

### <a name="encryption-downgrade-activity----skeleton-key"></a>Aktivita související s oslabením šifrování - Skeleton Key
02 – 21 – 2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Aktivita související s oslabením šifrování | 5 | start = 2018-02-21T14:19:41.8737870Z aplikace = Kerberos msg = metodu šifrování pole ETYPE_INFO2 KRB_ERR byl downgradovat zpráv z počítače CLIENT1, na základě dřív zjištěné chování. To může být důsledek Skeleton Key na řadič domény DC1. externalId = 2011 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label = aktivační událost cs2 = nový

### <a name="encryption-downgrade-activity---overpass-the-hash"></a>Aktivita související s oslabením šifrování - Overpass-the-Hash
02 – 21 – 2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Aktivita související s oslabením šifrování | 5 | start = 2018-02-21T14:19:41.8737870Z aplikace = Kerberos msg = metodu šifrování pole Encrypted_Timestamp v AS_REQ byla snížena zpráv z počítače CLIENT1, na základě dřív zjištěné chování. Může to být důsledek krádeže přihlašovacích údajů s pomocí Overpass-the-Hash z počítače CLIENT1. externalId = 2011 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label = aktivační událost cs2 = aktualizace

### <a name="honeytoken-activity"></a>Aktivita Honeytokenu
02 – 21 – 2018 16:20:36 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:34.106162 + 00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | HoneytokenActivitySecurityAlert | Aktivita Honeytokenu | 5 | start = 2018-02-21T14:20:26.6705617Z aplikace Kerberos suser = honey msg = = následující aktivity provedl honey: \r\nLogged v na počítači KLIENT2 přes řadič domény DC1. externalId = 2014 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c cs2Label = aktivační událost cs2 = nový

### <a name="identity-theft-using-pass-the-hash"></a>Krádež identity pomocí typu Pass-the-Hash
02 – 21 – 2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | PassTheHashSecurityAlert | Krádež identity pomocí útoku Pass-the-Hash | 10 | start = 2018-02-21T15:02:22.2577465Z aplikace Kerberos suser = = msg Eugene Jenkins = Eugene Jenkins (softwarový inženýr). hodnota hash byla ukradena z jednoho počítače dříve přihlašující Eugene Jenkins (Software Inženýr) a použít z počítače CLIENT1. externalId = 2017 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label = aktivační událost cs2 = aktualizace

### <a name="identity-theft-using-pass-the-ticket-attack"></a>Krádež identity pomocí útoku Pass-the-Ticket
02 – 21 – 2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | PassTheTicketSecurityAlert | Krádež identity pomocí útoku Pass-the-Ticket | 10 | start = 2018-02-21T15:02:22.2577465Z aplikace = Kerberos suser = msg Eugene Jenkins = Kerberos Eugene Jenkins (softwarový inženýr) pro lístky byly odcizeny z Admin-PC do Victim-PC a používá pro přístup k účtu krbtgt/Doména1. TEST. MÍSTNÍ. externalId = 2018 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label = aktivační událost cs2 = nový

### <a name="kerberos-golden-ticket"></a>Protokol Kerberos Golden Ticket 
02 – 21 – 2018 16:22:39 Auth.Error 192.168.0.220 1 2018-02-21T14:22:34.274054 + 00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | GoldenTicketSecurityAlert | Aktivita zlatého lístku Kerberos | 10 | start = 2018-02-21T14:19:03.2416152Z aplikace Kerberos suser = Lanell Campos msg = = podezřelé využití lístku Kerberos Lanell Campos (softwarový inženýr) společnosti, která potenciální útok metodou Golden Ticket, byla zjištěna. externalId = 2022 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0 cs2Label = aktivační událost cs2 = aktualizace

### <a name="kerberos-golden-ticket-non-existent-account"></a>Neexistující účet zlatý lístek protokolu Kerberos
07-01-2018 14:28:49 Auth.Error 192.168.0.100 1 2018-07-01T11:28:35.546638 + 00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.39.0.0 | ForgedPrincipalSecurityAlert | Kerberos Golden Ticket - neexistujících účtů | 10 | start = 2018-07-01T09:48:31.2567987Z app = Kerberos suser=domain1.test.local\fake msg=domain1.test.local\fake, který neexistuje v Active Directory, používá lístek protokolu Kerberos. -The-ticket byla zjištěna z 2 počítače přístup k prostředkům 3. To může znamenat potenciální útok metodou Golden Ticket. externalId = 2027 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4 cs2Label = aktivační událost cs2 = aktualizace

### <a name="malicious-data-protection-private-information-request"></a>Škodlivá žádost o soukromé informace přes Data Protection
10 – 29 – 2018 11:22:04 Auth.Error 192.168.0.202 1 2018-10-29T09:22:00.350864 + 00:00 DC3 CEF 3908 RetrieveDataProtectionBackupKeyS ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | RetrieveDataProtectionBackupKeySecurityAlert | Škodlivá žádost o informace soukromé ochrany dat | 10 | start = 2018-10-29T09:19:45.6307993Z app = LsaRpc shost = CLIENT1 msg = uzivatel1 provést 1 úspěšné pokusy o z počítače CLIENT1 načíst záložní klíč domény DPAPI z DC1. externalId = 2020 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/2f5717cb-2434-4d54-8af4-b2c6d14bc15c cs2Label = aktivační událost cs2 = nový

### <a name="malicious-replication-of-directory-services"></a>Škodlivá replikace adresářových služeb 
02 – 21 – 2018 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.254930 + 00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | MaliciousServiceCreationSecurityAlert | Podezřelé vytvoření služby | 5 | start = 2018-02-21T14:19:41.7897808Z aplikace = ServiceInstalledEvent shost = CLIENT1 msg = user1 vytvořili MaliciousService mohl spustit potenciálně škodlivé příkazy na počítači CLIENT1. externalId = 2026 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c cs2Label = aktivační událost cs2 = aktualizace

### <a name="privilege-escalation-using-forged-authorization-data"></a>Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace
10 – 29 – 2018 11:22:04 Auth.Error 192.168.0.202 1 2018-10-29T09:21:59.288337 + 00:00 DC3 CEF 3908 ForgedPacSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | ForgedPacSecurityAlert | Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace | 10 | start = 2018-10-29T09:19:43.6403358Z aplikace Kerberos suser = user1 msg = = uzivatel1 nepovedlo zvýšit oprávnění proti řadiči domény DC1 na host/domain1.test.local z počítače CLIENT1 pomocí falešných dat autorizace. externalId = 2013 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/b698d438-5013-4bca-be0b-f219f8b69108 cs2Label = aktivační událost cs2 = nový

### <a name="reconnaissance-using-account-enumeration"></a>Rekognoskace pomocí výčtu účtů
02 – 21 – 2018 16:19:35 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:27.540731 + 00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | AccountEnumerationSecurityAlert | Rekognoskace pomocí výčtu účtů | 5 | start = 2018-02 – 21T14:19:02.6045416Z app = Kerberos shost = CLIENT1 suser = LMaldonado msg = podezřelé přihlašovací aktivity výčet pomocí protokolu Kerberos, která pochází z počítače CLIENT1, a úspěšně odhadla Lamon Maldonado (softwarový inženýr). externalId = 2003 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d cs2Label = aktivační událost cs2 = nový

### <a name="reconnaissance-using-directory-services-queries"></a>Rekognoskace pomocí dotazů na adresářové služby 
02 – 21 – 2018 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | SamrReconnaissanceSecurityAlert | Rekognoskace pomocí výčtu adresářových služeb | 5 | start = 2018-02-21T14:19:41.9912772Z app = Samr shost = CLIENT1 suser = user1 outcome = Success msg = následující adresářové služby byla podniknuta výčty, které používají protokol SAMR, proti řadiči domény DC1 z CLIENT1:\r\nSuccessful výčet všech skupin v domain1.test.local uživatele User1. externalId = 2019 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label = aktivační událost cs2 = nový

### <a name="reconnaissance-using-dns"></a>Rekognoskace pomocí DNS
02 – 21 – 2018 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.063994 + 00:00 CENTER CEF 6076 DnsReconnaissanceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | DnsReconnaissanceSecurityAlert | Rekognoskace pomocí DNS | 5 | start = 2018-02-21T14:19:41.9417776Z aplikace = Dns shost = CLIENT1 požadavek ukázka dotazu requestMethod = = Axfr důvod = NoError outcome = Success msg = podezřelé DNS bylo zjištěno aktivitu pocházející z počítače CLIENT1 (což není DNS server). Dotaz byl pro ukázku dotazu (typ Axfr). Odpověď byla NoError. externalId = 2007 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c cs2Label = aktivační událost cs2 = aktualizace

### <a name="reconnaissance-using-smb-session-enumeration"></a>Rekognoskace pomocí výčtu relací SMB
02 – 21 – 2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.962930 + 00:00 CENTER CEF 6076 EnumerateSessionsSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | EnumerateSessionsSecurityAlert | Rekognoskace pomocí výčtu relací SMB | 5 | start = 2018-02-21T14:19:03.2071170Z app = SrvSvc shost = CLIENT1 msg = uživatele User1, z počítače CLIENT1 na DC1, vystavení Eugene Jenkins (uživatel2 počítač) se úspěšně provedly pokusy o výčet relací SMB . externalId = 2012 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440 cs2Label = aktivační událost cs2 = nový

### <a name="remote-code-execution-attempt"></a>Pokus o spuštění vzdáleného kódu
02 – 21 – 2018 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 CENTER CEF 6076 RemoteExecutionSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | RemoteExecutionSecurityAlert | Zjištěn pokus o vzdálené spuštění | 5 | start = 2018-02-21T14:19:41.9912772Z aplikace služby Wmi shost = = CLIENT1 suser = user1 outcome = Success msg = následující vzdálené spuštění došlo k pokusům na počítači DC1 z CLIENT1:\r\nSuccessful vzdálené spuštění služby WMI jeden nebo více metody uživatele User1. externalId = 2019 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label = aktivační událost cs2 = nový

### <a name="suspicious-authentication-failures"></a>Podezřelé chyby ověřování
02 – 21 – 2018 16:19:20 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:15.397995 + 00:00 CENTER CEF 6076 BruteForceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | BruteForceSecurityAlert | Podezřelé chyby ověřování | 5 | start = 2018-02-21T14:19:03.3831122Z app = Kerberos shost = CLIENT1 msg = podezřelá neúspěšná ověření indikující možný útok hrubou silou byly zjištěny z počítače CLIENT1. externalId = 2023 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6 cs2Label = aktivační událost cs2 = nový

### <a name="suspicious-communication-over-dns--preview"></a>Podezřelá komunikace prostřednictvím DNS – preview
10-04-2018 14:49:38 Auth.Warning 192.168.0.202 1 2018-10-04T11:49:25.954059 + 00:00 DC3 CEF 3604 DnsSuspiciousCommunicationSecuri ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.49.5589.58606 | DnsSuspiciousCommunicationSecurityAlert | [PREVIEW] Podezřelá komunikace prostřednictvím DNS | 5 | start = 2018-10-04T11:49:11.0822077Z aplikace DnsEvent dhost = suspiciousdomainname msg = CLIENT1 odeslané podezřelých dotazů DNS řešení suspiciousdomainname externalId = 2031 cs1Label = = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/0fc77777-49ca-40b3-a7ba-7644f355539e cs2Label = aktivovat cs2 = nový

### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Povýšení řadiče domény podezřelé (možný útok DcShadow)
07-12-2018 11:18:07 Auth.Error 192.168.0.200 1 2018-07-12T08:18:06.883880 + 00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.40.0.0 | DirectoryServicesRoguePromotionSecurityAlert | **Povýšení řadiče domény podezřelé (možný útok DcShadow)**| 10 | start = 2018-07-12T08:17:55.4067092Z app = Ldap shost = CLIENT1 msg = počítači CLIENT1 je počítač v domain1.test.local zaregistrovaný jako řadič domény na počítači DC1. externalId = 2028 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53 cs2Label = aktivační událost cs2 = aktualizace

### <a name="suspicious-modification-of-sensitive-groups"></a>Podezřelé úprava citlivých skupin
10 – 29 – 2018 11:21:03 Auth.Warning 192.168.0.202 1 2018-10-29T09:20:49.667014 + 00:00 DC3 CEF 3908 AbnormalSensitiveGroupMembership ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | AbnormalSensitiveGroupMembershipChangeSecurityAlert | Podezřelé úprava citlivých skupin | 5 | start = 2018-10-29T09:19:43.3013729Z aplikace GroupMembershipChangeEvent suser = user1 msg = = user1 má neobvykle upravená citlivá členství ve skupinách. externalId = 2024 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6f7e677e-f068-41e5-bada-708cd5a322b9 cs2Label = aktivační událost cs2 = nový

### <a name="suspicious-replication-of-directory-services"></a>Podezřelá replikace adresářových služeb
02 – 21 – 2018 16:21:22 Auth.Error 192.168.0.220 1 2018-02-21T14:21:13.978554 + 00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | DirectoryServicesReplicationSecurityAlert | Škodlivá replikace adresářových služeb | 10 | start = 2018-02-21T14:19:03.9975656Z aplikace Drsr shost = CLIENT1 msg = = škodlivou replikaci požadavků úspěšně provedl uživatel1, z počítače CLIENT1 proti DC1. výsledek = úspěch externalId = 2006 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7 cs2Label aktivační událost cs2 = = nový

### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Podezřelá replikace požadavku (možný útok DcShadow)
07-12-2018 11:18:37 Auth.Error 192.168.0.200 1 2018-07-12T08:18:32.265989 + 00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.40.0.0 | DirectoryServicesRogueReplicationSecurityAlert | **Podezřelá replikace požadavku (možný útok DcShadow)**| 10 | start = 2018-07-12T08:17:55.3816102Z **aplikace = aktivity replikace** shost = CLIENT1 msg = CLIENT1, která není platnou doménu. kontroler v domain1.test.local, odeslat změny objektů adresáře na počítači DC1. externalId = 2029 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515 cs2Label = aktivační událost cs2 = nový

### <a name="suspicious-service-creation"></a>Podezřelé vytvoření služby 
10 – 29 – 2018 11:20:02 Auth.Warning 192.168.0.202 1 2018-10-29T09:19:59.164874 + 00:00 DC3 CEF 3908 MaliciousServiceCreationSecurity ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | MaliciousServiceCreationSecurityAlert | Podezřelé vytvoření služby | 5 | start = 2018-10-29T09:19:44.9471965Z aplikace = ServiceInstalledEvent shost = CLIENT1 msg = user1 vytvořili MaliciousService mohl spustit potenciálně škodlivé příkazy na počítači CLIENT1. externalId = 2026 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/118bbe3d-fe72-40de-80d0-2678b68aa027 cs2Label = aktivační událost cs2 = nový

### <a name="suspicious-vpn-connection"></a>Připojení k síti VPN podezřelé
07-03-2018 13:13:12 Auth.Warning 192.168.0.200 1 2018-07-03T10:13:06.187834 + 00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.39.0.0 | AbnormalVpnSecurityAlert | Podezřelé připojení VPN | 5 | start = 2018-06-30T15:34:05.3887333Z aplikace připojení VpnConnection suser = user1 msg = = uzivatel1 připojené k síti VPN pomocí počítače se 3 ze 3 míst.     externalId = 2025 cs1Label = url cs1 =https://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68 cs2Label = aktivační událost cs2 = nový

### <a name="unusual-protocol-implementation---potential-use-of-malicious-tools-such-a-hydra"></a>Neobvyklá implementace protokolu - (potenciálně škodlivý nástroj, který tyto Hydra využití)
02 – 21 – 2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050 + 00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | AbnormalProtocolSecurityAlert | Neobvyklá implementace protokolu | 5 | start = 2018-02-21T14:19:03.1981155Z aplikace = Ntlm shost = CLIENT2 outcome = Success msg = došlo k pokusům o ověření z počítače CLIENT2 proti řadiči domény DC1 pomocí neobvyklé implementace protokolu. Může být důsledek použití škodlivých nástrojů ke spuštění útoku, třeba technikou Pass-the-Hash nebo hrubou silou. externalId = 2002 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label = aktivační událost cs2 = nový

### <a name="unusual-protocol-implementation--potential-use-of-malicious-tools-such-a-metasploit"></a>Neobvyklá implementace protokolu-(potenciálně škodlivý nástroj, který tyto Metasploit využití)
10 – 29 – 2018 11:22:04 Auth.Warning 192.168.0.202 1 2018-10-29T09:22:00.460233 + 00:00 DC3 CEF 3908 AbnormalProtocolSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | AbnormalProtocolSecurityAlert | Neobvyklá implementace protokolu (potenciální použijte Metasploit hacking nástroje) | 5 | start = 2018-10-29T09:19:46.6092465Z app = Ntlm shost = CLIENT2 outcome = Success msg = došlo k pokusům o ověření z počítače CLIENT2 proti řadiči domény DC1 pomocí neobvyklý protokol implementace. externalId = 2002 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/573f10a1-6f8a-44b1-a5b1-212d40996363 cs2Label = aktivační událost cs2 = nový

## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)