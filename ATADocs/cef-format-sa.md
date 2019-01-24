---
title: Referenční informace k protokolům pro ATA SIEM | Dokumentace Microsoftu
description: Obsahuje ukázky protokolů výstrah zabezpečení odeslaných ze služby ATA do vašeho systému SIEM.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 357f3517a864114c0aaa83a074c0b061d21259c2
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2019
ms.locfileid: "54840929"
---
# <a name="ata-siem-log-reference"></a>Referenční informace k protokolům pro ATA SIEM


*Platí pro: Advanced Threat Analytics verze 1.9*

ATA může předat zabezpečení a monitorování výstrahy události do vašeho systému SIEM. Ve formátu CEF se předávají výstrahy. Ukázka jednotlivých typů výstrah protokolu zabezpečení k odeslání do vašeho systému SIEM je níže.

## <a name="sample-ata-security-alerts-in-cef-format"></a>Ukázka ATA výstrah zabezpečení ve formátu CEF
Do systému SIEM se předávají následující pole a jejich hodnoty:

-   Začněte – čas spuštění výstrahy
-   suser – účet (obvykle uživatelský účet), součástí výstrahy
-   shost – zdrojový počítač výstrahy
-   výsledek – výstrahy s definovanou aktivity úspěch nebo neúspěch provést ve výstraze  
-   msg – popis výstrahy
-   CNT – výstrahy a počet, kolikrát (pro příklad útok hrubou silou má určité množství uhodnutí hesel) došlo k výstraze
-   aplikace – upozornění protokolu
-   externalId – zápisy události ID ATA do protokolu událostí, která odpovídá upozornění *
-   cs #label & cs # – řetězce zákazníků, které umožňuje CEF použít, cs #label je název nového pole a cs # je hodnota, například: cs1Label = url cs1 = https\://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

V tomto příkladu je cs1 pole s adresou URL výstrahy.

* Pokud vytváříte skripty nebo založené na protokolech služby automation, použijte jako názvy protokolů se mohou změnit bez předchozího upozornění trvalé externalID každý protokol místo použití názvu protokolu. 

|Upozornění názvy|ID oznámení událostí|
|---------|---------------|
|2001|Podezření na krádež identity na základě neobvyklého chování|
|2002|Neobvyklá implementace protokolu|
|2003|Rekognoskace pomocí výčtu účtů|
|2004|Útok hrubou silou pomocí jednoduché vazby LDAP.|
|2006|Škodlivá replikace adresářových služeb|
|2007|Rekognoskace pomocí DNS|
|2008|Aktivita snížení úrovně šifrování|
|2009|Aktivita snížení úrovně šifrování (potenciální zlatý lístek)|
|2010|Aktivita snížení úrovně šifrování (potenciální overpass-the-hash)|
|2011|Aktivita snížení úrovně šifrování (potenciální typu skeleton key)|
|2012|Rekognoskace pomocí výčtu relací SMB|
|2013|Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace|
|2014|Aktivita Honeytokenu|
|2016|Hromadné odstranění objektů|
|2017|Krádež identity pomocí útoku Pass-the-Hash|
|2018|Krádež identity pomocí útoku Pass-the-Ticket|
|2019|Zjištěn pokus o vzdálené spuštění|
|2020|Žádost o soukromé informace ochrany škodlivých dat|
|2021|Rekognoskace pomocí dotazů na adresářové služby|
|2022|Aktivita zlatého lístku Kerberos|
|2023|Podezřelé chyby ověřování|
|2024|Neobvyklá úprava citlivých skupin|
|2026|Podezřelé vytvoření služby|



## <a name="sample-logs"></a>Ukázky protokolů

Priority: 3 = nízká, 5 = střední, 10 = vysoká

### <a name="abnormal-modification-of-sensitive-groups"></a>Neobvyklá úprava citlivých skupin
1 2018-12-12T16:53:22.925757 + 00:00 CENTER ATA 4688 AbnormalSensitiveGroupMembership cef: 0 | Microsoft | ATA | 1.9.0.0 | AbnormalSensitiveGroupMembershipChangeSuspiciousActivity | Neobvyklá úprava citlivých skupin | 5 | start = 2018-12-12T18:52:58.0000000Z aplikace GroupMembershipChangeEvent suser = = krbtgt msg = krbtgt má neobvykle upravená citlivá členství ve skupinách. externalId=2024 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113d028ca1ec1250ca0491

