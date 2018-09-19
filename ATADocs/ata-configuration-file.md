---
title: Export a import konfigurace Advanced Threat Analytics | Dokumentace Microsoftu
description: Postup exportu a importu konfigurace ATA
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3abe18d7da00e5af0373d74db2dc2dc1f91a6fc9
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133306"
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

