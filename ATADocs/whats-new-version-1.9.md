---
title: Novinky ATA verze 1.9 | Dokumentace Microsoftu
description: Uvádí novinky ATA verze 1.9 spolu se známými problémy
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 51de491c-49ba-4aff-aded-cc133a8ccf0b
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: b10c2814fcac064d50bce292e86397ea5a0da21e
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196064"
---
# <a name="whats-new-in-ata-version-19"></a>Novinky ATA verze 1.9

Nejnovější aktualizovanou verzi ATA je možné [stáhnout z webu Download Center](https://www.microsoft.com/download/details.aspx?id=56725) nebo si můžete plnou verzi stáhnout z webu [Eval center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).

Tyto poznámky k verzi obsahují informace o aktualizacích, nových funkcích, opravy chyb a známých problémů v této verzi Advanced Threat Analytics.

## <a name="new--updated-detections"></a>Nové a aktualizované detekce

-  **Podezřelé vytvoření služby**: Útočníci se pokusit o spuštění podezřelých služby ve vaší síti. ATA teď zobrazí upozornění, když zjistí, že někdo novou službu, který se zdá podezřelá, běží na řadiči domény. Tato detekce se zakládá na událostech (ne síťový provoz), další informace naleznete v tématu [Průvodce prošetřováním podezřelých aktivit](suspicious-activity-guide.md#suspicious-service-creation).


## <a name="new-reports-to-help-you-investigate"></a>Nové sestavy, které pomáhají s prošetřením 

-   [ **Hesla se odhalily v nešifrovaném textu** ](reports.md) umožňuje rozpoznat, kdy se účty, citlivé a necitlivé, posílají přihlašovací údaje účtu v prostém textu. To vám umožňuje zkoumat a zmírnit použití jednoduché vazby LDAP ve vašem prostředí, vylepšení úrovně zabezpečení sítě. Tato sestava nahrazuje službu a výstrahy podezřelou aktivitu jako nezašifrovaný text k citlivým účtům.

- [ **Laterální cesty Lateral Movement k citlivým účtům** ](reports.md) obsahuje citlivé účty, které jsou zveřejňovány prostřednictvím cesty taktiky Lateral Movement. To umožňuje zmírnit tyto cesty a posilovat jejich zabezpečení sítě s cílem minimalizovat riziko útoku povrchu. To vám umožňuje zabránit taktiky Lateral Movement tak, aby útočníci nelze přesouvat mezi vaší sítě mezi uživatelé a počítače služby, dokud se přístupů v loterii zabezpečení virtuálních: přihlašovací údaje účtu správce citlivé.

## <a name="improved-investigation"></a>Vylepšené šetření

-  ATA 1.9 zahrnuje nové a vylepšené [profil entity](entity-profiles.md). Profil entity poskytuje řídicí panel navržený pro celý podrobný rozbor šetření uživatelů, prostředky, které k nim a jejich historie. Profil entity také umožňuje identifikovat citlivé uživatele, kteří jsou k dispozici prostřednictvím cesty taktiky Lateral Movement. 

-   ATA 1.9 umožňuje [ručně označit skupiny](tag-sensitive-accounts.md) nebo účtů jako citlivé na vylepšit detekce. Toto označení dopady, že mnoho ATA detekuje, jako je například zjišťování úpravy citlivých skupin a cesty laterální pohyb, závisí na jaké skupiny a účty se považují za citlivé.

## <a name="performance-improvements"></a>Vylepšení výkonu

- Infrastruktura ATA Center byla vylepšena z hlediska výkonu: agregovaná zobrazení provozu povolí optimalizaci CPU a paketů kanálu a opětovně používá sockets k řadičům domény, chcete-li minimalizovat relace protokolu SSL řadiči domény.



## <a name="additional-changes"></a>Další změny

- Po dokončení instalace nové verze ATA [ **novinky** ](working-with-ata-console.md) ikony se zobrazí na panelu nástrojů umožňuje víte, co bylo upraveno v nejnovější verzi. Je také poskytuje odkaz na podrobné verze protokolu změn.


## <a name="removed-and-deprecated-features"></a>Odebrané a zastaralé funkce

- **Poškozený vztah důvěryhodnosti podezřelou aktivitu** výstraha byla odebrána.
- Hesla odhalená v nešifrovaných podezřelých aktivit byla odebrána. Byl nahrazen [ **hesla přístupný ve formátu prostého textu sestavy**](reports.md).



## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizace ATA na verzi 1.9 – Průvodce migrací](ata-update-1.9-migration-guide.md)

