---
title: "Řešení potíží s Advanced Threat Analytics pomocí protokolů | Dokumentace Microsoftu"
description: "Popisuje, jak můžete protokoly ATA použít k řešení potíží."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 125376b1e3530481a3b9f62c4661dd10dce13f22
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="troubleshooting-ata-center-service-startup"></a>Řešení potíží se spuštěním služby ATA Center

Pokud ATA Center se nespustí, proveďte následující postup řešení potíží:

1.  Spusťte následující příkaz prostředí Windows PowerShell: `Get-Service Pla | Select Status` a ujistěte se, je spuštěna služba čítače výkonu. Pokud není, jedná se o problém platformy a vy musíte zajistit opětovné spuštění této služby.
2.  Pokud byl spuštěn, pokusí se ji restartovat a zobrazí, pokud se tím problém nevyřeší:`Restart-Service Pla`
3.  Zkuste vytvořit ručně nový kolektor dat (bude stačit jakýkoliv, třeba jenom procesor počítače pro sběr dat).
Pokud můžete spustit, je pravděpodobně poškozena platformu. Pokud ne, je stále problém platformy.

4.  Zkuste znovu vytvořit ručně ATA kolekcí dat, pomocí řádku se zvýšenými oprávněními, spuštění těchto příkazů:

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter



## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
