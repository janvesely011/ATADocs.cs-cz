---
title: Referenční informace k protokolům Azure ATP SIEM | Dokumentace Microsoftu
description: Obsahuje ukázky protokolů podezřelých aktivit odeslaných ze služby Azure ATP do vašeho systému SIEM.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/20/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 9cc4c2d04e1408a1fcae6125aa1f96d7f302f5f3
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166761"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="azure-atp-siem-log-reference"></a>Referenční informace k protokolům Azure ATP SIEM

Ochrana ATP v programu Azure může předat o podezřelých aktivitách a událostech výstrah do vašeho systému SIEM monitorování. Události podezřelých aktivit jsou ve formátu CEF. Tento referenční článek obsahuje ukázky protokolů podezřelých aktivit odesílaných do vašeho systému SIEM.

## <a name="sample-azure-atp-suspicious-activities-in-cef-format"></a>Ukázky služby Azure ATP podezřelé aktivity ve formátu CEF
Do systému SIEM se předávají následující pole a jejich hodnoty:

-   start – počáteční čas výstrahy
-   suser – účet (obvykle by to měl být uživatelský účet), kterého se tato výstraha týká
-   shost – zdrojový počítač pro tuto výstrahu
-   výsledek – pro výstrahy níž se nachází o úspěch nebo selhání aktivita prováděná v dané výstraze  
-   msg – popis výstrahy
-   CNT – pro výstrahy, které mají počet případů, kdy se výstrahy došlo (například u útoku hrubou silou o uhodnutí hesel)
-   app – protokol použitý ve výstraze
-   externalId – event ID Azure ATP zapíše do protokolu událostí, který odpovídá této výstraze
-   cs #label & cs # – jedná se o řetězce zákazníků, které umožňuje CEF použít, cs #label je název nového pole a cs # je hodnota, například: cs1Label = url cs1 =https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

V tomto příkladu je cs1 pole s adresou URL výstrahy.

## <a name="sample-logs"></a>Ukázky protokolů

Následující příklad protokoly v souladu s RFC 5242 ale ochrany ATP v programu Azure podporuje také RFC 3164.

Priority:

- 3 = nízká
- 5 = střední
- 10 = vysoká

### <a name="bruteforce--ldap"></a>BruteForce – LDAP
02 – 21 – 2018 16:20:21 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:06.156238 + 00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | LdapBruteForceSecurityAlert | Útok hrubou silou pomocí jednoduché vazby LDAP | 5 | start = 2018-02-21T14:19:41.7422810Z app = Ldap suser Wofford Thurston shost = = CLIENT1 msg = na Wofford Thurston (softwarový inženýr) pomocí protokolu Ldap protokolu došlo k pokusu o útok hrubou silou z počítače CLIENT1 (100 odhad pokusy o). CNT = 100 externalId = 2004 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a


