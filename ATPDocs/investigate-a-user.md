---
title: Kurz k vyšetřování uživatelů v Azure ATP | Microsoft Docs
d|Description: This article explains how to user Azure ATP security alerts to investigate a suspicious user.
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fdf0c4cc32137b23f7c2170a2c8dd0132b3b6462
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71004760"
---
# <a name="tutorial-investigate-a-user"></a>Návodu Prošetřování uživatelů

> [!NOTE]
> Funkce ATP Azure, které jsou na této stránce popsané, jsou dostupné taky pomocí nového [portálu](https://portal.cloudappsecurity.com).

Legitimace výstrah a boční cesty pro Azure ATP poskytují jasné údaje, když uživatelé provedli podezřelé aktivity nebo náznaky, že jejich účet je napadený. V tomto kurzu použijete návrhy na šetření, které vám pomůžou určit riziko pro vaši organizaci, rozhodnout se, jak opravit, a určit nejlepší způsob, jak zabránit podobným budoucím útokům.  

> [!div class="checklist"]
> * Shromážděte informace o uživateli.
> * Prozkoumejte aktivity, které uživatel provedl.
> * Prozkoumejte prostředky, ke kterým se uživatel přistupoval.
> * Prozkoumejte cesty bočního pohybu.

## <a name="recommended-investigation-steps-for-suspicious-users"></a>Doporučené kroky pro šetření pro podezřelé uživatele

Zkontrolujte a prozkoumejte profil uživatele pro následující podrobnosti a aktivity:

1. Kdo je [uživatel](entity-profiles.md)?
     1. Je uživatel [citlivý uživatel](sensitive-accounts.md) (například správce nebo seznamu ke zhlédnutí atd.)?  
     2. Jaká je jejich role v organizaci?
     3. Jsou v organizačním stromu významné?

2. Podezřelé aktivity k [prozkoumání](investigate-entity.md):
     1. Má uživatel další otevřené výstrahy v Azure ATP nebo v jiných nástrojích zabezpečení, jako je Windows Defender – ATP, Azure Security Center a/nebo Microsoft CAS?
     2. Došlo k chybě uživatele při přihlášení?
     3. Ke kterým prostředkům uživatel přistupuje?  
     4. Měl uživatel přístup k prostředkům s vysokou hodnotou?  
     5. Měl by uživatel přistupovat k prostředkům, ke kterým se přistupoval?  
     6. K jakým počítačům se uživatel přihlásil? 
     7. Měl by se uživatel přihlašovat do těchto počítačů?
     8. Existuje mezi uživatelem a citlivým uživatelem [mezipohybová cesta](use-case-lateral-movement-path.md) (LMP)?


## <a name="see-also"></a>Viz také

- [Prošetřování počítačů](investigate-a-computer.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Práce s cestami k příčnému přesunu](use-case-lateral-movement-path.md)
- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před taktikou lateral movement](atp-lateral-movement-alerts.md)
- [Výstrahy před dominancí v doméně](atp-domain-dominance-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
