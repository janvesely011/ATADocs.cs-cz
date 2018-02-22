---
title: Odkazy na Azure protokol ATP SIEM | Microsoft Docs
description: "Poskytuje ukázky podezřelou aktivitu protokolů odeslaný Azure ATP do vašeho systému SIEM."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 5d466014d96edb2deecf0c5d7b937d9e576a57b0
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="azure-atp-siem-log-reference"></a>Odkazy na Azure protokol ATP SIEM

Azure ATP může předat podezřelé aktivity a monitorování výstrahy události do vašeho systému SIEM. Události podezřelých aktivit jsou ve formátu CEF. Tento referenční článek obsahuje ukázky protokolů podezřelých aktivit odesílaných do vašeho systému SIEM.

## <a name="sample-azure-atp-suspicious-activities-in-cef-format"></a>Ukázka Azure ATP podezřelé aktivity ve formátu CEF
Do systému SIEM se předávají následující pole a jejich hodnoty:

-   start – počáteční čas výstrahy
-   suser – účet (obvykle by to měl být uživatelský účet), kterého se tato výstraha týká
-   shost – zdrojový počítač pro tuto výstrahu
-   outcome – pro výstrahy s informacemi, jestli se jedná o úspěch nebo selhání aktivity v dané výstraze  
-   msg – popis výstrahy
-   CNT – pro výstrahy, které mají a počet pokusů, které výstrahy se stalo (například hrubou silou s částkou odhadované hesel)
-   app – protokol použitý ve výstraze
-   externalId – událost ID Azure ATP zapíše do protokolu událostí, která odpovídá této výstrahy
-   cs#label & cs# – jedná se o řetězce zákazníků, které umožňuje CEF použít, cs#label je název nového pole a cs# je hodnota, například: cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

V tomto příkladu je cs1 pole s adresou URL výstrahy.

## <a name="sample-logs"></a>Ukázky protokolů

Následující příklad protokoly v souladu s RFC 5242, ale Azure ATP také podporuje RFC 3164.

Priority:

- 3 = nízká
- 5 = střední
- 10 = vysoká

### <a name="bruteforce--ldap"></a>BruteForce – LDAP
02-21-2018 16:20:21 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:06.156238 + 00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | LdapBruteForceSecurityAlert | Útoku hrubou silou použití jednoduché vazby protokolu LDAP | 5 | spustit = 2018-02-21T14:19:41.7422810Z aplikaci = Ldap suser Wofford Thurston shost = = CLIENT1 msg = útoku hrubou silou na Wofford Thurston (softwaru pracovníka) pomocí protokolu Ldap protokolu došlo k pokusu o z počítače CLIENT1 (100 odhad počet pokusů o). cnt=100 externalId=2004 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a