### <a name="brute-force-attack-using-ldap-simple-bind"></a>Útok hrubou silou pomocí jednoduché vazby LDAP.
12. 12 2018 19:52:18 Auth.Warning 192.168.0.222 1 2018-12-12T17:52:18.899690 + 00:00 ATA 4688 LdapBruteForceSuspiciousActivity ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | LdapBruteForceSuspiciousActivity | Útok hrubou silou pomocí jednoduché vazby protokolu LDAP | 5 | start = 2018-12-12T17:52:10.2350665Z aplikace Ldap msg = = 10000 uhádnout heslo pokusy byly provedeny na 100 účtů z W2012R2-000000-Server. Byla úspěšně odhadla jedno heslo účtu. externalId=2004 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114acb8ca1ec1250cacdcb

### <a name="encryption-downgrade-activity-golden-ticket"></a>Aktivita snížení úrovně šifrování (Golden Ticket)
12. 12 2018 20:12:35 Auth.Warning 192.168.0.222 1 2018-12-12T18:12:35.105942 + 00:00 ATA 4688 EncryptionDowngradeSuspiciousAct ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | EncryptionDowngradeSuspiciousActivity | Aktivita související s oslabením šifrování | 5 | start = 2018-12-12T18:10:35.0334169Z aplikace = Kerberos msg = metodu šifrování pole TGT v TGS_REQ byla downgradovat zprávu od W2012R2 000000 serverem, na základě dřív zjištěné chování. To může být výsledkem Golden Ticket používané na W2012R2-000000-Server. externalId=2009 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114f938ca1ec1250cafcfa

### <a name="encryption-downgrade-activity-overpass-the-hash"></a>Aktivita snížení úrovně šifrování (overpass-the-hash)
12. 12 2018 19:00:31 Auth.Warning 192.168.0.222 1 2018-12-12T17:00:31.963485 + 00:00 ATA 4688 EncryptionDowngradeSuspiciousAct ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | EncryptionDowngradeSuspiciousActivity | Aktivita související s oslabením šifrování | 5 | start = 2018-12-12T17:00:31.2975188Z aplikace = Kerberos msg = metodu šifrování pole Encrypted_Timestamp v AS_REQ byla downgradovat zprávu od W2012R2 000000 serverem, na základě dřív zjištěné chování. To může být důsledek krádeže přihlašovacích údajů s pomocí Overpass-the-Hash z W2012R2-000000-Server. externalId=2010 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113eaf8ca1ec1250ca0883

###  <a name="encryption-downgrade-activity-skeleton-key"></a>Aktivita související s oslabením šifrování (Skeleton Key)
12. 12 2018 20:07:24 Auth.Warning 192.168.0.222 1 2018-12-12T18:07:24.065140 + 00:00 ATA 4688 EncryptionDowngradeSuspiciousAct ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | EncryptionDowngradeSuspiciousActivity | Aktivita související s oslabením šifrování | 5 | start = 2018-12-12T18:07:24.0222746Z aplikace = Kerberos msg = metodu šifrování pole ETYPE_INFO2 KRB_ERR byl downgradovat zprávu od W2012R2 000000 serverem, na základě dřív zjištěné chování. To může být důsledek Skeleton Key na řadič domény DC1. externalId=2011 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114e5c8ca1ec1250cafafe

### <a name="honeytoken-activity"></a>Aktivita Honeytokenu
12. 12 2018 19:51:52 Auth.Warning 192.168.0.222 1 2018-12-12T17:51:52.659618 + 00:00 ATA 4688 HoneytokenActivitySuspiciousActi ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | HoneytokenActivitySuspiciousActivity | Aktivita Honeytokenu | 5 | start = 2018-12-12T17:51:52.5855994Z aplikace pomocí protokolu Kerberos suser = USR78982 msg = = následující aktivity provedl USR78982 LAST78982:\r\nAuthenticated z počítače CLIENT1 pomocí protokolu NTLM, když přistupoval k domain1.test.local\cifs na počítači DC1. externalId=2014 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114ab88ca1ec1250ca7f76

### <a name="identity-theft-using-pass-the-hash-attack"></a>Krádež identity pomocí útoku Pass-the-Hash
12. 12 2018 19:56:02 Auth.Error 192.168.0.222 1 2018-12-12T17:56:02.047236 + 00:00 ATA 4688 PassTheHashSuspiciousActivity ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | PassTheHashSuspiciousActivity | Krádež identity pomocí útoku Pass-the-Hash | 10 | start = 2018-12-12T17:54:01.9582400Z aplikace Ntlm suser = USR46829 LAST46829 msg = = USR46829 LAST46829 hash byla ukradena z jednoho z počítačů dříve přihlašující USR46829 LAST46829 a použita z W2012R2 000000 serverem. externalId=2017 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114bb28ca1ec1250caf673

