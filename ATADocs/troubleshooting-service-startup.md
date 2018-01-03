---
title: "Řešení potíží s spuštění služby Advanced Threat Analytics | Microsoft Docs"
description: "Popisuje, jak můžete potíže ATA spuštění"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 12/20/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 33ff11f592984b754521c562414ffeabd2d1f255
ms.sourcegitcommit: 91158e5e63ce2021a1f5f85d47de03d963b7cb70
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="troubleshooting-service-startup"></a>Řešení potíží s spuštění služby

## <a name="troubleshooting-ata-center-service-startup"></a>Řešení potíží se spuštěním služby ATA Center

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

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Řešení potíží s ATA Lightweight Gateway spuštění

**Příznaky**

ATA Gateway se nespustí a se tato chyba:<br></br>
*System.Net.Http.HttpRequestException: Stavový kód odpovědi není indikuje úspěšné provedení: 500 (vnitřní chyba serveru)*

**Popis**

K tomu dochází, protože jako součást procesu instalace Lightweight Gateway, ATA přiděluje procesoru prahovou hodnotu, která umožňuje Lightweight Gateway pro využití procesoru s vyrovnávací paměť % 15. Pokud jste nastavili nezávisle prahovou hodnotu pomocí klíče registru: Tento konflikt zabrání Lightweight Gateway spuštění. 

**Řešení**

1. V registru klíče, pokud je hodnota DWORD názvem **zakázat čítače výkonu** zkontrolujte, zda je nastavena na **0**: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\``HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance`
 
2. Potom restartujte službu Pla. ATA Lightweight Gateway automaticky rozpozná změny a restartujte službu.


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
