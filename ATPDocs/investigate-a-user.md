---
title: Kurz Azure šetření uživatele ochrany ATP v programu | Dokumentace Microsoftu
d|Description: This article explains how to user Azure ATP security alerts to investigate a suspicious user.
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 02/07/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d130cc6c52f27052305ae012409363e8437db5f6
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/14/2019
ms.locfileid: "56264073"
---
# <a name="tutorial-investigate-a-user"></a>Kurz: Prozkoumat uživatele

Došlo k napadení legitimaci a cesty taktiky Lateral Movement poskytnout jasné údaje při provedení podezřelé aktivity uživatele nebo údaje, které existují jeho účet Azure výstrah ochrany ATP v programu. V tomto kurzu použijete šetření návrhy pomůže určit rizika pro vaši organizaci, rozhodněte se, jak opravit a určit nejlepší způsob, jak zabránit budoucím útokům. podobné.  

> [!div class="checklist"]
> * Shromážděte informace o uživateli.
> * Prozkoumejte aktivity, které uživatel provedl.
> * Prozkoumejte prostředky uživatele získat přístup.
> * Prošetřování laterálních průnikových.

## <a name="recommended-investigation-steps-for-suspicious-users"></a>Doporučená pomoc postup podezřelé uživatele

Zkontrolujte a prozkoumat profil uživatele pro následující údaje a aktivity:

1. Kdo je [uživatele](entity-profiles.md)?
     1. Uživatel [citlivé uživatele](sensitive-accounts.md) (jako je například správce nebo seznamu ke zhlédnutí, atd.)?  
     2. Jaká je jejich role v organizaci?
     3. Jsou významné ve stromové struktuře organizační?

2. Podezřelých aktivit a [prozkoumat](investigate-entity.md):
     1. Uživatel nemá další otevřít upozornění v ochrany ATP v programu Azure nebo v jiných nástrojích zabezpečení, jako je Windows Defender – ochrana ATP v programu, Azure Security Center a/nebo Microsoft CAS?
     2. Uživatele se nepodařilo přihlášení?
     3. Které prostředky uživatel přístup?  
     4. Uživateli přístup k prostředkům vysoké hodnoty?  
     5. Byl uživatel má přístup k prostředkům, které k nim přistupovat?  
     6. Počítače, které uživatel přihlásit k? 
     7. Byl uživatel má k přihlášení do těchto počítačů?
     8. Je k dispozici [cesty laterální pohyb](use-case-lateral-movement-path.md) (LMP) mezi uživatelem a citlivé uživatele?


## <a name="see-also"></a>Viz také

- [Prošetřování počítačů](investigate-a-computer.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Práce s cesty taktiky Lateral Movement](use-case-lateral-movement-path.md)
- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před taktikou lateral movement](atp-lateral-movement-alerts.md)
- [Výstrahy před dominancí v doméně](atp-domain-dominance-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
