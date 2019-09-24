---
title: Stav posouzení zabezpečení identity služby Azure Advanced Threat Protection | Microsoft Docs
description: Tento článek poskytuje přehled sestav hodnocení zabezpečení služby zařazování tisku v Azure ATP pro stav.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1a7d9525-8923-4dae-af51-02a68aa61644
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: da5a9429e802f3597942abc5e21e6c5ae6fed0fb
ms.sourcegitcommit: 15f882cf45776877fdaca8367a7a0fe7f06a7917
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/23/2019
ms.locfileid: "71185545"
---
# <a name="security-assessment-domain-controllers-with-print-spooler-service-available---preview"></a>Posouzení zabezpečení: Řadiče domény se službou zařazování tisku, která je k dispozici – Preview

![Zakázat službu zařazování tisku](media/atp-cas-isp-print-spooler-1.png)
 
## <a name="what-is-the-print-spooler-service"></a>Co je služba **zařazování tisku** ? 

Služba zařazování tisku je softwarová služba, která spravuje procesy tisku. Zařazovací služba přijímá tiskové úlohy z počítačů a zajišťuje, že jsou k dispozici prostředky tiskárny. Zařazovací služba také naplánuje pořadí, ve kterém jsou tiskové úlohy odesílány do tiskové fronty pro tisk. V prvních dnech osobních počítačů museli uživatelé před provedením dalších akcí počkat na vytištění souborů. Díky modernímu zařazování tisku má teď tisk minimální dopad na celkovou produktivitu uživatelů.

## <a name="what-risks-does-the-print-spooler-service-on-domain-controllers-introduce"></a>Jaká rizika služba **zařazování tisku** v řadičích domény zavádí? 

I když zdánlivě neškodný uživatel může vzdáleně připojit k řadiči domény službu zařazování tisku a požádat o aktualizaci nových tiskových úloh. Kromě toho mohou uživatelé určit, že má řadič domény odesílat oznámení do systému s neomezeným [delegováním](atp-cas-isp-unconstrained-kerberos.md). Tyto akce testují připojení a zpřístupňují přihlašovací údaje účtu počítače řadiče domény (**Služba zařazování tisku** je vlastněná systémem). 

Z důvodu možnosti vystavení musí mít řadiče domény a systémy správy služby Active Directory zakázanou službu **zařazování tisku** . Doporučeným způsobem je použít objekt Zásady skupiny (GPO). 

I když se toto posouzení zabezpečení zaměřuje na řadiče domény, může na tento typ útoku potenciálně ohrozit kterýkoli server.

   > [!NOTE]
   > Než zakážete tuto službu a zabráníte aktivním pracovním postupům tisku, ujistěte se, že jste prozkoumali nastavení **služby zařazování tisku** , konfigurace a závislosti

## <a name="how-do-i-use-this-security-assessment"></a>Návody použít toto posouzení zabezpečení? 
1. V tabulce sestav můžete zjistit, které řadiče domény mají povolenou službu **zařazování tisku** .   
    <br>![Zakázat posouzení zabezpečení služby zařazování tisku](media/atp-cas-isp-print-spooler-2.png)
1. V případě rizikových řadičů domény a aktivně odeberte službu zařazování tisku přes objekt zásad skupiny nebo jiné typy vzdálených příkazů, proveďte příslušnou akci.

## <a name="remediation"></a>Náprava

Opravte tento konkrétní problém tím, že zakážete službu zařazování tisku na všech serverech, které to nevyžadují.
  

## <a name="next-steps"></a>Další kroky
- [Filtrování aktivit v Azure ATP v Cloud App Security](atp-activities-filtering-mcas.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)