### <a name="bruteforce"></a>BruteForce
02 – 21 – 2018 16:19:20 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:15.397995 + 00:00 CENTER CEF 6076 BruteForceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | BruteForceSecurityAlert | Podezřelé chyby ověřování | 5 | start = 2018-02-21T14:19:03.3831122Z app = Kerberos shost = CLIENT1 msg = podezřelá neúspěšná ověření indikující možný útok hrubou silou byly zjištěny z počítače CLIENT1. externalId = 2023 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6
### <a name="privilege-escalation"></a>Zvýšení oprávnění
#### <a name="silver"></a>Silver (Stříbrná)
02 – 21 – 2018 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:15.186167 + 00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | ForgedPacSecurityAlert | Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace | 10 | start = 2018-02-21T14:19:02.8595383Z aplikace Kerberos suser = user1 msg = = user1 se pokusil zvýšit oprávnění na host/domain1.test.local z počítače CLIENT1 pomocí falešných dat autorizace. externalId = 2013 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/029189e1-6bb4-490b-bcaf-5fac4457e9f3
#### <a name="gold"></a>Zlatá
02 – 21 – 2018 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:14.358037 + 00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | ForgedPacSecurityAlert | Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace | 10 | start = 2018-02-21T14:19:02.8595383Z aplikace Kerberos suser = user1 msg = = uzivatel1 nepovedlo zvýšit oprávnění proti řadiči domény DC1 na host/domain1.test.local z počítače CLIENT1 pomocí falešných dat autorizace. externalId = 2013 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f3359eff-cb59-44b9-82b6-5e82ff06e6c8
### <a name="golden-ticket"></a>Zlatý lístek
02 – 21 – 2018 16:22:39 Auth.Error 192.168.0.220 1 2018-02-21T14:22:34.274054 + 00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | GoldenTicketSecurityAlert | Aktivita zlatého lístku Kerberos | 10 | start = 2018-02-21T14:19:03.2416152Z aplikace Kerberos suser = Lanell Campos msg = = podezřelé využití lístku Kerberos Lanell Campos (softwarový inženýr) společnosti, která potenciální útok metodou Golden Ticket, byla zjištěna. externalId = 2022 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0
### <a name="kerberos-golden-ticket-nonexistent-account"></a>Neexistující účet zlatý lístek protokolu Kerberos
07-01-2018 14:28:49 Auth.Error 192.168.0.100 1 2018-07-01T11:28:35.546638 + 00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.39.0.0 | ForgedPrincipalSecurityAlert | Kerberos Golden Ticket - neexistujících účtů | 10 | start = 2018-07-01T09:48:31.2567987Z app = Kerberos suser=domain1.test.local\fake msg=domain1.test.local\fake, který neexistuje v Active Directory, používá lístek protokolu Kerberos. -The-ticket byla zjištěna z 2 počítače přístup k prostředkům 3. To může znamenat potenciální útok metodou Golden Ticket. externalId = 2027 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4


### <a name="honey-token-activity"></a>Aktivita Honey Token
02 – 21 – 2018 16:20:36 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:34.106162 + 00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | HoneytokenActivitySecurityAlert | Aktivita Honeytokenu | 5 | start = 2018-02-21T14:20:26.6705617Z aplikace Kerberos suser = honey msg = = následující aktivity provedl honey: \r\nLogged v na počítači KLIENT2 přes řadič domény DC1. externalId = 2014 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c
### <a name="suspicious-replication-of-directory-services"></a>Podezřelá replikace adresářových služeb
02 – 21 – 2018 16:21:22 Auth.Error 192.168.0.220 1 2018-02-21T14:21:13.978554 + 00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | DirectoryServicesReplicationSecurityAlert | Škodlivá replikace adresářových služeb | 10 | start = 2018-02-21T14:19:03.9975656Z aplikace Drsr shost = CLIENT1 msg = = škodlivou replikaci požadavků úspěšně provedl uživatel1, z počítače CLIENT1 proti DC1. výsledek = úspěch externalId = 2006 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7
### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Podezřelá replikace požadavku (možný útok DcShadow)
07-12-2018 11:18:37 Auth.Error 192.168.0.200 1 2018-07-12T08:18:32.265989 + 00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.40.0.0 | DirectoryServicesRogueReplicationSecurityAlert | **Podezřelá replikace požadavku (možný útok DcShadow)**| 10 | start = 2018-07-12T08:17:55.3816102Z **aplikace = aktivity replikace** shost = CLIENT1 msg = CLIENT1, která není platnou doménu. kontroler v domain1.test.local, odeslat změny objektů adresáře na počítači DC1. externalId = 2029 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515
### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Povýšení řadiče domény podezřelé (možný útok DcShadow)
07-12-2018 11:18:07 Auth.Error 192.168.0.200 1 2018-07-12T08:18:06.883880 + 00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.40.0.0 | DirectoryServicesRoguePromotionSecurityAlert | **Povýšení řadiče domény podezřelé (možný útok DcShadow)**| 10 | start = 2018-07-12T08:17:55.4067092Z app = Ldap shost = CLIENT1 msg = počítači CLIENT1 je počítač v domain1.test.local zaregistrovaný jako řadič domény na počítači DC1. externalId = 2028 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53