### <a name="identity-theft-using-pass-the-ticket-attack"></a>Krádež identity pomocí útoku Pass-the-Ticket
12. 12 2018 22:03:51 Auth.Error 192.168.0.222 1 2018-12-12T20:03:51.643633 + 00:00 ATA 4688 PassTheTicketSuspiciousActivity ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | PassTheTicketSuspiciousActivity | Krádež identity pomocí útoku Pass-the-Ticket | 10 | start = 2018-12-12T17:54:12.9960662Z aplikace Kerberos suser = Birdie jehněčí msg = = Kerberos Birdie jehněčí (softwarový inženýr) pro lístky byly odcizeny z W2012R2 000106 serverem W2012R2-000051-server a použít k přístup k domain1.test.local\host. externalId=2018 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b458ca1ec1250caf5b7

### <a name="kerberos-golden-ticket-activity"></a>Aktivita zlatého lístku Kerberos
12. 12 2018 19:53:26 Auth.Error 192.168.0.222 1 2018-12-12T17:53:26.869091 + 00:00 ATA 4688 GoldenTicketSuspiciousActivity ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | GoldenTicketSuspiciousActivity | Aktivita zlatého lístku Kerberos | 10 | start = 2018-12-13T06:51:26.7290524Z aplikace Kerberos suser = Sonja Chadsey msg = = podezřelé využití lístku Kerberos Sonja Chadsey (softwarový inženýr) společnosti, která potenciální útok metodou Golden Ticket, byla zjištěna. externalId=2022 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b168ca1ec1250caf556

### <a name="malicious-data-protection-private-information-request"></a>Žádost o soukromé informace ochrany škodlivých dat
12. 12 2018 20:03:49 Auth.Error 192.168.0.222 1 2018-12-12T18:03:49.814620 + 00:00 ATA 4688 RetrieveDataProtectionBackupKeyS ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | RetrieveDataProtectionBackupKeySuspiciousActivity | Žádost o soukromé informace ochrany škodlivých dat | 10 | start = 2018-12-12T17:58:56.3537533Z app = LsaRpc shost W2012R2 000000 serverem msg = = Neznámý uživatel provedl 1 úspěšný pokus o z W2012R2-000000-Server pokusil načíst záložní klíč domény DPAPI z řadiče domény DC1. externalId=2020 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114d858ca1ec1250caf983

### <a name="malicious-replication-of-directory-services"></a>Škodlivá replikace adresářových služeb
12. 12 2018 19:56:49 Auth.Error 192.168.0.222 1 2018-12-12T17:56:49.312648 + 00:00 ATA 4688 DirectoryServicesReplicationSusp ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | DirectoryServicesReplicationSuspiciousActivity | Škodlivá replikace adresářových služeb | 10 | start = 2018-12-12T17:52:34.3287329Z aplikace Drsr shost = W2012R2 000000 serverem msg = = škodlivou replikaci z 000000 serverem W2012R2 proti řadiči domény DC1 se úspěšně odeslaly požadavky. výsledek = úspěch externalId = 2006 cs1Label = url cs1 = https\://192.168.0.220/suspiciousActivity/5c114be18ca1ec1250caf6b8

### <a name="privilege-escalation-using-forged-authorization-data"></a>Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace
12. 12 2018 19:51:15 Auth.Error 192.168.0.222 1 2018-12-12T17:51:15.658608 + 00:00 ATA 4688 ForgedPacSuspiciousActivity ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | ForgedPacSuspiciousActivity | Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace | 10 | start = 2018-12-12T17:51:15.0261128Z aplikace pomocí protokolu Kerberos suser = triservice msg = = triservice pokusil zvýšit oprávnění proti řadiči domény DC1 z W2012R2 000000 serverem pomocí falešných dat autorizace. externalId=2013 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a938ca1ec1250ca7f48

