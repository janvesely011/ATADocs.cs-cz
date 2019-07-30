---
title: Azure Průvodce výstrah zabezpečení ochrany ATP v programu | Dokumentace Microsoftu
d|Description: This article provides a list of the security alerts issued by Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/25/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2ac458831e47db99c0b61d56cd390c5d01ed8ca1
ms.sourcegitcommit: dd8c94db68e85752c20bba3446b678cd1edcd932
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/29/2019
ms.locfileid: "68604348"
---
# <a name="azure-atp-security-alerts"></a>Výstrahy zabezpečení Azure ATP

Výstrahy zabezpečení Azure ATP vysvětlují podezřelé aktivity zjištěné senzory ATP Azure ve vaší síti a aktérů a počítačích zapojenými do každé hrozby. Seznamy legitimace výstrah obsahují přímé odkazy na zúčastněné uživatele a počítače, aby bylo možné vaše vyšetřování snadno a rychle zvýšit.

Výstrahy zabezpečení Azure ATP jsou rozdělené do následujících kategorií nebo fází, jako jsou například fáze zobrazené v typickém dezaktivačním řetězu internetového útoku. Přečtěte si další informace o jednotlivých fázích, upozorněních určených k detekci jednotlivých útoků a o tom, jak používat výstrahy k ochraně sítě pomocí následujících odkazů:

  1. [Výstrahy fáze rekognoskace](atp-reconnaissance-alerts.md)
  2. [Výstrahy fáze zneužití přihlašovacích údajů](atp-compromised-credentials-alerts.md)
  3. [Výstrahy fáze pohybu na okraji](atp-lateral-movement-alerts.md)
  4. [Výstrahy fáze dominantního postavení domény](atp-domain-dominance-alerts.md)
  5. [Výstrahy fáze exfiltrace](atp-exfiltration-alerts.md)

Další informace o struktuře a běžných součástech všech výstrah zabezpečení Azure ATP najdete v tématu [Principy výstrah zabezpečení](understanding-security-alerts.md).

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>Mapování názvu výstrahy zabezpečení a jedinečných externích ID

Ve verzi 2.56 všechny existující výstrahy zabezpečení služby Azure ATP byly přejmenovány s snáze pochopit názvy. Mapování mezi staré i nové názvy a jejich odpovídající jedinečný externalIds jsou uvedené v následující tabulce. Při použití se skripty nebo automatizací doporučuje společnost Microsoft používat místo názvů výstrah externí ID výstrah, protože pouze externí ID výstrahy zabezpečení jsou trvalá a nemusejí se měnit.

> [!div class="mx-tableFixed"] 

