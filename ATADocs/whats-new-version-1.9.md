---
title: Novinky ATA verze 1.9 | Microsoft Docs
description: Uvádí novinky ATA verze 1.9 spolu se známými problémy
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 51de491c-49ba-4aff-aded-cc133a8ccf0b
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: f4a0776d52a69ba519e5cfdd0befb6bbd39d73c3
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
ms.locfileid: "30202387"
---
# <a name="whats-new-in-ata-version-19"></a>Novinky ATA verze 1.9

Nejnovější aktualizovanou verzi ATA je možné [stáhnout z webu Download Center](https://www.microsoft.com/download/details.aspx?id=56725) nebo si můžete plnou verzi stáhnout z webu [Eval center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Tyto poznámky k verzi obsahují informace o aktualizacích, nové funkce, opravy chyb a známé problémy v této verzi Advanced Threat Analytics.

## <a name="new--updated-detections"></a>Nové a aktualizované detekce

-  **Vytvoření podezřelé služby**: útočníci pokusí spustit podezřelé služby ve vaší síti. ATA nyní vyvolá výstrahu, pokud rozpozná, že někdo nové služby, který se zdá podezřelé, běží na řadiči domény. Toto zjišťování je na základě událostí (ne síťový provoz), další informace najdete v tématu [Průvodce podezřelou aktivitu](suspicious-activity-guide.md#suspicious-service-creation).


## <a name="new-reports-to-help-you-investigate"></a>Nové sestavy, které pomáhají s prošetřením 

-   [ **Hesla vystavený jako nezašifrovaný text** ](reports.md) umožňuje rozpoznat, kdy se účty, citlivé a necitlivých, odeslání přihlašovacích údajů k účtu ve formátu prostého textu. To umožňuje prozkoumat a zmírnit použití jednoduché vazby protokolu LDAP ve vašem prostředí, vylepšení úrovně zabezpečení sítě. Tato sestava nahrazuje služby a zpřístupnění citlivých účtů ve formě prostého textu podezřelou aktivitu výstrahy.

- [ **Pomoci odhalit laterální pohyb cesty k citlivým účtům** ](reports.md) uvádí citlivé účty, které jsou zveřejňovány prostřednictvím cesty laterální pohyb. To umožňuje zmírnit tyto cesty a posilovat jejich zabezpečení sítě s cílem minimalizovat riziko útoku prostor. To vám umožňuje zabránit laterální pohyb tak, aby útočníci nelze přesunout ve vaší síti mezi uživatelé a počítače, dokud se dosáhl jackpotu virtuální zabezpečení: přihlašovací údaje účtu citlivé správce.

## <a name="improved-investigation"></a>Vylepšené šetření

-  ATA 1.9 zahrnuje novou a vylepšenou [profil entity](entity-profiles.md). Profil entity poskytuje řídicí panel pro úplné přímým – podrobnější prošetření uživatelé, prostředky, které k nim a jejich historie. Profil entity také umožňuje identifikovat citlivé uživatelé, kteří jsou přístupné přes laterální pohyb cesty. 

-   ATA 1.9 umožňuje [ručně označit skupiny](tag-sensitive-accounts.md) nebo účtů jako citlivé pro zlepšení detekce. Tato označování ovlivňuje, že mnoho ATA detekuje, jako je například zjišťování úpravy citlivou skupinu a cestu laterální pohyb, závisí na které skupiny a účty se považují za citlivé.

## <a name="performance-improvements"></a>Vylepšení výkonu

- ATA Center infrastruktury byl vylepšen výkonu: agregovaná zobrazení provozu umožňuje optimalizace procesoru a paket kanálu a opětovně používá sockets na řadičích domény, chcete-li minimalizovat relací SSL na řadič domény.



## <a name="additional-changes"></a>Další změny

- Po instalaci nové verze ATA [ **co je nového** ](working-with-ata-console.md) ikonu se zobrazí na panelu nástrojů umožníte víte, co se změnilo v nejnovější verzi. Je také poskytuje odkaz na verzi podrobnější protokol změn.


## <a name="removed-and-deprecated-features"></a>Odebrané a zastaralé funkce

- **Poškozený vztah důvěryhodnosti podezřelou aktivitu** výstraha byla odebrána.
- Byl odebrán hesla v nešifrovaném textu podezřelou aktivitu. Byla nahrazena [ **zveřejněné hesla v nešifrovaném textu sestavy**](reports.md).



## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizace ATA na verzi 1.9 – Průvodce migrací](ata-update-1.9-migration-guide.md)

