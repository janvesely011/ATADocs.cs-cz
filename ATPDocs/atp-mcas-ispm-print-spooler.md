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
ms.openlocfilehash: 0be5e5c80c4a055e5248bf90fa987f4bf5b3c668
ms.sourcegitcommit: 09275d3400534200fa6ea572e89e440b3cc58360
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2019
ms.locfileid: "67788816"
---
# <a name="security-assessment-domain-controllers-with-print-spooler-service-available"></a>Posouzení zabezpečení: Řadiče domény se službou zařazování tisku je k dispozici

![Zakázat službu zařazování tisku](media/atp-mcas-ispm-print-spooler-1.png)
 
## <a name="what-is-the-print-spooler-service"></a>Co je služba **zařazování tisku** ? 

Služba zařazování tisku je softwarová služba, která spravuje procesy tisku. Zařazovací služba přijímá tiskové úlohy z počítačů a zajišťuje, že jsou k dispozici prostředky tiskárny. Zařazovací služba také naplánuje pořadí, ve kterém jsou tiskové úlohy odesílány do tiskové fronty pro tisk. V prvních dnech osobních počítačů museli uživatelé před provedením dalších akcí počkat na vytištění souborů. Díky modernímu zařazování tisku má teď tisk minimální dopad na produktivitu uživatelů.

## <a name="what-risks-does-the-print-spooler-service-on-domain-controllers-introduce"></a>Jaká rizika služba **zařazování tisku** v řadičích domény zavádí? 

I když zdánlivě neškodný uživatel může vzdáleně připojit k řadiči domény službu zařazování tisku a požádat o aktualizaci nových tiskových úloh. Kromě toho mohou uživatelé určit, že má řadič domény odesílat oznámení do systému s neomezeným [delegováním](atp-mcas-ispm-unconstrained-kerberos.md). Tyto akce testují připojení a zpřístupňují přihlašovací údaje účtu počítače řadiče domény (**Služba zařazování tisku** je vlastněná systémem). 

Z důvodu možnosti vystavení musí mít řadiče domény a systémy správy služby Active Directory zakázanou službu **zařazování tisku** . Doporučeným způsobem je použít objekt Zásady skupiny (GPO). 

I když se toto posouzení zabezpečení zaměřuje na řadiče domény, může na tento typ útoku potenciálně ohrozit kterýkoli server.

## <a name="how-do-i-use-this-security-assessment"></a>Návody použít toto posouzení zabezpečení? 
1. V tabulce sestav můžete zjistit, které řadiče domény mají povolenou službu **zařazování tisku** .   
    <br>![Zakázat posouzení zabezpečení služby zařazování tisku](media/atp-mcas-ispm-print-spooler-2.png)
1. V případě rizikových řadičů domény a aktivně odeberte službu zařazování tisku přes objekt zásad skupiny nebo jiné typy vzdálených příkazů, proveďte příslušnou akci.

## <a name="remediation"></a>Náprava

Tento problém vyřešte tak, že zakážete službu zařazování tisku na všech serverech, které ji nevyžadují, a zajistěte, aby nedocházelo k žádným účtům s nakonfigurovaným neomezeným delegováním.
  

## <a name="next-steps"></a>Další postup
- [Filtrování aktivit v Azure ATP v Cloud App Security](atp-activities-filtering-mcas.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)