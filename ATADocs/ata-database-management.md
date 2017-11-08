---
title: "Správa databáze Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Postupy, které vám pomůžou přesunout, zálohovat a obnovit databázi ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 98923fbd56678291c4e10e595396f9454b0aeb11
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="ata-database-management"></a>Správa databáze ATA
Když potřebujete přesunout, zálohovat nebo obnovit databázi ATA, použijte tyto postupy pro práci s MongoDB.

## <a name="backing-up-the-ata-database"></a>Zálohování databáze ATA
Viz [příslušná dokumentace k MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Obnovení databáze ATA
Viz [příslušná dokumentace k MongoDB](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Přesunutí databáze ATA na jinou jednotku

1.  Zastavte službu **Microsoft Advanced Threat Analytics Center**.
> [!Important] 
> Zajistěte, aby se před přechodem k dalšímu kroku služba ATA Center zastavila.

2.  Zastavte službu **MongoDB**.

3.  Otevřete konfigurační soubor Mongo, standardně C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Vyhledání parametru `storage: dbPath`

4.  Přesuňte složku uvedenou v parametru `dbPath` do nového umístění.

5.  Změňte parametr `dbPath` v konfiguračním souboru mongo na novou cestu ke složce a uložte a zavřete soubor.

    ![Úprava konfigurační image MongoDB](media/ATA-mongoDB-moveDB.png)

6.  Spusťte službu **MongoDB**.

7. Spusťte službu **Microsoft Advanced Threat Analytics Center**.

## <a name="see-also"></a>Viz také
- [Architektura ATA](ata-architecture.md)
- [Požadavky ATA](ata-prerequisites.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

