---
title: Referenční informace k protokolům Azure ATP SIEM | Dokumentace Microsoftu
description: Obsahuje ukázky protokolů podezřelých aktivit odeslaných ze služby Azure ATP do vašeho systému SIEM.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/17/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: eeb158ed3da07b57a3071b5fa9f60b8ec9d20db7
ms.sourcegitcommit: 9252c74620abb99d8fa2b8d2cc2169018078bec9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/18/2019
ms.locfileid: "58136888"
---
# <a name="azure-atp-siem-log-reference"></a>Referenční informace k protokolům Azure ATP SIEM

Ochrana ATP v programu Azure můžete dál zabezpečení výstrahy a monitorování výstrahy události do vašeho systému SIEM. Výstrahy a události jsou ve formátu CEF. Tento referenční článek obsahuje ukázky protokolů odeslané do vašeho systému SIEM.

## <a name="sample-azure-atp-security-alerts-in-cef-format"></a>Ukázka služby Azure ATP výstrah zabezpečení ve formátu CEF
Do systému SIEM se předávají následující pole a jejich hodnoty:

|Podrobnosti|Vysvětlení|
|---------|---------------|
|Spuštění|Počáteční čas výstrahy|
|suser|účet (obvykle uživatelský účet) účastnící se upozornění|
|účet počítače|účet (obvykle uživatelský účet) účastnící se upozornění|
|Výsledek|Pokud je to relevantní, úspěch nebo neúspěch podezřelých aktivit ve výstraze|
|msg|popis výstrahy|
|CNT|pro výstrahy, které mají počet, kolikrát, aktivity, ke kterým došlo (například útok hrubou silou má určité množství uhodnutí hesel)|
|Aplikace |protokol použitý ve výstraze|
|externalId|Typ události ID Azure ATP zapíše do protokolu událostí, která odpovídá pro každý typ výstrahy|
|cs #label|řetězce zákazníků, které jsou povoleny ve formátu CEF, kde cs #label je název nového pole |
|cs #|povolené ve formátu CEF, kde cs # je hodnota řetězce zákazníků.|
|
- Například: cs1Label = url cs1 = https\://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
<br> Cs1 pole je adresa URL výstrahy. 

- Příklad: cs2Label = aktivační událost cs2 = nový
<br> Pole cs2 identifikuje, pokud je výstraha nové nebo aktualizované.


> [!NOTE]
> Pokud budete chtít vytvořit automatizace nebo skriptů pro protokolů SIEM ochrany ATP v programu Azure, doporučujeme použít **externalId** pole k identifikaci typu výstrahy místo názvu upozornění pro tento účel. Upozornění názvy mohou být občas upravit, zatímco **externalId** jednotlivých výstrah je trvalá.  

## <a name="azure-atp-security-alert-unique-externalids"></a>Azure ATP zabezpečení výstrah jedinečný externalIds

> [!div class="mx-tableFixed"] 

