---
title: "Správa databáze ATA | Microsoft ATA"
description: "Postupy, které vám pomůžou přesunout, zálohovat a obnovit databázi ATA"
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
ms.openlocfilehash: e295e0a0a8b5adbd40ddeb7e389ff82c7482c6d9


---

*Platí pro: Advanced Threat Analytics verze 1.7*



# <a name="ata-database-management"></a>Správa databáze ATA
Když potřebujete přesunout, zálohovat nebo obnovit databázi ATA, použijte tyto postupy pro práci s MongoDB.

## <a name="backing-up-the-ata-database"></a>Zálohování databáze ATA
Viz [příslušná dokumentace k MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Obnovení databáze ATA
Viz [příslušná dokumentace k MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Přesunutí databáze ATA na jinou jednotku

1.  Zastavte službu **Microsoft Advanced Threat Analytics Center**.

2.  Zastavte službu **MongoDB**.

3.  Otevřete konfigurační soubor Mongo, standardně C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Vyhledání parametru `storage: dbPath`

4.  Přesuňte složku uvedenou v parametru `dbPath` do nového umístění.

5.  Změňte parametr `dbPath` v konfiguračním souboru mongo na novou cestu ke složce a uložte a zavřete soubor.

    ![Úprava konfigurační image MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Spusťte službu **MongoDB**.

7. Spusťte službu **Microsoft Advanced Threat Analytics Center**.

## <a name="see-also"></a>Viz také
- [Architektura ATA](/advanced-threat-analytics/plan-design/ata-architecture)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Oct16_HO5-->


