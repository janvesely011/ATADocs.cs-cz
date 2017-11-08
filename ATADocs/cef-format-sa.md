---
title: "Referenční informace k protokolům pro ATA SIEM | Dokumentace Microsoftu"
description: "Obsahuje ukázky protokolů podezřelých aktivit odeslaných ze služby ATA do vašeho systému SIEM."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: d9e226f06c407cb16a3486f81658e05433b00fb1
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*


# <a name="ata-siem-log-reference"></a>Referenční informace k protokolům pro ATA SIEM

ATA může předat do vašeho systému SIEM informace o podezřelých aktivitách a událostech výstrah monitorování. Události podezřelých aktivit jsou ve formátu CEF. Tento referenční článek obsahuje ukázky protokolů podezřelých aktivit odesílaných do vašeho systému SIEM.

## <a name="sample-ata-suspicious-activities-in-cef-format"></a>Ukázky podezřelých aktivit ATA ve formátu CEF
Do systému SIEM se předávají následující pole a jejich hodnoty:

-   start – počáteční čas výstrahy
-   suser – účet (obvykle by to měl být uživatelský účet), kterého se tato výstraha týká
-   shost – zdrojový počítač pro tuto výstrahu
-   outcome – pro výstrahy s informacemi, jestli se jedná o úspěch nebo selhání aktivity v dané výstraze  
-   msg – popis výstrahy
-   CNT – pro výstrahy, které mají a počet pokusů, které výstrahy se stalo (například hrubou silou s částkou odhadované hesel)
-   app – protokol použitý ve výstraze
-   externalId – zápisy události ID ATA do protokolu událostí, který odpovídá této výstraze
-   cs#label & cs# – jedná se o řetězce zákazníků, které umožňuje CEF použít, cs#label je název nového pole a cs# je hodnota, například: cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

V tomto příkladu je cs1 pole s adresou URL výstrahy.

## <a name="sample-logs"></a>Ukázky protokolů

Priority: 3 = nízká, 5 = střední, 10 = vysoká

