---
title: Azure Průvodce výstrah zabezpečení ochrany ATP v programu | Dokumentace Microsoftu
d|Description: This article provides a list of the security alerts issued by Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/13/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2a00a7b4262f37e59de7e3209e939fab63a15415
ms.sourcegitcommit: 6a0ac21f59e72db8615811da2c886f54cf3727f5
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/13/2019
ms.locfileid: "54249959"
---
*Platí pro: Azure Advanced Threat Protection*

# <a name="azure-atp-security-alerts"></a>Výstrahy zabezpečení služby Azure ATP

## <a name="security-alert-name-mapping-and-unique-external-ids"></a>Mapování názvu upozornění zabezpečení a jedinečných externí ID

Ve verzi 2.56 všechny existující výstrahy zabezpečení služby Azure ATP byly přejmenovány s snáze pochopit názvy. Mapování mezi staré i nové názvy a jejich odpovídající jedinečný externalIds jsou uvedené v následující tabulce. Společnost Microsoft doporučuje použití externí ID výstrah místo upozornění názvů pro skripty nebo Automatizace pouze zabezpečení upozornil externí ID jsou trvalé a nelze změnit.

> [!div class="mx-tableFixed"] 

|Nový název výstrahy zabezpečení|Předchozí název výstrahy zabezpečení|Jedinečné ID externí|
|---------|----------|---------|
|Rekognoskace výčtu účtů|Rekognoskace pomocí výčtu účtů|2003|
|Průsak dat ven přes protokol SMB| Není k dispozici| 2030|
|Aktivita Honeytokenu|Aktivita Honeytokenu|2014|
|Škodlivá žádost Data Protection API hlavní klíč|Škodlivá žádost o soukromé informace přes Data Protection|2020|
|Mapování sondování sítě (DNS)|Rekognoskace pomocí DNS|2007|
|Pokus o spuštění vzdáleného kódu|Pokus o spuštění vzdáleného kódu|2019|
|Podezřelý útok hrubou silou (LDAP)|Útok hrubou silou pomocí jednoduché vazby LDAP.|2004|
|Podezřelý útok hrubou silou (pomocí protokolu Kerberos, NTLM)|Podezřelé chyby ověřování|2023|
|Podezřelý útok hrubou silou (SMB)|Neobvyklá implementace protokolu (potenciální použití škodlivých nástrojů, jako je Hydra)|2033|
|Podezřelý útok DCShadow (povýšení řadiče domény)|Povýšení řadiče domény podezřelé (možný útok DCShadow)|2028|
|Podezřelý útok DCShadow (žádost o replikaci řadiče domény)|Žádost o replikaci řadiče domény podezřelé (možný útok DCShadow)|2029|
|Podezřelý útok DCSync (replikace adresářových služeb)|Škodlivá replikace adresářových služeb|2006|
|Podezřelé použití lístku Golden (oslabení šifrování)|Aktivita snížení úrovně šifrování (potenciální útok metodou golden ticket)|2009|
|Podezřelé použití lístku Golden (falešných dat autorizace) |Eskalace oprávnění prostřednictvím zfalšovaných dat autorizace|2013|
|Podezřelé použití Golden Ticket (neexistující účet)|Protokol Kerberos Golden Ticket - neexistující účet|2027|
|Podezřelé použití Golden Ticket (čas anomálií) |Kerberos Golden Ticket – čas anomálií|2022|
|Podezřelé použití Golden Ticket (ticket anomálií) – preview|Není k dispozici|2032|
|Krádež identity podezřelého softwaru (pass-the-hash)|Krádež identity pomocí útoku Pass-the-Hash|2017|
|Krádež identity podezřelého softwaru (pass-the-ticket)|Krádež identity pomocí útoku Pass-the-Ticket|2018|
|Podezření na útok over-pass-the-hash (oslabení šifrování)|Aktivita snížení úrovně šifrování (možný útok overpass-the-hash)|2008|
|Podezření na útok overpass-the-hash (Kerberos)|Neobvyklá implementace protokolu Kerberos (možný útok overpass-the-hash)|2002|
|Podezřelé použití Metasploit hacking framework|Neobvyklá implementace protokolu (potenciální použijte Metasploit hacking nástroje)|2034|
|Útoku typu skeleton key podezřelého softwaru (oslabení šifrování)|Aktivita snížení úrovně šifrování (potenciální útoku typu skeleton key)|2010|
|Podezření na útok WannaCry ransomwaru|Neobvyklá implementace protokolu (možný útok ransomwarem WannaCry)|2035|
|Podezřelá komunikace prostřednictvím DNS|Podezřelá komunikace prostřednictvím DNS|2031|
|Podezřelé úprava citlivých skupin|Podezřelé úprava citlivých skupin|2024|
|Podezřelé vytvoření služby|Podezřelé vytvoření služby|2026|
|Podezřelé připojení k síti VPN|Podezřelé připojení k síti VPN|2025|
|Rekognoskace členství uživatelů a skupin (SAMR)|Rekognoskace pomocí dotazů na adresářové služby|2021|
|Uživatele a IP adres pro rekognoskaci (SMB) |Rekognoskace pomocí výčtu relací SMB|2012|


Upozornění zabezpečení v Azure ochrany ATP v programu jsou rozdělené do následujících kategorií nebo fází, jako je fáze v řetězu událostí typické internetového útoku. Další informace o každé fáze, výstrahy, které jsou navržené k detekování každého útoku a jak používat výstrahy k ochraně sítě pomocí následujících odkazů:

*Fáze:* [1. Rekognoskace výstrahy](atp-reconnaissance-alerts.md)
   <br>[2. Upozornění ohrožení zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
   <br>[3. Upozornění taktiky Lateral Movement](atp-lateral-movement-alerts.md)
   <br>[4. Upozornění dominance v doméně](atp-domain-dominance-alerts.md)
   <br>[5. Upozornění průsak ven](atp-exfiltration-alerts.md)

> [!NOTE]
> Pokud chcete zakázat všechny výstrahy zabezpečení, obraťte se na podporu.


## <a name="see-also"></a>Viz také
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Principy výstrah zabezpečení](understanding-security-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
