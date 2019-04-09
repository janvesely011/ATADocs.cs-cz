---
title: Azure Průvodce výstrah zabezpečení ochrany ATP v programu | Dokumentace Microsoftu
d|Description: This article provides a list of the security alerts issued by Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 04/07/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0dcdd37bdad7c52325c527b3fa768f851000ff3a
ms.sourcegitcommit: 4072bb8accd439590412f1380694f19aeaaa7a28
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/08/2019
ms.locfileid: "59233356"
---
# <a name="azure-atp-security-alerts"></a>Výstrahy zabezpečení služby Azure ATP

Upozornění zabezpečení v Azure ochrany ATP v programu popisují podezřelých aktivitách zjištěných ochrany ATP v programu Azure senzorů v síti a objekty actor a počítačů zahrnutých v každém útoky.   Upozornění důkazy seznamy obsahovat přímé odkazy na související uživatelé a počítače, abyste se mohli vaše šetření, snadno a s přímým přístupem.

Upozornění zabezpečení v Azure ochrany ATP v programu jsou rozdělené do následujících kategorií nebo fází, jako je fáze v řetězu událostí typické internetového útoku. Další informace o každé fáze, výstrahy, které jsou navržené k detekování každého útoku a jak používat výstrahy k ochraně sítě pomocí následujících odkazů:
  1. [Upozornění fáze rekognoskace](atp-reconnaissance-alerts.md)
  2. [Ohrožení zabezpečení přihlašovacích údajů Fáze oznámení](atp-compromised-credentials-alerts.md)
  3. [Laterální pohyb fáze oznámení](atp-lateral-movement-alerts.md)
  4. [Upozornění fáze dominance v doméně](atp-domain-dominance-alerts.md)
  5. [Fáze oznámení průsak ven](atp-exfiltration-alerts.md)

Další informace o struktuře a běžné součásti všech výstrah zabezpečení ochrany ATP v programu Azure najdete v tématu [Principy výstrah zabezpečení](understanding-security-alerts.md).

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>Mapování názvu upozornění zabezpečení a jedinečných externí ID

Ve verzi 2.56 všechny existující výstrahy zabezpečení služby Azure ATP byly přejmenovány s snáze pochopit názvy. Mapování mezi staré i nové názvy a jejich odpovídající jedinečný externalIds jsou uvedené v následující tabulce. Při použití se skripty a automatizace, společnost Microsoft doporučuje použití externí ID výstrah místo upozornění názvů, pouze zabezpečení upozornil externí ID jsou trvalé a nelze změnit.

> [!div class="mx-tableFixed"] 