### <a name="bruteforce"></a>BruteForce
02-21-2018 16:19:20 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:15.397995 + 00:00 CENTER CEF 6076 BruteForceSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | BruteForceSecurityAlert | Počet selhání ověření podezřelé | 5 | start = 2018-02-21T14:19:03.3831122Z aplikace Kerberos shost = = CLIENT1 msg = selhání podezřelé ověřování indikující možný útok hrubou silou byly zjištěny z počítače CLIENT1. externalId=2023 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6
### <a name="privilege-escalation"></a>Zvýšení oprávnění
#### <a name="silver"></a>Silver (Stříbrná)
02-21-2018 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:15.186167 + 00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | ForgedPacSecurityAlert | Pomocí zvýšení oprávnění forged data autorizace | 10 | start = 2018-02-aplikace 21T14:19:02.8595383Z = suser protokolu Kerberos = uživatel1 msg = uživatel1 pokus o zvýšení oprávnění k host/domain1.test.local z počítače CLIENT1 pomocí podvržené autorizační data. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/029189e1-6bb4-490b-bcaf-5fac4457e9f3
#### <a name="gold"></a>Zlatá
02-21-2018 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:14.358037 + 00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | ForgedPacSecurityAlert | Pomocí zvýšení oprávnění forged data autorizace | 10 | spustit = 2018-02-21T14:19:02.8595383Z aplikaci = suser protokolu Kerberos = uživatel1 msg = uživatel1 zvýšení oprávnění vůči řadiči domény DC1 na host/domain1.test.local z počítače CLIENT1 pomocí podvržené autorizační data se nezdařilo. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f3359eff-cb59-44b9-82b6-5e82ff06e6c8
### <a name="golden-ticket"></a>Zlatý lístek
02-21-2018 16:22:39 Auth.Error 192.168.0.220 1 2018-02-21T14:22:34.274054 + 00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | GoldenTicketSecurityAlert | Zlatý lístek protokolu Kerberos aktivity | 10 | spustit = 2018-02-21T14:19:03.2416152Z aplikaci = suser protokolu Kerberos = Lanell Campos msg = podezřelé použití lístek protokolu Kerberos Lanell Campos (pracovník softwaru) je, indikující možný útok zlatý lístek, byla zjištěna. externalId=2022 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0
### <a name="honey-token-activity"></a>Aktivita Honey Token
02-21-2018 16:20:36 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:34.106162 + 00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | HoneytokenActivitySecurityAlert | Aktivita Honeytokenu | 5 | spustit = 2018-02-21T14:20:26.6705617Z aplikace = suser protokolu Kerberos = med msg = následující aktivity se provádí med: \r\nLogged v na počítači KLIENT2 prostřednictvím DC1. externalId=2014 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c
### <a name="suspicious-replication-of-directory-services"></a>Podezřelá replikace adresářových služeb
02-21-2018 16:21:22 Auth.Error 192.168.0.220 1 2018-02-21T14:21:13.978554 + 00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | DirectoryServicesReplicationSecurityAlert | Škodlivou replikaci adresářových služeb | 10 | spustit = 2018-02-21T14:19:03.9975656Z aplikace = Drsr shost = CLIENT1 msg = škodlivou replikaci požadavky byly úspěšně provádí uživatel1, z počítače CLIENT1 proti DC1. outcome=Success externalId=2006 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7
### <a name="malicious-data-protection-private-information-request"></a>Škodlivá žádost o soukromé informace přes Data Protection
02-21-2018 16:22:08 Auth.Error 192.168.0.220 1 2018-02-21T14:21:54.080266 + 00:00 CENTER CEF 6076 RetrieveDataProtectionBackupKeyS ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | RetrieveDataProtectionBackupKeySecurityAlert | Škodlivý požadavek na Data Protection soukromé informace | 10 | spustit = 2018-02-21T14:19:41.8382786Z aplikace = LsaRpc shost = CLIENT1 msg = uživatel1 provést 1 úspěšné pokusí z počítače CLIENT1 DPAPI domény záložní klíč načíst z řadiče domény DC1. externalId=2020 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/b22221d1-764a-4fae-a5ce-e6a0c69dc55a

### <a name="over-pass-the-hash"></a>Over-pass-the-hash
02-21-2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Přechod na starší verzi aktivity šifrování | 5 | spustit = 2018-02-21T14:19:41.8737870Z aplikace = msg protokolu Kerberos = metodu šifrování Encrypted_Timestamp pole AS_REQ byla snížit zpráv z počítače CLIENT1, na základě dřív zjištěné chování. Může to být důsledek krádeže přihlašovacích údajů s pomocí Overpass-the-Hash z počítače CLIENT1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2
### <a name="pass-the-hash"></a>Pass-the-hash
02-21-2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | PassTheHashSecurityAlert | Krádeži identity pomocí útoku Pass-the-Hash | 10 | spustit = 2018-02-aplikace 21T15:02:22.2577465Z = suser protokolu Kerberos = Eugene volaných msg = Eugene volaných (softwaru pracovníka) na hodnotu hash byla odcizení z jednoho z počítačů ve volaných Eugene (Software v dříve zaznamenaných do Pracovník) a použít v počítači CLIENT1. externalId=2017 cs1Label=url cs1=https://test-syslog.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd
### <a name="account-enumeration"></a>Výčet účtů
02-21-2018 16:19:35 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:27.540731 + 00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | AccountEnumerationSecurityAlert | Rekognoskace pomocí zjišťování účtů | 5 | start = 2018-02-21T14:19:02.6045416Z aplikace Kerberos shost = = CLIENT1 suser = LMaldonado msg = podezřelé účet výčtu aktivity pomocí protokolu Kerberos, pocházející z počítače CLIENT1, se zjištěnými a úspěšně uhádnout Lamon Maldonado (pracovník softwaru). externalId=2003 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d
### <a name="dns-recon"></a>Rekognoskace DNS
02-21-2018 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.063994 + 00:00 CENTER CEF 6076 DnsReconnaissanceSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | DnsReconnaissanceSecurityAlert | Rekognoskace pomocí DNS | 5 | start = 2018-02-21T14:19:41.9417776Z aplikace Dns shost = = CLIENT1 požadavek = ukázkový dotaz requestMethod = důvod Axfr = NoError výsledek = úspěch msg = podezřelé DNS zjištěnými aktivity, pocházející z počítače CLIENT1 (který není DNS server). Dotaz byl pro ukázkový dotaz (typ Axfr). Odpověď byla NoError. externalId=2007 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c


