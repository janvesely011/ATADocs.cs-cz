---
title: Referenční informace o události ID ATA | Dokumentace Microsoftu
description: Poskytuje seznam události ID ATA a jejich popisy.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: e21e2b984db3d58703cf6503817401f1bab0fda1
ms.sourcegitcommit: c390d36d75f13607698c2a8d7ac757ecef4c748e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53709910"
---
*Platí pro: Advanced Threat Analytics verze 1.9*


# <a name="ata-event-id-reference"></a>ATA referenční informace o ID události

V prohlížeči událostí komponenty ATA Center protokoluje události pro ATA. Tento článek obsahuje seznam ID událostí a popis jednotlivých.

Události najdete tady:

![umístění ID události](./media/event-id-location.png)

## <a name="ata-health-events"></a>Události stavu ATA

|ID události monitorování| Název monitorování výstrah|
|---------|---------------|
|1001|System Center dochází místo na disku|
|1003|System Center přetížení|
|1004|Vypršela platnost certifikátu Center se vypršení platnosti / Center certifikátu|
|1005|MongoDB je mimo provoz|
|1006|Hesla uživatele jen pro čtení, který brzy vyprší platnost nebo platnost hesla uživatele jen pro čtení|
|1007|Nepřiřazený synchronizátor domény|
|1008|Nejsou k dispozici některé nebo všechny síťové adaptéry pro zachytávání na bránu|
|1009|Síťový adaptér pro zachytávání na bránu už neexistuje.|
|1010|Některé řadiče domény nejsou dostupné prostřednictvím brány / všechny řadiče domény nejsou dostupné prostřednictvím brány|
|1011|Gateway přestala komunikovat|
|1012|Některé předané události se neanalyzují|
|1013|Některý síťový provoz se neanalyzuje|
|1014|Chyba odeslání e-mailu|
|1015|Neúspěšné připojení k serveru SIEM pomocí protokolu Syslog|
|1016|Verze brány zastaralá|
|1017|Z řadiče domény se nepřijímá žádný provoz|
|1018|Nepovedlo se spustit službu brány|
|1019|Komponenta Lightweight Gateway dosáhla limitu prostředků paměti|
|1020|Brána nezpracovává události Radius|
|1021|Brána nezpracovává události Syslog|
|1022|Informace o zeměpisné poloze služba není dostupná.|
 
## <a name="ata-security-alert-events"></a>Události výstrah zabezpečení ATA

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

## <a name="ata-auditing-events"></a>Události auditu ATA

|Upozornění názvy|ID oznámení událostí|
|---------|---------------|
|3001|Změna konfigurace ATA|
|3002|Přidání komponenty ATA Gateway|
|3003|Odstranit komponenty ATA Gateway|
|3004|Aktivovat licenci ATA|
|3005|Přihlášení ke konzole ATA|
|3006|Ruční změna stavu aktivity|
|3007|Ruční změna stavu podezřelé aktivity|

## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