|Nový název výstrahy zabezpečení|Předchozí název výstrahy zabezpečení|Jedinečné externí ID|severity|MITRE ATT&CK Matrix™ |
|---------|----------|---------|---------|---------|
|[Rekognoskace výčtu účtů](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|Rekognoskace pomocí výčtu účtů|2003|Střední|Zjišťování|
|[Data exfiltrace přes SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)| Není k dispozici| 2030|Vysoká|Exfiltrace<br>Boční pohyb,<br>Příkaz a ovládací prvek|
|[Aktivita honeytokenu](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|Aktivita Honeytokenu|2014|Střední|Přístup k přihlašovacím údajům<br> Zjišťování|
|[Škodlivá žádost o Data Protection API hlavní klíč](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|Škodlivá žádost o soukromé informace přes Data Protection|2020|Vysoká|Přístup k přihlašovacím údajům|
|[Mapování sítě rekognoskace (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|Rekognoskace pomocí DNS|2007|Střední|Zjišťování|
|[Pokus o vzdálené spuštění kódu](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|Pokus o spuštění vzdáleného kódu|2019|Střední|Realizaci<br> Dočasné<br> Eskalace oprávnění,<br> Obrany proti úniku,<br> Laterální pohyb|
|[Vzdálené spuštění kódu přes DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|Není k dispozici|2036|Střední|Eskalace oprávnění,<br> Laterální pohyb|
|[Objekt zabezpečení rekognoskace (LDAP)](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)|Není k dispozici|2038|Střední|Přístup k přihlašovacím údajům|
|[Podezření na útok hrubou silou (Kerberos, NTLM)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|Podezřelé chyby ověřování|2023|Střední|Přístup k přihlašovacím údajům|
|[Podezřelý útok hrubou silou (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|Útok hrubou silou pomocí jednoduché vazby LDAP.|2004|Střední|Přístup k přihlašovacím údajům|
|[Podezřelý útok hrubou silou (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|Neobvyklá implementace protokolu (potenciální použití škodlivých nástrojů, jako je Hydra)|2033|Střední|Laterální pohyb|
|[Podezřelý útok DCShadow (povýšení řadiče domény)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|Povýšení řadiče domény podezřelé (možný útok DCShadow)|2028|Vysoká|Podaňová povinnost ochrany|
|[Podezřelý útok DCShadow (požadavek na replikaci řadiče domény)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|Žádost o replikaci řadiče domény podezřelé (možný útok DCShadow)|2029|Vysoká|Podaňová povinnost ochrany|
|[Podezřelý útok DCSync (replikace adresářových služeb)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|Škodlivá replikace adresářových služeb|2006|Vysoká|Dočasné<br> Přístup k přihlašovacím údajům|
|[Podezřelé použití zlatého lístku (downgrade šifrování)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|Aktivita snížení úrovně šifrování (potenciální útok metodou golden ticket)|2009|Střední|Eskalace oprávnění,<br> Boční pohyb,<br>Dočasné|
|[Podezřelé použití zlatého lístku (data s falešným oprávněním)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace|2013|Vysoká|Eskalace oprávnění,<br>Boční pohyb,<br>Dočasné|
|[Podezřelé používání lístku (neexistující účet)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|Protokol Kerberos Golden Ticket - neexistující účet|2027|Vysoká|Eskalace oprávnění,<br> Boční pohyb,<br>Dočasné|
|[Podezřelé použití zlatého lístku (anomálie lístků)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|Není k dispozici|2032|Vysoká|Eskalace oprávnění,<br> Boční pohyb,<br>Dočasné|
|[Podezřelé použití zlatého lístku (časová anomálie)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|Protokol Kerberos – anomálie času lístku|2022|Vysoká|Eskalace oprávnění,<br> Boční pohyb,<br>Dočasné|
|[Podezření na krádež identity (pass-the-hash)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|Krádež identity pomocí útoku Pass-the-Hash|2017|Vysoká|Laterální pohyb|
|[Podezření na krádež identity (pass-the-Ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|Krádež identity pomocí útoku Pass-the-Ticket|2018|Vysoká nebo střední|Laterální pohyb|
|[Podezření na manipulaci s ověřováním NTLM – Preview](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039---preview)|Není k dispozici|2039|Střední|Eskalace oprávnění, <br>Laterální pohyb|
|[Podezřelý útok na Relay protokolu NTLM](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)|Není k dispozici|2037|Střední nebo nízká, je-li zjištěno pomocí podepsaného protokolu NTLM v2|Eskalace oprávnění, <br> Laterální pohyb|
|[Podezření na útok přes pass-the-hash (downgrade šifrování)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|Aktivita snížení úrovně šifrování (možný útok overpass-the-hash)|2008|Střední|Laterální pohyb|
|[Podezřelá Overpass-the-hash – útok (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|Neobvyklá implementace protokolu Kerberos (možný útok overpass-the-hash)|2002|Střední|Laterální pohyb|
|[Podezřelý útok z podklíče šifrování (downgrade)](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|Aktivita snížení úrovně šifrování (potenciální útoku typu skeleton key)|2010|Střední|Boční pohyb,<br> Dočasné|
|[Podezření na použití rozhraní Metasploit pro hackery](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|Neobvyklá implementace protokolu (potenciální použijte Metasploit hacking nástroje)|2034|Střední|Laterální pohyb|
|[Podezřelý útok WannaCry ransomwarem](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|Neobvyklá implementace protokolu (možný útok ransomwarem WannaCry)|2035|Střední|Laterální pohyb|
|[Podezřelá komunikace přes DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|Podezřelá komunikace prostřednictvím DNS|2031|Střední|Exfiltrace|
|[Podezřelé přídavky citlivých skupin](atp-domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)|Podezřelé přídavky citlivých skupin|2024|Střední|Přístup k přihlašovacím údajům<br>Dočasné|
|[Podezřelé vytvoření služby](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|Podezřelé vytvoření služby|2026|Střední|Realizaci<br> Dočasné<br> Eskalace oprávnění,<br> Obrany proti úniku,<br>Laterální pohyb|
|[Podezřelé připojení VPN](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|Podezřelé připojení k síti VPN|2025|Střední|Dočasné<br>Podaňová povinnost ochrany|
|[Rekognoskace členství uživatelů a skupin (SAMR)](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|Rekognoskace pomocí dotazů na adresářové služby|2021|Střední|Zjišťování|
|[Uživatel a IP adresa rekognoskace (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|Rekognoskace pomocí výčtu relací SMB|2012|Střední|Zjišťování|
|

> [!NOTE]
> Pokud chcete zakázat jakoukoli výstrahu zabezpečení, obraťte se na podporu.


## <a name="see-also"></a>Viz také
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Porozumění výstrahám zabezpečení](understanding-security-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
