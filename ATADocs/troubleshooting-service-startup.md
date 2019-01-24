---
title: Řešení potíží se spuštěním služby Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje, jak můžete řešit problémy s ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 21afd487fbf15b3fc1f5d618e0e6b98d50d07cae
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2019
ms.locfileid: "54839559"
---
# <a name="troubleshooting-service-startup"></a>Řešení potíží se spuštěním služby

*Platí pro: Advanced Threat Analytics verze 1.9*

## <a name="troubleshooting-ata-center-service-startup"></a>Řešení potíží se spuštěním služby ATA Center

Pokud ATA Center nespustí, proveďte následující postup řešení potíží:

1.  Spuštěním následujícího příkazu Windows Powershellu: `Get-Service Pla | Select Status`
    Ujistěte se, že je spuštěna služba čítače výkonu. Pokud není, jedná se o problém platformy a vy musíte zajistit opětovné spuštění této služby.
2.  Pokud byl spuštěn, zkuste ji restartovat a jestli řešení problému: `Restart-Service Pla`
3.  Zkuste vytvořit ručně nový kolektor dat (bude stačit jakýkoliv, třeba jenom procesor počítače pro sběr dat).
Pokud se dá spustit, je platforma pravděpodobně v pořádku. V opačném případě se stále o problém platformy.

4.  Zkuste znovu vytvořit ručně kolektor dat ATA, pomocí řádku se zvýšenými oprávněními spuštěním těchto příkazů:

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>Řešení potíží se spuštěním ATA Lightweight Gateway

**Symptom**

ATA Gateway se nespustí a zobrazí tato chyba:<br></br>
*System.Net.Http.HttpRequestException: Stavový kód odpovědi neoznačuje Úspěch: 500 (vnitřní chyba serveru)*

**Popis**

K tomu dochází, protože jako součást procesu instalace Lightweight Gateway, ATA přiděluje prahová hodnota využití procesoru umožňuje Lightweight Gateway pro využití procesoru s vyrovnávací pamětí 15 %. Pokud jste nastavili nezávisle na sobě prahové hodnoty pomocí klíče registru: Tento konflikt zabrání Lightweight Gateway spuštění. 

**Řešení**

1. V registru názvem klíče, pokud je hodnota DWORD **zakažte čítače výkonu** Ujistěte se, že je nastavena na **0**: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\`
    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance`
 
2. Restartujte službu service Pla. ATA Lightweight Gateway bude automaticky rozpoznávat změny a restartujte službu.


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