### <a name="malicious-data-protection-private-information-request"></a>Škodlivá žádost o soukromé informace přes Data Protection
02 – 21 – 2018 16:22:08 Auth.Error 192.168.0.220 1 2018-02-21T14:21:54.080266 + 00:00 CENTER CEF 6076 RetrieveDataProtectionBackupKeyS ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | RetrieveDataProtectionBackupKeySecurityAlert | Škodlivá žádost o informace soukromé ochrany dat | 10 | start = 2018-02-21T14:19:41.8382786Z app = LsaRpc shost = CLIENT1 msg = uzivatel1 provést 1 úspěšné pokusy o z počítače CLIENT1 načíst záložní klíč domény DPAPI z DC1. externalId = 2020 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/b22221d1-764a-4fae-a5ce-e6a0c69dc55a

### <a name="over-pass-the-hash"></a>Over-pass-the-hash
02 – 21 – 2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Aktivita související s oslabením šifrování | 5 | start = 2018-02-21T14:19:41.8737870Z aplikace = Kerberos msg = metodu šifrování pole Encrypted_Timestamp v AS_REQ byla snížena zpráv z počítače CLIENT1, na základě dřív zjištěné chování. Může to být důsledek krádeže přihlašovacích údajů s pomocí Overpass-the-Hash z počítače CLIENT1. externalId = 2011 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2
### <a name="pass-the-hash"></a>Pass-the-hash
02 – 21 – 2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | PassTheHashSecurityAlert | Krádež identity pomocí útoku Pass-the-Hash | 10 | start = 2018-02-21T15:02:22.2577465Z aplikace Kerberos suser = = msg Eugene Jenkins = Eugene Jenkins (softwarový inženýr). hodnota hash byla ukradena z jednoho počítače dříve přihlašující Eugene Jenkins (Software Inženýr) a použít z počítače CLIENT1. externalId = 2017 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd
### <a name="account-enumeration"></a>Výčet účtů
02 – 21 – 2018 16:19:35 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:27.540731 + 00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | AccountEnumerationSecurityAlert | Rekognoskace pomocí výčtu účtů | 5 | start = 2018-02 – 21T14:19:02.6045416Z app = Kerberos shost = CLIENT1 suser = LMaldonado msg = podezřelé přihlašovací aktivity výčet pomocí protokolu Kerberos, která pochází z počítače CLIENT1, a úspěšně odhadla Lamon Maldonado (softwarový inženýr). externalId = 2003 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d
### <a name="dns-recon"></a>Rekognoskace DNS
02 – 21 – 2018 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.063994 + 00:00 CENTER CEF 6076 DnsReconnaissanceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | DnsReconnaissanceSecurityAlert | Rekognoskace pomocí DNS | 5 | start = 2018-02-21T14:19:41.9417776Z aplikace = Dns shost = CLIENT1 požadavek ukázka dotazu requestMethod = = Axfr důvod = NoError outcome = Success msg = podezřelé DNS bylo zjištěno aktivitu pocházející z počítače CLIENT1 (což není DNS server). Dotaz byl pro ukázku dotazu (typ Axfr). Odpověď byla NoError. externalId = 2007 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c


