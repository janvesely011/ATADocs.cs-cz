---
title: Posouzení zabezpečení pro nečinný entity Azure Advanced Threat Protection | Microsoft Docs
description: Tento článek poskytuje přehled nečinných entit služby Azure ATP v sestavě posouzení zabezpečení stav citlivých skupin identity.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 190cdecd8ec0835c84329157f2e3a7c76b8b9ebe
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71005218"
---
# <a name="security-assessment-dormant-entities-in-sensitive-groups---preview"></a>Posouzení zabezpečení: Neaktivní entity v **citlivých** skupinách – Preview

## <a name="what-are-sensitive-dormant-entities"></a>Co jsou **citlivé** neaktivní entity? 
Azure ATP zjišťuje, jestli jsou konkrétní uživatelé **citlivé** , a poskytuje atributy, které jsou v případě neaktivního, vypnutí nebo vypršení platnosti. 

**Citlivé** účty ale můžou být *neaktivní* , i když se nepoužívají po dobu 180 dnů. Neaktivní [citlivé entity](sensitive-accounts.md) jsou cílem příležitosti škodlivých aktérů získat citlivý přístup k vaší organizaci. 

## <a name="what-risk-do-dormant-entities-create-in-sensitive-groups"></a>Jaké riziko nečinných entit vytvořit v citlivých skupinách? 

Organizace, které nebezpečnosti svých nespících uživatelských účtů, ponechají v bezpečí dvířka, která jsou chráněná proti citlivým datům.  

Škodlivé objekty actor, podobně jako zloději, často hledají nejjednodušší a tišší způsob v jakémkoli prostředí. Snadná a tichá cesta hluboko ve vaší organizaci je prostřednictvím **citlivých** účtů uživatelů a služeb, které se už nepoužívají. 

Nezáleží na tom, jestli jde o příčinu obratu zaměstnanců nebo prostředků. Tento krok přeskočí z důvodu ohrožení a zpřístupnění nejdůležitějších entit vaší organizace.   

## <a name="how-do-i-use-this-security-assessment"></a>Návody použít toto posouzení zabezpečení? 
1. Pomocí tabulky sestav můžete zjistit, které z vašich citlivých účtů jsou neaktivní. 
1. Z těchto uživatelských účtů proveďte příslušné akce odebráním jejich privilegovaného přístupového práva nebo odstraněním účtu.  


## <a name="see-also"></a>Viz také
- [Filtrování aktivit v Azure ATP v Cloud App Security](atp-activities-filtering-mcas.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
