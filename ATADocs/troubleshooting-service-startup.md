---
title: "Řešení potíží s Advanced Threat Analytics pomocí protokolů | Dokumentace Microsoftu"
description: "Popisuje, jak můžete protokoly ATA použít k řešení potíží."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/26/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1291281273188a21b61b29f06a5220eee589767c
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/30/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="troubleshooting-ata-center-service-startup"></a>Řešení potíží se spuštěním služby ATA Center

Pokud se ATA Center nespustí, postupujte podle následujících pokynů k řešení potíží:

1.  Spusťte následující příkaz Windows PowerShellu: Get-Service Pla | Vyberte stav a ujistěte se, že je spuštěná služba čítače výkonu. Pokud není, jedná se o problém platformy a vy musíte zajistit opětovné spuštění této služby.
2.  Pokud služba byla spuštěná, zkuste ji restartovat a podívejte se, jestli to nevyřeší váš problém: Restart-Service Pla
3.  Zkuste vytvořit ručně nový kolektor dat (bude stačit jakýkoliv, třeba jenom procesor počítače pro sběr dat).
Pokud se dá spustit, je platforma pravděpodobně v pořádku, v opačném případě se jedná o problém platformy.

4.  Zkuste znovu vytvořit ručně kolektor dat ATA z příkazového řádku se zvýšenými oprávněními spuštěním těchto příkazů: sc stop ATACenter logman stop "Microsoft ATA Center" logman export "Microsoft ATA Center" -xml c:\center.xml logman delete "Microsoft ATA Center" logman import "Microsoft ATA Center" -xml c:\center.xml logman start "Microsoft ATA Center" sc start ATACenter



## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