### <a name="bruteforce--ldap"></a>BruteForce – LDAP
05-03-2017          13:35:01               Auth.Warning    192.168.0.220     3. května 10:35:01 CENTER ATA:CEF:0|Microsoft|ATA|.5942.64854|BruteForceSuspiciousActivity|Útok hrubou silou za použití jednoduché vazby protokolu LDAP|5|start=2017-05-03T10:34:57.2785534Z app=Ldap suser=Darris Woods shost=CLIENT1 msg=Byl proveden útok hrubou silou na uživatele Darris Woods (softwarový inženýr) pomocí protokolu LDAP z počítače CLIENT1 (76 pokusů o uhodnutí hesla). cnt=76 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     3. května 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Útok hrubou silou za použití jednoduché vazby protokolu LDAP|5|start=2017-05-03T10:34:58.7004159Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=Byl proveden útok hrubou silou na uživatele Dino Hopkins (softwarový inženýr) pomocí protokolu LDAP z počítače CLIENT1 (3 pokusy o uhodnutí hesla). cnt=3 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     3. května 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Útok hrubou silou za použití jednoduché vazby protokolu LDAP|5|start=2017-05-03T10:34:59.7269332Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=Byl úspěšně proveden útok hrubou silou na uživatele Dino Hopkins (softwarový inženýr) pomocí protokolu LDAP z počítače CLIENT1 (77 pokusů o uhodnutí hesla). cnt=77 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70
### <a name="bruteforce"></a>BruteForce
05-14-2017          13:27:05               Auth.Warning    192.168.0.220     1 2017-05- ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|BruteForceSuspiciousActivity|Nezdařené podezřelé pokusy o ověření|5|start=2017-05-14T10:27:04.3904739Z app=Kerberos shost=CLIENT1 msg=Byly zjištěny podezřelé nezdařené pokusy o ověření ukazující na možný útok hrubou silou z počítače CLIENT1. externalId=2023 cs1Label=url cs1=https://center/suspiciousActivity/591830f98ca1ec11d0c0d7f5
### <a name="privilege-escalation"></a>Zvýšení oprávnění
#### <a name="silver"></a>Silver (Stříbrná)
05-10-2017          17:14:15               Auth.Error           192.168.0.220     1 2017-05-10T14:14:15.589415+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Zvýšení oprávnění s pomocí falešných autorizačních dat|10|start=2017-05-10T14:11:51.8053059Z app=Kerberos suser=user1 msg=Uživatel user1 se pokusil zvýšit oprávnění k počítači HOST/client1 z počítače CLIENT2 s pomocí falešných autorizačních dat. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/591320378ca1ec02543e4747
#### <a name="gold"></a>Zlatá
05-10-2017          17:13:30               Auth.Error           192.168.0.220     1 2017-05-10T14:13:30.244377+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Zvýšení oprávnění s pomocí falešných autorizačních dat|10|start=2017-05-10T14:11:27.6455273Z app=Kerberos suser=user1 msg=Uživatel user1 se pokusil zvýšit oprávnění k počítači DC4 z počítače CLIENT1 s pomocí falešných autorizačních dat. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/5913200a8ca1ec02543e3ea8
### <a name="golden-ticket"></a>Zlatý lístek
05-14-2017          15:57:10               Auth.Warning    192.168.0.220     1 2017-05-14T12:57:10.392730+00:00 CENTER ATA 4732 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Aktivita downgradu šifrování|5|start=2017-05-14T12:55:08.6913033Z app=Kerberos msg=Metoda šifrování pole TGT ve zprávě TGS_REQ z počítače CLIENT1 byla downgradována na základě dříve naučeného chování. Může to být výsledek použití lístku Golden Ticket (Zlatý lístek) na počítači CLIENT1. externalId=2009 cs1Label=url cs1=https://center/suspiciousActivity/591854268ca1ec127ceec396
### <a name="honey-token-activity"></a>Aktivita Honey Token
05-11-2017          16:49:10               Auth.Warning    192.168.0.220     1 2017-05-11T13:49:10.725605+00:00 CENTER ATA 876 HoneytokenActivitySuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|HoneytokenActivitySuspiciousActivity|Honeytoken activity|5|start=2017-05-11T13:49:09.6455794Z app=Kerberos suser=privtriservice msg=Služba privtriservice provedla tyto aktivity:\r\nOvěření z DC1 s použitím NTLM na základě podnikových prostředků přes DC1. externalId=2014 cs1Label=url cs1=https://center/suspiciousActivity/59146bd68ca1ec036ce57d29
### <a name="suspicious-replication-of-directory-services"></a>Podezřelá replikace adresářových služeb
3. května 11:02:28 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DirectoryServicesReplicationSuspiciousActivity|Škodlivá replikace adresářových služeb|10|start=2017-05-03T11:00:13.6560919Z suser=user1 shost=CLIENT1 outcome=Failure msg=Uživatel user1 se pokusil provést žádosti o škodlivou replikaci z počítače CLIENT1 proti DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b8c48ca1ec04d05ed28d
### <a name="malicious-data-protection-private-information-request"></a>Škodlivý požadavek na soukromé informace přes Data Protection
3. května 13:39:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RetrieveDataProtectionBackupKeySuspiciousActivity|Škodlivá žádost týkající se ochrany dat a soukromých informací|10|start=2017-05-03T13:37:06.4039886Z app=LsaRpc shost=CLIENT1 suser= outcome=Success msg=Neznámý uživatel provedl z počítače CLIENT1 4 úspěšné pokusy o načtení záložního klíče domény DPAPI z DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dd868ca1ec04d05fb01d
### <a name="massive-object-deletion"></a>Hromadné odstranění objektů
05-14-2017          14:38:34               Auth.Warning    192.168.0.220     1 2017-05-14T11:38:34.898810+00:00 CENTER ATA 3748 MassiveObjectDeletionSuspiciousA ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|MassiveObjectDeletionSuspiciousActivity|Hromadné odstranění objektů|5|start=2017-05-14T11:33:32.0000000Z msg=496 objektů (9,75 % z celkového počtu objektů AD) bylo odstraněno během neurčené doby z domény domain1.test.local. cnt=496 externalId=2016 cs1Label=url cs1=https://center/suspiciousActivity/591841ba8ca1ec0ea4ad587a
### <a name="over-pass-the-hash"></a>Over-pass-the-hash
05-14-2017          12:07:46               Auth.Warning    192.168.0.220     1 2017-05-14T09:07:46.652319+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Aktivita downgradu šifrování|5|start=2017-05-14T09:07:44.9933773Z app=Kerberos msg=Metoda šifrování pole Encrypted_Timestamp ve zprávě AS_REQ z počítače CLIENT1 byla downgradována na základě dříve naučeného chování. Může to být důsledek krádeže přihlašovacích údajů s pomocí Overpass-the-Hash z počítače CLIENT1. externalId=2010 cs1Label=url cs1=https://center/suspiciousActivity/59181e628ca1ec045cdfa929
### <a name="pass-the-hash"></a>Pass-the-hash
05-10-2017          17:48:51               Auth.Error           192.168.0.220     1 2017-05-10T14:48:51.998620+00:00 CENTER ATA 596 PassTheHashSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|PassTheHashSuspiciousActivity|Krádež identity pomocí útoku Pass-the-Hash|10|start=2017-05-10T14:46:50.9463800Z app=Ntlm suser=user2 msg=Byla odcizena hodnota hash uživatele user2 z jednoho z počítačů, na který se dříve přihlásil uživatel user2, a tato hodnota byla použita z počítače CLIENT1. externalId=2017 cs1Label=url cs1=https://center/suspiciousActivity/591328538ca1ec02543f9a1a
### <a name="account-enumeration"></a>Výčet účtů
05-10-2017          16:44:22               Auth.Warning    192.168.0.220     1 2017-05-10T13:44:22.706381+00:00 CENTER ATA 596 AccountEnumerationSuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|AccountEnumerationSuspiciousActivity|Rekognoskace s použitím výčtu účtů|5|start=2017-05-10T13:44:20.9930644Z app=Kerberos shost=CLIENT3 msg=Byla zjištěna podezřelá aktivita výčtu účtů s použitím protokolu Kerberos z počítače CLIENT3. Útočník provedl celkem 72 pokusů o uhodnutí hesla pro názvy účtů, u 2 pokusů o uhodnutí hesla existuje ve službě Active Directory shoda s existujícími názvy účtů. externalId=2003 cs1Label=url cs1=https://center/suspiciousActivity/591319368ca1ec02543c56ee
### <a name="dns-recon"></a>Rekognoskace DNS
05-03-2017          13:16:57               Auth.Warning    192.168.0.220     3. května 10:16:57 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Rekognoskace s použitím DNS|5|start=2017-05-03T10:16:41.8297467Z app=Dns shost=CLIENT1 msg=Byla pozorována podezřelá aktivita DNS z počítače CLIENT1 (což není server DNS) na DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa 05-03-2017          13:24:21               Auth.Warning    192.168.0.220     3. května 10:24:21 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Rekognoskace s pomocí DNS|5|start=2017-05-03T10:24:08.0950753Z app=Dns shost=CLIENT1 request=contoso.com requestMethod=Axfr reason=NameError outcome=Failure msg=Byla pozorována podezřelá aktivita DNS z počítače CLIENT1 (což není server DNS). Dotaz byl pro doménu contoso.com (typ Axfr). Odpověď byla NameError. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
### <a name="smb-session-enumeration"></a>Výčet relací SMB
3. května 11:55:43 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|EnumerateSessionsSuspiciousActivity|Rekognoskace s pomocí výčtu relací SMB|5|start=2017-05-03T11:52:02.4360718Z app=SrvSvc shost=CLIENT1 msg=Úspěšně byly provedeny pokusy o výčet relací SMB z počítače CLIENT1 na DC1 se zveřejněním uživatele user1 (daf::1). cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c53f8ca1ec04d05f1cf1
### <a name="samr-enumeration"></a>Výčet SAMR
3. května 11:44:48 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|SamrReconnaissanceSuspiciousActivity|Rekognoskace s použitím výčtu adresářových služeb|5|start=2017-05-03T11:42:46.5911225Z app=Samr shost=CLIENT1 suser=user1 outcome=Success msg=Byly provedeny následující pokusy o vytvoření výčtů adresářových služeb s použitím protokolu SAMR u DC1 z počítače CLIENT1:\r\nÚspěšný výčet všech skupin v: domain1.test.local provedený uživatelem user1 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c2b08ca1ec04d05f0e19
### <a name="remote-execution"></a>Vzdálené spuštění
3. května 12:36:47 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RemoteExecutionSuspiciousActivity|Zjištěn pokus o vzdálené spuštění|3|start=2017-05-03T12:34:32.3714348Z app=ServiceControl shost=CLIENT1 suser=Administrator outcome=Success msg=Na DC1 byly z počítače CLIENT1 provedeny následující pokusy o vzdálené spuštění:\r\nÚspěšné vytvoření PSEXESVC správcem na dálku. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cedf8ca1ec04d05f5692
### <a name="skeleton-key"></a>Skeleton Key
05-14-2017          12:13:12               Auth.Warning    192.168.0.220     1 2017-05-14T09:13:12.102468+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Aktivita downgradu šifrování|5|start=2017-05-14T09:13:03.3509467Z app=Kerberos msg=Metoda šifrování pole ETYPE_INFO2 ve zprávě KRB_ERR z počítače CLIENT2 byla downgradována na základě dříve naučeného chování. Může to být důsledek Skeleton Key na DC3. externalId=2011 cs1Label=url cs1=https://center/suspiciousActivity/59181fa88ca1ec045cdfe630
### <a name="unusual-protocol-implementation"></a>Neobvyklá implementace protokolu
3. května 12:28:19 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|AbnormalProtocolSuspiciousActivity|Neobvyklá implementace protokolu|5|start=2017-05-03T12:28:05.3561302Z app=Ntlm shost=CLIENT1 suser=Administrator outcome=Success msg=Správce se úspěšně ověřil z počítače CLIENT1 na DC1 s použitím neobvyklé implementace protokolu. Může se jednat o důsledek použití škodlivých nástrojů ke spuštění útoku, jako je například Pass-the-Hash nebo útok hrubou silou. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4
### <a name="sensitive-account-credentials-exposed"></a>Zveřejnění důvěrných přihlašovacích údajů k účtu
3. května 13:23:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|Byly zveřejněny důvěrné přihlašovací údaje k účtu|3|start=2017-05-03T13:23:09.7798589Z app=Ldap shost=CLIENT1 suser=Administrator msg=Byly zveřejněny přihlašovací údaje správce v nešifrovaném textu s pomocí jednoduché vazby protokolu LDAP z počítače CLIENT1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909d9c68ca1ec04d05f9918
### <a name="services-exposing-account-credentials"></a>Služby zveřejňující přihlašovací údaje k účtu
3. května 13:34:23 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|Služby zveřejňující přihlašovací údaje k účtu|3|start=2017-05-03T13:28:36.5159194Z app=Ldap shost=daf::220 msg=Služby spuštěné na: daf::220 (daf::220) zveřejňují přihlašovací údaje k účtu v nešifrovaném textu s pomocí jednoduché vazby protokolu LDAP. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dc5f8ca1ec04d05fa8b1
### <a name="pass-the-ticket"></a>Pass-the-ticket
4. května 13:15:41 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|PassTheTicketSuspiciousActivity|Krádež identity pomocí útoku Pass-the-Ticket|10|start=2017-05-04T13:13:44.5160000Z app=Kerberos shost=CLIENT1 suser=Administrator request=krbtgt/DOMAIN1.TEST.LOCAL msg=Byly odcizeny lístky Kerberos správce z počítače CLIENT2 do počítače CLIENT1 a byly použity k přístupu do: krbtgt/DOMAIN1.TEST.LOCAL. cs2Label=ticketSourceComputer cs2=CLIENT2 cs3Label=ticketSourceComputerIpAddress cs3= cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/590b29168ca1ec0ba438acf6

## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
