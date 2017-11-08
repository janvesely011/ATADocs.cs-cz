---
title: Export a import konfigurace Advanced Threat Analytics | Dokumentace Microsoftu
description: Postup exportu a importu konfigurace ATA
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e1e032adefc650bd4578f29043be313d2c44a866
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="export-and-import-the-ata-configuration"></a>Export a import konfigurace ATA
Konfigurace ATA je uložená v databázi v kolekci SystemProfile.
Tato kolekce se zálohuje každou hodinu službou ATA Center pro soubory:  **SystemProfile_*časové razítko*.json**. Ukládá se 10 posledních verzí. Tento soubor je umístěný v podsložce s názvem **zálohování**. Ve výchozím umístění instalace ATA se nachází tady: *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*časové-razítko*.json*. 

**Poznámka:** Doporučujeme, abyste si tento soubor někam zazálohovali, pokud v ATA provádíte velké změny.

Je možné obnovit všechna nastavení spuštěním následujícího příkazu:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Viz také
- [Architektura ATA](ata-architecture.md)
- [Požadavky ATA](ata-prerequisites.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

