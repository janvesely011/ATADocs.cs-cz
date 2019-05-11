---
title: Export a import konfigurace Advanced Threat Analytics | Dokumentace Microsoftu
description: Postup exportu a importu konfigurace ATA
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 06c225b26c43d48aeba6c032434af08231106dad
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196463"
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