|Nový název výstrahy zabezpečení|Předchozí název výstrahy zabezpečení|Jedinečné ID externí|MITRE ATT&CK Matrix™ |
|---------|----------|---------|---------|
|[Rekognoskace výčtu účtů](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|Rekognoskace pomocí výčtu účtů|2003|Zjišťování|
|[Průsak dat ven přes protokol SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)| Není k dispozici| 2030|Průsak ven,<br>Laterální pohyb<br>Příkazy a ovládání|
|[Aktivita Honeytokenu](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|Aktivita Honeytokenu|2014||
|[Škodlivá žádost Data Protection API hlavní klíč](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|Škodlivá žádost o soukromé informace přes Data Protection|2020|Přihlašovací údaje přístup|
|[Mapování sondování sítě (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|Rekognoskace pomocí DNS|2007|Zjišťování|
|[Pokus o spuštění vzdáleného kódu](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|Pokus o spuštění vzdáleného kódu|2019|Spuštění,<br> Trvalost,<br> Zvýšení úrovně oprávnění<br> Únik obrany<br> Laterální pohyb|
|[Vzdálené spuštění kódu v DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|Není k dispozici|2036|Zvýšení úrovně oprávnění<br> Laterální pohyb|
|[Rekognoskace instančního objektu zabezpečení (LDAP) – preview](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038---preview)|Není k dispozici|2038|Přihlašovací údaje přístup|
|[Podezřelý útok hrubou silou (pomocí protokolu Kerberos, NTLM)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|Podezřelé chyby ověřování|2023|Přihlašovací údaje přístup|
|[Podezřelý útok hrubou silou (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|Útok hrubou silou pomocí jednoduché vazby LDAP.|2004|Přihlašovací údaje přístup|
|[Podezřelý útok hrubou silou (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|Neobvyklá implementace protokolu (potenciální použití škodlivých nástrojů, jako je Hydra)|2033|Laterální pohyb|
|[Podezřelý útok DCShadow (povýšení řadiče domény)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|Povýšení řadiče domény podezřelé (možný útok DCShadow)|2028|Únik obrany|
|[Podezřelý útok DCShadow (žádost o replikaci řadiče domény)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|Žádost o replikaci řadiče domény podezřelé (možný útok DCShadow)|2029|Únik obrany|
|[Podezřelý útok DCSync (replikace adresářových služeb)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|Škodlivá replikace adresářových služeb|2006||
|[Podezřelé použití lístku Golden (oslabení šifrování)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|Aktivita snížení úrovně šifrování (potenciální útok metodou golden ticket)|2009|
|[Podezřelé použití lístku Golden (falešných dat autorizace)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013) |Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace|2013|Zvýšení úrovně oprávnění<br>Laterální pohyb||
|[Podezřelé použití Golden Ticket (neexistující účet)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|Protokol Kerberos Golden Ticket - neexistující účet|2027||
|[Podezřelé použití Golden Ticket (ticket anomálií)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|Není k dispozici|2032||
|[Podezřelé použití Golden Ticket (čas anomálií)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|Kerberos Golden Ticket – čas anomálií|2022||
|[Krádež identity podezřelého softwaru (pass-the-hash)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|Krádež identity pomocí útoku Pass-the-Hash|2017|Laterální pohyb|
|[Krádež identity podezřelého softwaru (pass-the-ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|Krádež identity pomocí útoku Pass-the-Ticket|2018|Laterální pohyb|
|[Podezření na útok over-pass-the-hash (oslabení šifrování)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|Aktivita snížení úrovně šifrování (možný útok overpass-the-hash)|2008||
|[Podezření na útok overpass-the-hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|Neobvyklá implementace protokolu Kerberos (možný útok overpass-the-hash)|2002|Laterální pohyb|
|[Útoku typu skeleton key podezřelého softwaru (oslabení šifrování)](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|Aktivita snížení úrovně šifrování (potenciální útoku typu skeleton key)|2010||
|[Podezřelé použití Metasploit hacking framework](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|Neobvyklá implementace protokolu (potenciální použijte Metasploit hacking nástroje)|2034|Laterální pohyb|
|[Podezření na útok WannaCry ransomwaru](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|Neobvyklá implementace protokolu (možný útok ransomwarem WannaCry)|2035||
|[Podezření na útok relay NTLM (účet Exchange) – preview](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview)|Není k dispozici|2037||
|[Podezřelá komunikace prostřednictvím DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|Podezřelá komunikace prostřednictvím DNS|2031|Průsak ven|
|[Podezřelé úprava citlivých skupin](atp-domain-dominance-alerts.md#suspicious-modification-of-sensitive-groups-external-id-2024)|Podezřelé úprava citlivých skupin|2024|Přihlašovací údaje přístup<br>Trvalost|
|[Podezřelé vytvoření služby](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|Podezřelé vytvoření služby|2026|Spuštění,<br> Trvalost,<br> Zvýšení úrovně oprávnění<br> Únik obrany<br>Laterální pohyb|
|[Podezřelé připojení k síti VPN](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|Podezřelé připojení k síti VPN|2025|Trvalost,<br>Únik obrany|
|[Rekognoskace členství uživatelů a skupin (SAMR)](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|Rekognoskace pomocí dotazů na adresářové služby|2021|Zjišťování|
|[Uživatele a IP adres pro rekognoskaci (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|Rekognoskace pomocí výčtu relací SMB|2012|Zjišťování|

## <a name="sample-logs"></a>Ukázky protokolů

Příklady protokolu v souladu s RFC 5242 ale ochrany ATP v programu Azure podporuje také RFC 3164.

Priority:

- 3 = nízká
- 5 = střední
- 10 = vysoká

### <a name="account-enumeration-reconnaissance"></a>Rekognoskace výčtu účtů 
02 – 21 – 2018 16:19:35 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:27.540731 + 00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | AccountEnumerationSecurityAlert | Rekognoskace pomocí výčtu účtů | 5 | start = 2018-02 – 21T14:19:02.6045416Z app = Kerberos shost = CLIENT1 suser = LMaldonado msg = podezřelé přihlašovací aktivity výčet pomocí protokolu Kerberos, která pochází z počítače CLIENT1, a úspěšně odhadla Lamon Maldonado (softwarový inženýr). externalId = 2003 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d cs2Label = aktivační událost cs2 = nový

### <a name="data-exfiltration-over-smb"></a>Průsak dat ven přes protokol SMB
12. 19 2018 14:17:46 Auth.Error 127.0.0.1 1 2018-12-19T12:17:34.645993 + 00:00 DC1 CEF. 3288 SmbDataExfiltrationSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.60.0.0 | SmbDataExfiltrationSecurityAlert | [PREVIEW] Průsak dat ven přes protokol SMB | 10 | start = 2018-12-19T12:14:12.4932821Z aplikace Smb shost = CLIENT1 msg = = Eugene Jenkins (softwarový inženýr) na počítač DC2 zkopírovat podezřelé soubory na počítači CLIENT1. externalId=2030 cs1Label=url cs1=https\://contoso-corp.atp.azure.com:13000/securityAlert/3ca2ec9d-2c67-44cc-a2d6-391716611bb6 cs2Label=trigger cs2=new

### <a name="honeytoken-activity"></a>Aktivita Honeytokenu
02 – 21 – 2018 16:20:36 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:34.106162 + 00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | HoneytokenActivitySecurityAlert | Aktivita Honeytokenu | 5 | start = 2018-02-21T14:20:26.6705617Z aplikace Kerberos suser = honey msg = = následující aktivity provedl honey: \r\nLogged v na počítači KLIENT2 přes řadič domény DC1. externalId = 2014 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c cs2Label = aktivační událost cs2 = nový

### <a name="malicious-request-of-data-protection-api-master-key"></a>Škodlivá žádost Data Protection API hlavní klíč 
10 – 29 – 2018 11:22:04 Auth.Error 192.168.0.202 1 2018-10-29T09:22:00.350864 + 00:00 DC3 CEF 3908 RetrieveDataProtectionBackupKeyS ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | RetrieveDataProtectionBackupKeySecurityAlert | Škodlivá žádost o informace soukromé ochrany dat | 10 | start = 2018-10-29T09:19:45.6307993Z app = LsaRpc shost = CLIENT1 msg = uzivatel1 provést 1 úspěšné pokusy o z počítače CLIENT1 načíst záložní klíč domény DPAPI z DC1. externalId = 2020 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/2f5717cb-2434-4d54-8af4-b2c6d14bc15c cs2Label = aktivační událost cs2 = nový

### <a name="network-mapping-reconnaissance-dns"></a>Rekognoskace mapování sítě (DNS)
10 – 29 – 2018 11:20:02 Auth.Warning 192.168.0.202 1 2018-10-29T09:19:59.056894 + 00:00 DC3 CEF 3908 DnsReconnaissanceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | DnsReconnaissanceSecurityAlert | Rekognoskace pomocí DNS | 5 | start = 2018-10-29T09:19:43.5033765Z app = Dns shost = CLIENT1 msg = podezřelé DNS aktivity původcem, proti řadiči domény DC1 CLIENT1 (což není DNS server). externalId = 2007 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/23937d33-ff71-484d-be0a-3c417fe573ce cs2Label = aktivační událost cs2 = nový

### <a name="reconnaissance-using-directory-services-queries"></a>Rekognoskace pomocí dotazů na adresářové služby 
02 – 21 – 2018 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | SamrReconnaissanceSecurityAlert | Rekognoskace pomocí výčtu adresářových služeb | 5 | start = 2018-02-21T14:19:41.9912772Z app = Samr shost = CLIENT1 suser = user1 outcome = Success msg = následující adresářové služby byla podniknuta výčty, které používají protokol SAMR, proti řadiči domény DC1 z CLIENT1:\r\nSuccessful výčet všech skupin v domain1.test.local uživatele User1. externalId = 2019 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0 cs2Label aktivační událost cs2 = = nový

### <a name="remote-code-execution-attempt"></a>Pokus o spuštění vzdáleného kódu
10 – 29 – 2018 11:22:04 Auth.Warning 192.168.0.202 1 2018-10-29T09:22:00.100856 + 00:00 DC3 CEF 3908 RemoteExecutionSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | RemoteExecutionSecurityAlert | Pokus o spuštění vzdáleného kódu | 5 | start = 2018-10-29T09:19:45.0552367Z shost = CLIENT1 msg = následující vzdálené spuštění kódu došlo k pokusům na počítači DC1 z CLIENT1:\r\nSuccessful vzdálené plánování jeden nebo více úloh podle user1.\r\nFailed vzdálené jeden nebo více úloh plánování podle user1.\r\nSuccessful vzdálené spuštění jedné nebo více metod WMI uživatele User1. externalId = 2019 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/f063c778-830c-4e9f-98d1-bc6c11c94e11 cs2Label aktivační událost cs2 = = nový

### <a name="remote-code-execution-over-dns"></a>Vzdálené spuštění kódu v DNS
1-17 – 2019 08:24:54 Auth.Warning 192.168.0.202 1 2019-01-17T08:24:54.100856 + 00:00 DC3 CEF 3908 DnsRemoteCodeExecutionSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.63.0.0 | DnsRemoteCodeExecutionSecurityAlert | [PREVIEW] Vzdálené spuštění kódu přes DNS | 5 | start = 2019-01-17T08:24:54.5293800Z app = Dns shost = CLIENT1 msg = prvek "actor" se pokusil spustit příkazy vzdáleně na počítači CLIENT1 od řadiče domény DC1, protokolu DNS. externalId=2036 cs1Label=url cs1=https\:////contoso-corp.atp.azure.com:13000/securityAlert/591f9769-d904-40b1-89fa-c307c2ca814f cs2Label=trigger cs2=new

### <a name="security-principal-reconnaissance-ldap---preview"></a>Rekognoskace instančního objektu zabezpečení (LDAP) – preview 
02-18-2019 16:48:08 Auth.Warning 127.0.0.1 1 2019-02-18T14:48:02.912264 + 00:00 DC1 CEF 4656 LdapSearchReconnaissanceSecurity ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.66.0.0 | LdapSearchReconnaissanceSecurityAlert | [PREVIEW] Rekognoskace pomocí dotazů protokolu LDAP | 5 | start = 2019-02-18T14:46:29.4644276Z aplikace ldapsearch – shost = CLIENT1 msg = = prvek "actor" na počítači CLIENT1 odeslané podezřelých dotazů protokolu LDAP na řadiče domény DC1, hledání pro 4 typy výčet a Server Operators (členové mohou spravovat domény servery) v 2 domén externalId = 2038 cs1Label = url cs1 = https\://contoso-corp.atp.azure..com:13000/securityAlert/81ea99c4-ce1f-4581-ac8f-7440fbed7cd0 cs2Label = aktivační událost cs2 = nový

### <a name="suspected-brute-force-attack-ldap"></a>Podezřelý útok hrubou silou (LDAP)
02 – 21 – 2018 16:20:21 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:06.156238 + 00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | LdapBruteForceSecurityAlert | Útok hrubou silou pomocí jednoduché vazby LDAP | 5 | start = 2018-02-21T14:19:41.7422810Z app = Ldap suser Wofford Thurston shost = = CLIENT1 msg = na Wofford Thurston (softwarový inženýr) pomocí protokolu Ldap protokolu došlo k pokusu o útok hrubou silou z počítače CLIENT1 (100 odhad pokusy o). CNT = 100 externalId = 2004 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a cs2Label = aktivační událost cs2 = aktualizace

### <a name="suspected-brute-force-attack-kerberos-ntlm"></a>Podezřelý útok hrubou silou (pomocí protokolu Kerberos, NTLM)
10 – 29 – 2018 11:20:47 Auth.Warning 192.168.0.202 1 2018-10-29T09:20:44.478827 + 00:00 DC3 CEF 3908 BruteForceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | BruteForceSecurityAlert | Podezřelé chyby ověřování | 5 | start = 2018-10-29T09:19:44.9512286Z app = Kerberos shost = CLIENT1 msg = podezřelá neúspěšná ověření indikující možný útok hrubou silou byly zjištěny z počítače CLIENT1. externalId=2023 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/85042c8e-27fa-49b3-8667-dabc1aa31580 cs2Label=trigger cs2=new

### <a name="suspected-golden-ticket-usage-encryption-downgrade"></a>Podezřelé použití lístku Golden (oslabení šifrování)
10 – 29 – 2018 11:25:07 Auth.Warning 192.168.0.202 1 2018-10-29T09:25:01.007701 + 00:00 DC3 CEF 3908 GoldenTicketEncryptionDowngradeS ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | GoldenTicketEncryptionDowngradeSecurityAlert | Aktivita snížení úrovně šifrování (potenciální útok metodou golden ticket) | 5 | start = 2018-10-29T09:37:49.0849130Z aplikace = Kerberos msg = W10. 000007 okruh používá slabší metodu šifrování (RC4), v žádosti o službu pomocí protokolu Kerberos (TGS_REQ), z W10-000007 – nástroje pro přístup k Host/domain1.test.Local. externalId = 2009 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/f01f8403-88b2-437e-b4ad-d72485fe05ac cs2Label = aktivační událost cs2 = nový

### <a name="suspected-golden-ticket-usage-non-existent-account"></a>Podezřelé použití Golden Ticket (neexistující účet)
07-01-2018 14:28:49 Auth.Error 192.168.0.100 1 2018-07-01T11:28:35.546638 + 00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.39.0.0 | ForgedPrincipalSecurityAlert | Kerberos Golden Ticket - neexistujících účtů | 10 | start = 2018-07-01T09:48:31.2567987Z app = Kerberos suser=domain1.test.local\fake msg=domain1.test.local\fake, který neexistuje v Active Directory, používá lístek protokolu Kerberos. -The-ticket byla zjištěna z 2 počítače přístup k prostředkům 3. To může znamenat potenciální útok metodou Golden Ticket. externalId = 2027 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4 cs2Label = aktivační událost cs2 = aktualizace

### <a name="suspected-golden-ticket-usage-ticket-anomaly"></a>Podezřelé použití Golden Ticket (ticket anomálií) 
1 2018-11-18T10:46:23.346946 + 00:00 MAXIMG 7050 CEF 24284 GoldenTicketSizeAnomalySecurityA 0 | Microsoft | Ochrana ATP v programu Azure | 2.56.0.0 | GoldenTicketSizeAnomalySecurityAlert | [PREVIEW] Podezřelé použití Golden Ticket (ticket anomálií) | 10 | start = 2018-11-18T10:44:12.9317797Z app = Kerberos shost CLIENT2 suser = RFosdyke msg = = Renzo Fosdyke (softwarový inženýr) pro přístup k ldap/domain1.test.local podezřelé lístek Kerberos z počítače CLIENT2. externalId =. 2032 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com:13000/securityAlert/63600e03-f423-49bf-a92d-4010e1d52b9f cs2Label = aktivační událost cs2 = aktualizace

### <a name="suspected-golden-ticket-usage-time-anomaly"></a>Podezřelé použití Golden Ticket (čas anomálií) 
02 – 21 – 2018 16:22:39 Auth.Error 192.168.0.220 1 2018-02-21T14:22:34.274054 + 00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | GoldenTicketSecurityAlert | Aktivita zlatého lístku Kerberos | 10 | start = 2018-02-21T14:19:03.2416152Z aplikace Kerberos suser = Lanell Campos msg = = podezřelé využití lístku Kerberos Lanell Campos (softwarový inženýr) společnosti, která potenciální útok metodou Golden Ticket, byla zjištěna. externalId = 2022 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0 cs2Label = aktivační událost cs2 = aktualizace

### <a name="suspected-golden-ticket-usage-forged-authorization-data"></a>Podezřelé použití lístku Golden (falešných dat autorizace) 
10 – 29 – 2018 11:22:04 Auth.Error 192.168.0.202 1 2018-10-29T09:21:59.288337 + 00:00 DC3 CEF 3908 ForgedPacSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | ForgedPacSecurityAlert | Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace | 10 | start = 2018-10-29T09:19:43.6403358Z aplikace Kerberos suser = user1 msg = = uzivatel1 nepovedlo zvýšit oprávnění proti řadiči domény DC1 na host/domain1.test.local z počítače CLIENT1 pomocí falešných dat autorizace. externalId = 2013 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/b698d438-5013-4bca-be0b-f219f8b69108 cs2Label = aktivační událost cs2 = nový

### <a name="suspected-identity-theft-pass-the-hash"></a>Krádež identity podezřelého softwaru (Pass-the-Hash)
02 – 21 – 2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | PassTheHashSecurityAlert | Krádež identity pomocí útoku Pass-the-Hash | 10 | start = 2018-02-21T15:02:22.2577465Z aplikace Kerberos suser = = msg Eugene Jenkins = Eugene Jenkins (softwarový inženýr). hodnota hash byla ukradena z jednoho počítače dříve přihlašující Eugene Jenkins (Software Inženýr) a použít z počítače CLIENT1. externalId = 2017 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label = aktivační událost cs2 = aktualizace

### <a name="suspected-identity-theft-pass-the-ticket"></a>Krádež identity podezřelého softwaru (Pass-the-Ticket) 
02 – 21 – 2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | PassTheTicketSecurityAlert | Krádež identity pomocí útoku Pass-the-Ticket | 10 | start = 2018-02-21T15:02:22.2577465Z aplikace = Kerberos suser = msg Eugene Jenkins = Kerberos Eugene Jenkins (softwarový inženýr) pro lístky byly odcizeny z Admin-PC do Victim-PC a používá pro přístup k účtu krbtgt/Doména1. TEST. MÍSTNÍ. externalId = 2018 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd cs2Label = aktivační událost cs2 = nový

### <a name="suspected-over-pass-the-hash-attack-encryption-downgrade"></a>Podezření na útok over-pass-the-Hash (oslabení šifrování) 
02 – 21 – 2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Aktivita související s oslabením šifrování | 5 | start = 2018-02-21T14:19:41.8737870Z aplikace = Kerberos msg = metodu šifrování pole Encrypted_Timestamp v AS_REQ byla snížena zpráv z počítače CLIENT1, na základě dřív zjištěné chování. Může to být důsledek krádeže přihlašovacích údajů s pomocí Overpass-the-Hash z počítače CLIENT1. externalId=2008 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=update

### <a name="suspected-skeleton-key-attack-encryption-downgrade"></a>Podezřelý útoku typu Skeleton Key (oslabení šifrování) 
02 – 21 – 2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Aktivita související s oslabením šifrování | 5 | start = 2018-02-21T14:19:41.8737870Z aplikace = Kerberos msg = metodu šifrování pole ETYPE_INFO2 KRB_ERR byl downgradovat zpráv z počítače CLIENT1, na základě dřív zjištěné chování. To může být důsledek Skeleton Key na řadič domény DC1. externalId=2010 cs1Label=url cs1=https\://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2 cs2Label=trigger cs2=new

### <a name="suspected-dcsync-attack-replication-of-directory-services"></a>Podezřelý útok DCSync (replikace adresářových služeb)
02 – 21 – 2018 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.254930 + 00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | MaliciousServiceCreationSecurityAlert | Podezřelé vytvoření služby | 5 | start = 2018-02-21T14:19:41.7897808Z aplikace = ServiceInstalledEvent shost = CLIENT1 msg = user1 vytvořili MaliciousService mohl spustit potenciálně škodlivé příkazy na počítači CLIENT1. externalId = 2026 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c cs2Label = aktivační událost cs2 = aktualizace

### <a name="suspicious-authentication-failures"></a>Podezřelé chyby ověřování
02 – 21 – 2018 16:19:20 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:15.397995 + 00:00 CENTER CEF 6076 BruteForceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | BruteForceSecurityAlert | Podezřelé chyby ověřování | 5 | start = 2018-02-21T14:19:03.3831122Z app = Kerberos shost = CLIENT1 msg = podezřelá neúspěšná ověření indikující možný útok hrubou silou byly zjištěny z počítače CLIENT1. externalId = 2023 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6 cs2Label = aktivační událost cs2 = nový

### <a name="suspicious-communication-over-dns"></a>Podezřelá komunikace prostřednictvím DNS
10-04-2018 14:49:38 Auth.Warning 192.168.0.202 1 2018-10-04T11:49:25.954059 + 00:00 DC3 CEF 3604 DnsSuspiciousCommunicationSecuri ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.49.5589.58606 | DnsSuspiciousCommunicationSecurityAlert | Podezřelá komunikace prostřednictvím DNS | 5 | start = 2018-10-04T11:49:11.0822077Z aplikace DnsEvent dhost = suspiciousdomainname msg = CLIENT1 odeslané podezřelých dotazů DNS řešení suspiciousdomainname externalId = 2031 cs1Label = = url cs1 = https\:/ / contoso-corp.atp.azure.com/securityAlert/0fc77777-49ca-40b3-a7ba-7644f355539e cs2Label = aktivační událost cs2 = nový

### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Povýšení řadiče domény podezřelé (možný útok DcShadow)
07-12-2018 11:18:07 Auth.Error 192.168.0.200 1 2018-07-12T08:18:06.883880 + 00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.40.0.0 | DirectoryServicesRoguePromotionSecurityAlert | **Povýšení řadiče domény podezřelé (možný útok DcShadow)**| 10 | start = 2018-07-12T08:17:55.4067092Z app = Ldap shost = CLIENT1 msg = počítači CLIENT1 je počítač v domain1.test.local zaregistrovaný jako řadič domény na počítači DC1. externalId = 2028 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53 cs2Label = aktivační událost cs2 = aktualizace

### <a name="suspicious-modification-of-sensitive-groups"></a>Podezřelé úprava citlivých skupin
10 – 29 – 2018 11:21:03 Auth.Warning 192.168.0.202 1 2018-10-29T09:20:49.667014 + 00:00 DC3 CEF 3908 AbnormalSensitiveGroupMembership ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | AbnormalSensitiveGroupMembershipChangeSecurityAlert | Podezřelé úprava citlivých skupin | 5 | start = 2018-10-29T09:19:43.3013729Z aplikace GroupMembershipChangeEvent suser = user1 msg = = user1 má neobvykle upravená citlivá členství ve skupinách. externalId = 2024 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/6f7e677e-f068-41e5-bada-708cd5a322b9 cs2Label = aktivační událost cs2 = nový

### <a name="suspicious-replication-of-directory-services"></a>Podezřelá replikace adresářových služeb
02 – 21 – 2018 16:21:22 Auth.Error 192.168.0.220 1 2018-02-21T14:21:13.978554 + 00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | DirectoryServicesReplicationSecurityAlert | Škodlivá replikace adresářových služeb | 10 | start = 2018-02-21T14:19:03.9975656Z aplikace Drsr shost = CLIENT1 msg = = škodlivou replikaci požadavků úspěšně provedl uživatel1, z počítače CLIENT1 proti DC1. výsledek = úspěch externalId = 2006 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7 cs2Label aktivační událost cs2 = = nový

### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Podezřelá replikace požadavku (možný útok DcShadow)
07-12-2018 11:18:37 Auth.Error 192.168.0.200 1 2018-07-12T08:18:32.265989 + 00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.40.0.0 | DirectoryServicesRogueReplicationSecurityAlert | **Podezřelá replikace požadavku (možný útok DcShadow)**| 10 | start = 2018-07-12T08:17:55.3816102Z **aplikace = aktivity replikace** shost = CLIENT1 msg = CLIENT1, která není platnou doménu. kontroler v domain1.test.local, odeslat změny objektů adresáře na počítači DC1. externalId = 2029 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515 cs2Label = aktivační událost cs2 = nový

### <a name="suspicious-service-creation"></a>Podezřelé vytvoření služby 
10 – 29 – 2018 11:20:02 Auth.Warning 192.168.0.202 1 2018-10-29T09:19:59.164874 + 00:00 DC3 CEF 3908 MaliciousServiceCreationSecurity ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.52.5704.46184 | MaliciousServiceCreationSecurityAlert | Podezřelé vytvoření služby | 5 | start = 2018-10-29T09:19:44.9471965Z aplikace = ServiceInstalledEvent shost = CLIENT1 msg = user1 vytvořili MaliciousService mohl spustit potenciálně škodlivé příkazy na počítači CLIENT1. externalId = 2026 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/118bbe3d-fe72-40de-80d0-2678b68aa027 cs2Label = aktivační událost cs2 = nový

### <a name="suspicious-vpn-connection"></a>Připojení k síti VPN podezřelé
07-03-2018 13:13:12 Auth.Warning 192.168.0.200 1 2018-07-03T10:13:06.187834 + 00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.39.0.0 | AbnormalVpnSecurityAlert | Podezřelé připojení VPN | 5 | start = 2018-06-30T15:34:05.3887333Z aplikace připojení VpnConnection suser = user1 msg = = uzivatel1 připojené k síti VPN pomocí počítače se 3 ze 3 míst.     externalId = 2025 cs1Label = url cs1 = https\://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68 cs2Label = aktivační událost cs2 = nový

### <a name="suspected-wannacry-ransomware-attack"></a>Podezření na útok WannaCry ransomwaru
02 – 21 – 2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050 + 00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | AbnormalProtocolSecurityAlert | SuspectedWannaCryRansomwareAttack | 5 | start = 2018-02-21T14:19:03.1981155Z aplikace = Ntlm shost = CLIENT2 outcome = Success msg = došlo k pokusům o ověření z počítače CLIENT2 proti řadiči domény DC1 pomocí neobvyklé implementace protokolu. Může být důsledek použití škodlivých nástrojů ke spuštění útoku, třeba technikou WannaCry. externalId = 2035 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label = aktivační událost cs2 = nový

### <a name="suspected-brute-force-attack-smb"></a>Podezřelý útok hrubou silou (SMB)
002 – 21 – 2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050 + 00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | AbnormalProtocolSecurityAlert | SuspectedBrutForceAttack | 5 | start = 2018-02-21T14:19:03.1981155Z aplikace = Ntlm shost = CLIENT2 outcome = Success msg = došlo k pokusům o ověření z počítače CLIENT2 proti řadiči domény DC1 pomocí neobvyklé implementace protokolu. Může být důsledek použití škodlivých nástrojů ke spuštění útoku, třeba technikou Hydra. externalId = roku 2033 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label = aktivační událost cs2 = nový

### <a name="suspected-use-of-metasploit-hacking-framework"></a>Podezřelé použití Metasploit hacking framework
002 – 21 – 2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050 + 00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | AbnormalProtocolSecurityAlert | SuspectedAttackUsingMetasploit | 5 | start = 2018-02-21T14:19:03.1981155Z aplikace = Ntlm shost = CLIENT2 outcome = Success msg = došlo k pokusům o ověření z počítače CLIENT2 proti řadiči domény DC1 pomocí neobvyklé implementace protokolu. Může být důsledek použití škodlivých nástrojů ke spuštění útoku, třeba technikou Metasploit. externalId =. 2034 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label aktivační událost cs2 = = nový

### <a name="suspected-overpass-the-hash-attack-kerberos"></a>Podezření na útok overpass-the-hash (Kerberos)
002 – 21 – 2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050 + 00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | AbnormalProtocolSecurityAlert | SuspectedOverPassTheHashAttack | 5 | start = 2018-02-21T14:19:03.1981155Z aplikace = Ntlm shost = CLIENT2 outcome = Success msg = došlo k pokusům o ověření z počítače CLIENT2 proti řadiči domény DC1 pomocí neobvyklé implementace protokolu. Může být výsledkem škodlivým činnostem pomocí protokolu Kerberos. externalId = 2002 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label = aktivační událost cs2 = nový

### <a name="user-and-ip-address-reconnaissance-smb"></a>Uživatele a IP adres pro rekognoskaci (SMB) 
002 – 21 – 2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050 + 00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | AbnormalProtocolSecurityAlert | ReconnaissanceusingSMBSessionEnumeration | 5 | start = 2018-02-21T14:19:03.1981155Z aplikace = Ntlm shost = CLIENT2 outcome = Success msg = došlo k pokusům o ověření z počítače CLIENT2 proti řadiči domény DC1 pomocí neobvyklé implementace protokolu. Může být důsledek použití škodlivých nástrojů ke spuštění útoku, třeba technikou Metasploit. externalId =. 2034 cs1Label = url cs1 = https\://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs2Label aktivační událost cs2 = = nový

## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
