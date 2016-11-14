---
title: "Konfigurační soubor ATA | Microsoft ATA"
description: "Zálohování konfigurace ATA"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 10/31/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f334f9c8440e4bb0202579de220f6530d0aabad8
ms.openlocfilehash: 542bdf983e26fa98c036de55860b482d0b1d734d


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="ata-configuration-file"></a>Konfigurační soubor ATA
Konfigurace ATA je uložená v databázi v kolekci SystemProfile.
Tato kolekce se zálohuje každou hodinu službou ATA Center do souboru s názvem „SystemProfile_*časové-razítko*.json“. Ukládá se 10 posledních verzí.
Je umístěný v podsložce s názvem Backup. Ve výchozím umístění instalace ATA se nachází tady: *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*časové-razítko*.json*. 

**Poznámka:** Doporučujeme, abyste si tento soubor někam zazálohovali, pokud v ATA provádíte velké změny.

Je možné obnovit všechna nastavení spuštěním následujícího příkazu:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Viz také
- [Architektura ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Oct16_HO5-->


