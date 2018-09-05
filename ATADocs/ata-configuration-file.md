---
title: Export a import konfigurace Advanced Threat Analytics | Dokumentace Microsoftu
description: Postup exportu a importu konfigurace ATA
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f8847d8ca3671f765a1d101121eefad62073f60f
ms.sourcegitcommit: 6f1406f28c4c2af6a36bc691ebaf4e819adc6b4b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/04/2018
ms.locfileid: "43675147"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="export-and-import-the-ata-configuration"></a>Export a import konfigurace ATA
Konfigurace ATA je uložená v databázi v kolekci SystemProfile.
Tato kolekce se zálohuje každé 4 hodiny ve službě ATA Center do souboru s názvem: **SystemProfile_*časové razítko*.json**. Jsou uloženy 300 nejnovější verze.
Tento soubor je umístěný v podsložce s názvem **zálohování**. Ve výchozím umístění instalace ATA se nachází tady: *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_* časové-razítko *.json*. 

**Poznámka:** Doporučujeme, abyste si tento soubor někam zazálohovali, pokud v ATA provádíte velké změny.

Je možné obnovit všechna nastavení spuštěním následujícího příkazu:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Viz také
- [Architektura ATA](ata-architecture.md)
- [Požadavky ATA](ata-prerequisites.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

