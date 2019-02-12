---
title: Export a import konfigurace Advanced Threat Analytics | Dokumentace Microsoftu
description: Postup exportu a importu konfigurace ATA
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b1b0c23547783b9cdb671dda35acf7cb8689f64b
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076381"
---
# <a name="export-and-import-the-ata-configuration"></a>Export a import konfigurace ATA

*Platí pro: Advanced Threat Analytics verze 1.9*

Konfigurace ATA je uložená v databázi v kolekci SystemProfile.
Tato kolekce se zálohuje každé 4 hodiny ve službě ATA Center do souboru s názvem: **SystemProfile_*timestamp*.json**. Jsou uloženy 300 nejnovější verze.
Tento soubor je umístěný v podsložce s názvem **zálohování**. Ve výchozím nastavení instalace ATA umístění, do kterého ji najdete tady:  <em>C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_</em>timestamp<em>.json</em>. 

**Poznámka**: Doporučujeme zálohovat tento soubor někam hlavní změny ATA.

Je možné obnovit všechna nastavení spuštěním následujícího příkazu:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Viz také
- [Architektura ATA](ata-architecture.md)
- [Požadavky ATA](ata-prerequisites.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