|Nový název výstrahy zabezpečení|Předchozí název výstrahy zabezpečení|Jedinečné ID externí|Severity|MITRE ATT&CK Matrix™ |
|---------|----------|---------|---------|---------|
|[Rekognoskace výčtu účtů](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)|Rekognoskace pomocí výčtu účtů|2003|Střední|Zjišťování|
|[Průsak dat ven přes protokol SMB](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)| Není k dispozici| 2030|Vysoká|Průsak ven,<br>Laterální pohyb<br>Příkazy a ovládání|
|[Aktivita Honeytokenu](atp-compromised-credentials-alerts.md#honeytoken-activity-external-id-2014)|Aktivita Honeytokenu|2014|Střední|Přihlašovací údaje přístup<br> Zjišťování|
|[Škodlivá žádost Data Protection API hlavní klíč](atp-domain-dominance-alerts.md#malicious-request-of-data-protection-api-master-key-external-id-2020)|Škodlivá žádost o soukromé informace přes Data Protection|2020|Vysoká|Přihlašovací údaje přístup|
|[Mapování sondování sítě (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)|Rekognoskace pomocí DNS|2007|Střední|Zjišťování|
|[Pokus o spuštění vzdáleného kódu](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)|Pokus o spuštění vzdáleného kódu|2019|Střední|Spuštění,<br> Trvalost,<br> Zvýšení úrovně oprávnění<br> Únik obrany<br> Laterální pohyb|
|[Vzdálené spuštění kódu v DNS](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)|Není k dispozici|2036|Střední|Zvýšení úrovně oprávnění<br> Laterální pohyb|
|[Rekognoskace instančního objektu zabezpečení (LDAP) – preview](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038---preview)|Není k dispozici|2038|Střední|Přihlašovací údaje přístup|
|[Podezřelý útok hrubou silou (pomocí protokolu Kerberos, NTLM)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-kerberos-ntlm-external-id-2023)|Podezřelé chyby ověřování|2023|Střední|Přihlašovací údaje přístup|
|[Podezřelý útok hrubou silou (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004)|Útok hrubou silou pomocí jednoduché vazby LDAP.|2004|Střední|Přihlašovací údaje přístup|
|[Podezřelý útok hrubou silou (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)|Neobvyklá implementace protokolu (potenciální použití škodlivých nástrojů, jako je Hydra)|2033|Střední|Laterální pohyb|
|[Podezřelý útok DCShadow (povýšení řadiče domény)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-promotion-external-id-2028)|Povýšení řadiče domény podezřelé (možný útok DCShadow)|2028|Vysoká|Únik obrany|
|[Podezřelý útok DCShadow (žádost o replikaci řadiče domény)](atp-domain-dominance-alerts.md#suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029)|Žádost o replikaci řadiče domény podezřelé (možný útok DCShadow)|2029|Vysoká|Únik obrany|
|[Podezřelý útok DCSync (replikace adresářových služeb)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)|Škodlivá replikace adresářových služeb|2006|Vysoká|Trvalost,<br> Přihlašovací údaje přístup|
|[Podezřelé použití lístku Golden (oslabení šifrování)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-encryption-downgrade-external-id-2009)|Aktivita snížení úrovně šifrování (potenciální útok metodou golden ticket)|2009|Střední|Zvýšení úrovně oprávnění<br> Laterální pohyb<br>Trvalost|
|[Podezřelé použití lístku Golden (falešných dat autorizace)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-forged-authorization-data-external-id-2013)|Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace|2013|Vysoká|Zvýšení úrovně oprávnění<br>Laterální pohyb<br>Trvalost|
|[Podezřelé použití Golden Ticket (neexistující účet)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)|Protokol Kerberos Golden Ticket - neexistující účet|2027|Vysoká|Zvýšení úrovně oprávnění<br> Laterální pohyb<br>Trvalost|
|[Podezřelé použití Golden Ticket (ticket anomálií)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)|Není k dispozici|2032|Vysoká|Zvýšení úrovně oprávnění<br> Laterální pohyb<br>Trvalost|
|[Podezřelé použití Golden Ticket (čas anomálií)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)|Kerberos Golden Ticket – čas anomálií|2022|Vysoká|Zvýšení úrovně oprávnění<br> Laterální pohyb<br>Trvalost|
|[Krádež identity podezřelého softwaru (pass-the-hash)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-hash-external-id-2017)|Krádež identity pomocí útoku Pass-the-Hash|2017|Vysoká|Laterální pohyb|
|[Krádež identity podezřelého softwaru (pass-the-ticket)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)|Krádež identity pomocí útoku Pass-the-Ticket|2018|Střední nebo Vysoká|Laterální pohyb|
|[Podezření na útok over-pass-the-hash (oslabení šifrování)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008)|Aktivita snížení úrovně šifrování (možný útok overpass-the-hash)|2008|Střední|Laterální pohyb|
|[Podezření na útok overpass-the-hash (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)|Neobvyklá implementace protokolu Kerberos (možný útok overpass-the-hash)|2002|Střední|Laterální pohyb|
|[Útoku typu skeleton key podezřelého softwaru (oslabení šifrování)](atp-domain-dominance-alerts.md#suspected-skeleton-key-attack-encryption-downgrade-external-id-2010)|Aktivita snížení úrovně šifrování (potenciální útoku typu skeleton key)|2010|Střední|Laterální pohyb<br> Trvalost|
|[Podezřelé použití Metasploit hacking framework](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)|Neobvyklá implementace protokolu (potenciální použijte Metasploit hacking nástroje)|2034|Střední|Laterální pohyb|
|[Podezření na útok relay NTLM (účet Exchange) – preview](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview)|Není k dispozici|2037|Střední nebo Nízká, pokud pomocí podepsané protokolu NTLM v2|Zvýšení úrovně oprávnění <br> Laterální pohyb|
|[Podezření na útok WannaCry ransomwaru](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)|Neobvyklá implementace protokolu (možný útok ransomwarem WannaCry)|2035|Střední|Laterální pohyb|
|[Podezřelá komunikace prostřednictvím DNS](atp-exfiltration-alerts.md#suspicious-communication-over-dns-external-id-2031)|Podezřelá komunikace prostřednictvím DNS|2031|Střední|Průsak ven|
|[Podezřelé úprava citlivých skupin](atp-domain-dominance-alerts.md#suspicious-modification-of-sensitive-groups-external-id-2024)|Podezřelé úprava citlivých skupin|2024|Střední|Přihlašovací údaje přístup<br>Trvalost|
|[Podezřelé vytvoření služby](atp-domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)|Podezřelé vytvoření služby|2026|Střední|Spuštění,<br> Trvalost,<br> Zvýšení úrovně oprávnění<br> Únik obrany<br>Laterální pohyb|
|[Podezřelé připojení k síti VPN](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)|Podezřelé připojení k síti VPN|2025|Střední|Trvalost,<br>Únik obrany|
|[Rekognoskace členství uživatelů a skupin (SAMR)](atp-reconnaissance-alerts.md#user-and-group-membership-reconnaissance-samr-external-id-2021)|Rekognoskace pomocí dotazů na adresářové služby|2021|Střední|Zjišťování|
|[Uživatele a IP adres pro rekognoskaci (SMB)](atp-reconnaissance-alerts.md#user-and-ip-address-reconnaissance-smb-external-id-2012)|Rekognoskace pomocí výčtu relací SMB|2012|Střední|Zjišťování|
|

> [!NOTE]
> Pokud chcete zakázat všechny výstrahy zabezpečení, obraťte se na podporu.


## <a name="see-also"></a>Viz také
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Porozumění výstrahám zabezpečení](understanding-security-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