### <a name="smb-session-enumeration"></a>Výčet relací SMB
02 – 21 – 2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.962930 + 00:00 CENTER CEF 6076 EnumerateSessionsSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | EnumerateSessionsSecurityAlert | Rekognoskace pomocí výčtu relací SMB | 5 | start = 2018-02-21T14:19:03.2071170Z app = SrvSvc shost = CLIENT1 msg = uživatele User1, z počítače CLIENT1 na DC1, vystavení Eugene Jenkins (uživatel2 počítač) se úspěšně provedly pokusy o výčet relací SMB . externalId = 2012 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440
### <a name="sam-r-enumeration"></a>Výčet SAM-R
02 – 21 – 2018 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | SamrReconnaissanceSecurityAlert | Rekognoskace pomocí výčtu adresářových služeb | 5 | start = 2018-02-21T14:19:41.9912772Z app = Samr shost = CLIENT1 suser = user1 outcome = Success msg = následující adresářové služby byla podniknuta výčty, které používají protokol SAMR, proti řadiči domény DC1 z CLIENT1:\r\nSuccessful výčet všech skupin v domain1.test.local uživatele User1. externalId = 2019 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="remote-execution"></a>Vzdálené spuštění
02 – 21 – 2018 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 CENTER CEF 6076 RemoteExecutionSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | RemoteExecutionSecurityAlert | Zjištěn pokus o vzdálené spuštění | 5 | start = 2018-02-21T14:19:41.9912772Z aplikace služby Wmi shost = = CLIENT1 suser = user1 outcome = Success msg = následující vzdálené spuštění došlo k pokusům na počítači DC1 z CLIENT1:\r\nSuccessful vzdálené spuštění služby WMI jeden nebo více metody uživatele User1. externalId = 2019 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="skeleton-key"></a>Skeleton Key
02 – 21 – 2018 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Aktivita související s oslabením šifrování | 5 | start = 2018-02-21T14:19:41.8737870Z aplikace = Kerberos msg = metodu šifrování pole ETYPE_INFO2 KRB_ERR byl downgradovat zpráv z počítače CLIENT1, na základě dřív zjištěné chování. To může být důsledek Skeleton Key na řadič domény DC1. externalId = 2011 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2

### <a name="unusual-protocol-implementation"></a>Neobvyklá implementace protokolu
02 – 21 – 2018 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050 + 00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | AbnormalProtocolSecurityAlert | Neobvyklá implementace protokolu | 5 | start = 2018-02-21T14:19:03.1981155Z aplikace = Ntlm shost = CLIENT2 outcome = Success msg = došlo k pokusům o ověření z počítače CLIENT2 proti řadiči domény DC1 pomocí neobvyklé implementace protokolu. Může se jednat o důsledek použití škodlivých nástrojů ke spuštění útoku, jako je například Pass-the-Hash nebo útok hrubou silou. externalId = 2002 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs1 =https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4

### <a name="malicious-service-creation"></a>Vytvoření škodlivé služby
02 – 21 – 2018 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.254930 + 00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | MaliciousServiceCreationSecurityAlert | Podezřelé vytvoření služby | 5 | start = 2018-02-21T14:19:41.7897808Z aplikace = ServiceInstalledEvent shost = CLIENT1 msg = user1 vytvořili MaliciousService mohl spustit potenciálně škodlivé příkazy na počítači CLIENT1. externalId = 2026 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c

### <a name="pass-the-ticket"></a>Pass-the-ticket
02 – 21 – 2018 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.22.4228.22540 | PassTheTicketSecurityAlert | Krádež identity pomocí útoku Pass-the-Ticket | 10 | start = 2018-02-21T15:02:22.2577465Z aplikace = Kerberos suser = msg Eugene Jenkins = Kerberos Eugene Jenkins (softwarový inženýr) pro lístky byly odcizeny z Admin-PC do Victim-PC a používá pro přístup k účtu krbtgt/Doména1. TEST. MÍSTNÍ. externalId = 2017 cs1Label = url cs1 =https://contoso-corp.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd

### <a name="suspicious-vpn-connection"></a>Připojení k síti VPN podezřelé
07-03-2018 13:13:12 Auth.Warning 192.168.0.200 1 2018-07-03T10:13:06.187834 + 00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï» ¿0 | Microsoft | Ochrana ATP v programu Azure | 2.39.0.0 | AbnormalVpnSecurityAlert | Podezřelé připojení VPN | 5 | start = 2018-06-30T15:34:05.3887333Z aplikace připojení VpnConnection suser = user1 msg = = uzivatel1 připojené k síti VPN pomocí počítače se 3 ze 3 míst.     externalId = 2025 cs1Label = url cs1 =https://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68


## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)