### <a name="smb-session-enumeration"></a>Výčet relací SMB
02-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.962930 + 00:00 CENTER CEF 6076 EnumerateSessionsSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EnumerateSessionsSecurityAlert | Rekognoskace pomocí výčet relací SMB | 5 | spustit = 2018-02-21T14:19:03.2071170Z aplikace = SrvSvc shost = CLIENT1 msg = relace protokolu SMB. pokusy o výčet byly úspěšně provádí uživatel1, z počítače CLIENT1 proti počítači DC1 vystavení Eugene volaných (uživatel2 počítače) . externalId=2012 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440
### <a name="sam-r-enumeration"></a>SAM-R – výčet
02-21-2018 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | SamrReconnaissanceSecurityAlert | Rekognoskace pomocí výčtem adresářů služby | 5 | spustit = 2018-02-21T14:19:41.9912772Z aplikace Samr shost = = CLIENT1 suser = uživatel1 výsledek = úspěch msg = výčty pomocí protokolu SAMR pokusů o proti DC1 z následující adresářovými službami CLIENT1:\r\nSuccessful výčet všech skupin v domain1.test.local uživatele User1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="remote-execution"></a>Vzdálené spuštění
02-21-2018 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 CENTER CEF 6076 RemoteExecutionSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | RemoteExecutionSecurityAlert | Pokus o vzdálené spuštění zjistil | 5 | start = 2018-02-21T14:19:41.9912772Z aplikace Wmi shost = = CLIENT1 suser = uživatel1 výsledek = úspěch msg = následující vzdálené spuštění pokusy o provedených na řadiči domény DC1 ze vzdálené spuštění CLIENT1:\r\nSuccessful jeden nebo více rozhraní WMI metody uživatele User1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="skeleton-key"></a>Skeleton Key
02-21-2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Přechod na starší verzi aktivity šifrování | 5 | spustit = 2018-02-21T14:19:41.8737870Z aplikace = msg protokolu Kerberos = metodu šifrování ETYPE_INFO2 pole KRB_ERR byla snížit zpráv z počítače CLIENT1, na základě dřív zjištěné chování. To může být výsledek typu Skeleton Key na počítači DC1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2

### <a name="unusual-protocol-implementation"></a>Neobvyklá implementace protokolu
02-21-2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050 + 00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | AbnormalProtocolSecurityAlert | Neobvyklá implementace protokolu | 5 | start = 2018-02-21T14:19:03.1981155Z aplikace Ntlm shost = = CLIENT2 výsledek = úspěch msg = existuje byly pokusy o ověření z CLIENT2 proti DC1 pomocí neobvyklá implementace protokolu. Může se jednat o důsledek použití škodlivých nástrojů ke spuštění útoku, jako je například Pass-the-Hash nebo útok hrubou silou. externalId=2002 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4

### <a name="malicious-service-creation"></a>Vytvoření škodlivý služby
02-21-2018 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.254930 + 00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | MaliciousServiceCreationSecurityAlert | Vytvoření podezřelé služby | 5 | spustit = 2018-02-21T14:19:41.7897808Z aplikace = ServiceInstalledEvent shost = CLIENT1 msg = uživatel1 vytvořit MaliciousService provádění potenciálně škodlivého příkazy na počítači CLIENT1. externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c

### <a name="pass-the-ticket"></a>Pass-the-ticket

02-21-2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | PassTheTicketSecurityAlert | Krádeži identity pomocí útoku Pass-the-Ticket | 10 | spustit = 2018-02-aplikace 21T15:02:22.2577465Z = suser protokolu Kerberos = Eugene volaných msg = Kerberos Eugene volaných (pracovník softwaru) pro lístky byly odcizení z počítače správce k počítači Victom a slouží k přístupu k krbtgt/Doména1. TEST. MÍSTNÍ. externalId=2017 cs1Label=url cs1=https://contoso-corp.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd


## <a name="see-also"></a>Viz také
- [Požadavky Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)