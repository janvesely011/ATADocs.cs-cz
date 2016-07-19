---
title: "Správa databáze ATA | Microsoft Advanced Threat Analytics"
description: "Postupy, které vám pomůžou přesunout, zálohovat a obnovit databázi ATA"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 6c0e2abe43da5351568cf8db4e6ffe6fa919d835


---

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

7.  Otevřete příkazový řádek a spusťte prostředí Mongo spuštěním `mongo.exe ATA`.

    Standardně je mongo.exe umístěný v adresáři C:\Program Files\Microsoft rozšířené hrozba Analytics\Center\MongoDB\bin.

8.  Spusťte následující příkaz: `db.SystemProfiles.update( {_t: "CenterSystemProfile"} , {$set:{"Configuration.CenterDatabaseClientConfiguration.DataPath" : "<New DB Location>"}})`


    Místo <New DB Location>, kde `&lt;New DB Location&gt;` je nová cesta ke složce.

9.  Aktualizujte HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath na novou cestu ke složce.

9. Spusťte službu **Microsoft Advanced Threat Analytics Center**.

## Viz také
- [Architektura ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/
- home?forum=mata)




<!--HONumber=Jun16_HO4-->


