---
title: "Správa databáze ATA | Microsoft ATA"
description: "Postupy, které vám pomůžou přesunout, zálohovat a obnovit databázi ATA"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5cd030f3b952d08c6617a6cda121c344a9c36f51
ms.openlocfilehash: b4e68e9e8dbd94075a34a8e3e8f42d4f534caf50


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# Správa databáze ATA
Když potřebujete přesunout, zálohovat nebo obnovit databázi ATA, použijte tyto postupy pro práci s MongoDB.

## Zálohování databáze ATA
Viz [příslušná dokumentace k MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## Obnovení databáze ATA
Viz [příslušná dokumentace k MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## Přesunutí databáze ATA na jinou jednotku

1.  Zastavte službu **Microsoft Advanced Threat Analytics Center**.

2.  Zastavte službu **MongoDB**.

3.  Otevřete konfigurační soubor Mongo, standardně C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Vyhledání parametru `storage: dbPath`

4.  Přesuňte složku uvedenou v parametru `dbPath` do nového umístění.

5.  Změňte parametr `dbPath` v konfiguračním souboru mongo na novou cestu ke složce a uložte a zavřete soubor.

    ![Úprava konfigurační image MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Spusťte službu **MongoDB**.

7. Spusťte službu **Microsoft Advanced Threat Analytics Center**.

## Konfigurační soubor ATA
Konfigurace ATA je uložená v databázi v kolekci SystemProfile.
Tato kolekce se zálohuje každou hodinu službou ATA Center do souboru s názvem „SystemProfile_*časové-razítko*.json“. Ukládá se 10 posledních verzí.
Je umístěný v podsložce s názvem Backup. Ve výchozím umístění instalace ATA se nachází tady: *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*časové-razítko*.json*. 

**Poznámka:** Doporučujeme, abyste si tento soubor někam zazálohovali, pokud v ATA provádíte velké změny.

Je možné obnovit všechna nastavení spuštěním následujícího příkazu:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## Viz také
- [Architektura ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Aug16_HO5-->