### <a name="reconnaissance-using-directory-services-queries"></a>Rekognoskace pomocí dotazů na adresářové služby
12. 12 2018 20:23:52 Auth.Warning 192.168.0.222 1 2018-12-12T18:23:52.155531 + 00:00 ATA 4688 SamrReconnaissanceSuspiciousActi ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | SamrReconnaissanceSuspiciousActivity | Rekognoskace pomocí dotazů na adresářové služby | 5 | start = 2018-12-12T18:04:12.9868815Z app = Samr shost W2012R2 000000 serverem msg = = následující adresářové služby byla podniknuta dotazy, které používají protokol SAMR, proti řadiči domény DC1 z W2012R2 – 000000 – Server: \r\ dotaz nSuccessful tvůrci příchozí vztah důvěryhodnosti doménové struktury (členové této skupiny můžete vytvořit příchozí jednosměrné vztahy důvěryhodnosti na těchto doménových strukturách) v domain1.test.local externalId = 2021 cs1Label = url cs1 = https\://192.168.0.220/suspiciousActivity/ 5c114e758ca1ec1250cafb2e

### <a name="reconnaissance-using-account-enumeration"></a>Rekognoskace pomocí výčtu účtů
1 2018-12-12T16:57:09.661680 + 00:00 CENTER ATA 4688 AccountEnumerationSuspiciousActi cef: 0 | Microsoft | ATA | 1.9.0.0 | AccountEnumerationSuspiciousActivity | Rekognoskace pomocí výčtu účtů | 5 | start = 2018-12-12T16:57:09.1706828Z app = Kerberos shost W2012R2 000000 serverem msg = = podezřelé přihlašovací aktivity výčet pomocí protokolu Kerberos, která pochází z W2012R2 000000 serverem, byla zjištěna. Útočník provedl celkem tento počet pokusů uhádnout 100 pro názvy účtů, 1 počet pokusů o uhádnutí odpovídající existujícími názvy účtů ve službě Active Directory. externalId=2003 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113de58ca1ec1250ca06d8

### <a name="reconnaissance-using-dns"></a>Rekognoskace pomocí DNS
1 2018-12-12T16:57:20.743634 + 00:00 CENTER ATA 4688 DnsReconnaissanceSuspiciousActiv cef: 0 | Microsoft | ATA | 1.9.0.0 | DnsReconnaissanceSuspiciousActivity | Rekognoskace pomocí DNS | 5 | start = 2018-12-12T16:57:20.2556472Z app = Dns shost W2012R2 000000 serverem msg = = podezřelé DNS aktivity původcem, W2012R2-000000-Server (což není DNS server) proti řadiči domény DC1. externalId=2007 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113df08ca1ec1250ca074c

### <a name="reconnaissance-using-smb-session-enumeration"></a>Rekognoskace pomocí výčtu relací SMB
12. 12 2018 19:50:51 Auth.Warning 192.168.0.222 1 2018-12-12T17:50:51.090247 + 00:00 ATA 4688 EnumerateSessionsSuspiciousActiv ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | EnumerateSessionsSuspiciousActivity | Rekognoskace pomocí výčtu relací SMB | 5 | start = 2018-12-12T17:00:42.7234229Z app = SrvSvc shost W2012R2 000000 serverem msg = = SMB pokusy o výčet relací z 000000 serverem W2012R2 proti řadiči domény DC1 se nezdařil. Žádné účty byly vystaveny. externalId=2012 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114a788ca1ec1250ca7735

### <a name="remote-execution-attempt-detected"></a>Zjištěn pokus o vzdálené spuštění
12. 12 2018 19:58:45 Auth.Warning 192.168.0.222 1 2018-12-12T17:58:45.082799 + 00:00 ATA 4688 RemoteExecutionSuspiciousActivit ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | RemoteExecutionSuspiciousActivity | Zjištěn pokus o vzdálené spuštění | 5 | start = 2018-12-12T17:54:23.9523766Z shost W2012R2 000000 serverem msg = = následující vzdálené spuštění na řadiči domény DC1 z W2012R2 došlo k pokusům – 000000 – Server: \r\nFailed vzdálené plánování jeden nebo více úloh. externalId=2019 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114c548ca1ec1250caf783

### <a name="unusual-protocol-implementation"></a>Neobvyklá implementace protokolu
1 2018-12-12T16:50:46.930234 + 00:00 CENTER ATA 4688 AbnormalProtocolSuspiciousActivi cef: 0 | Microsoft | ATA | 1.9.0.0 | AbnormalProtocolSuspiciousActivity | Neobvyklá implementace protokolu | 5 | start = 2018-12-12T16:48:46.6480337Z app = Ntlm shost = outcome W2012R2 000000 serverem = Success msg = triservice se úspěšně ověřil u W2012R2-000000-Server proti řadiči domény DC1 pomocí neobvyklý protokol implementace. Může se jednat o důsledek použití škodlivých nástrojů ke spuštění útoku, jako je například Pass-the-Hash nebo útok hrubou silou. externalId=2002 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c668ca1ec1250ca0397

### <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Podezření na krádež identity na základě neobvyklého chování
1 2018-12-12T16:50:35.746877 + 00:00 CENTER ATA 4688 AbnormalBehaviorSuspiciousActivi cef: 0 | Microsoft | ATA | 1.9.0.0 | AbnormalBehaviorSuspiciousActivity | Podezření na krádež identity na základě neobvyklého chování | 5 | start = 2018-12-12T16:48:35.5501183Z aplikace Kerberos suser = USR45964 msg = = USR45964 LAST45964 monitorujícím neobvyklého chování při provádění aktivity, které nebyly viděli za poslední měsíc a jsou také v souladu s aktivitami ostatních účtů v organizaci. Neobvyklé chování je založeno na následující aktivity: \r\nPerformed interaktivní přihlášení z 30 workstations.\r\nRequested neobvyklý přístup k 30 neobvyklé prostředky. externalId=2001 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113c5b8ca1ec1250ca0355

### <a name="suspicious-authentication-failures"></a>Podezřelé chyby ověřování
12. 12 2018 19:50:34 Auth.Warning 192.168.0.222 1 2018-12-12T17:04:25.214067 + 00:00 ATA 4688 BruteForceSuspiciousActivity ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | BruteForceSuspiciousActivity | Podezřelá neúspěšná ověření | 5 | start = 2018-12-12T17:03:58.5892462Z app = Kerberos shost W2012R2 000106 serverem msg = = podezřelá neúspěšná ověření indikující možný útok hrubou silou byly zjištěny z W2012R2-000106-Server. externalId=2023 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c113f988ca1ec1250ca5810

### <a name="suspicious-service-creation"></a>Podezřelé vytvoření služby
12. 12 2018 19:53:49 Auth.Warning 192.168.0.222 1 2018-12-12T17:53:49.913034 + 00:00 ATA 4688 MaliciousServiceCreationSuspicio ‹¯¨CEF:0 CENTER | Microsoft | ATA | 1.9.0.0 | MaliciousServiceCreationSuspiciousActivity | Podezřelé vytvoření služby | 5 | start = 2018-12-12T19:53:49.0000000Z aplikace ServiceInstalledEvent shost = W2012R2 000000 serverem msg = = triservice vytvořili FakeService mohl spustit potenciálně škodlivé příkazy na W2012R2-000000-Server. externalId=2026 cs1Label=url cs1=https\://192.168.0.220/suspiciousActivity/5c114b2d8ca1ec1250caf577

## <a name="monitoring-alerts"></a>Monitorování výstrah

### <a name="gatewaydisconnectedmonitoringalert"></a>GatewayDisconnectedMonitoringAlert
1 2018-12-12T16:52:41.520759 + 00:00 CENTER ATA 4688 GatewayDisconnectedMonitoringAle cef: 0 | Microsoft | ATA | 1.9.0.0 | GatewayDisconnectedMonitoringAlert | GatewayDisconnectedMonitoringAlert | 5 | externalId = 1011 cs1Label = url cs1 = https\://192.168.0.220/monitoring msg = nebyl komunikaci ze brána CENTER po dobu 5 minut. Poslední komunikaci došlo v 12/12/2018 16:47:03: 00 UTC.

### <a name="gatewaystartfailuremonitoringalert"></a>GatewayStartFailureMonitoringAlert
1 2018-12-12T15:36:59.701097 + 00:00 CENTER ATA 1372 GatewayStartFailureMonitoringAle cef: 0 | Microsoft | ATA | 1.9.0.0 | GatewayStartFailureMonitoringAlert | GatewayStartFailureMonitoringAlert | 5 | externalId = 1018 cs1Label = url cs1 = https\://192.168.0.220/monitoring msg = The Gateway službu na počítači DC1 se nepodařilo spustit. Jeho poslední spuštění se zjistilo 12/12/2018 15:04:12: 00 UTC.

> [!NOTE]
> Všechna monitorování výstrahy chodit nebudou pomocí stejné šablony, jak je uvedeno výše.


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
