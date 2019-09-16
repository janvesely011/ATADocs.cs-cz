---
title: Kurz k vyšetřování počítačů v Azure ATP | Microsoft Docs
d|Description: This article explains how to use Azure ATP security alerts to investigate a suspicious computer.
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 91fc13a9d85e8d3653965530a9f0f35debaa728f
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71004782"
---
# <a name="tutorial-investigate-a-computer"></a>Návodu Prošetřování počítačů

> [!NOTE]
> Funkce ATP Azure, které jsou na této stránce popsané, jsou dostupné taky pomocí nového [portálu](https://portal.cloudappsecurity.com).

Legitimace s výstrahami Azure ATP poskytuje jasné údaje o tom, že počítače byly zapojeny do podezřelých aktivit nebo když existují náznaky ohrožení počítače. V tomto kurzu použijete návrhy na šetření, které vám pomůžou určit riziko pro vaši organizaci, rozhodnout se, jak opravit, a určit nejlepší způsob, jak v budoucnu zabránit podobným útokům.  

> [!div class="checklist"]
> * Ověřte, jestli je počítač přihlášený uživatel.
> * Ověřte, jestli uživatel normálně přistupuje k počítačům.
> * Prozkoumejte podezřelé aktivity z počítače.
> * V jakém časovém intervalu jsou jiné výstrahy?


## <a name="investigation-steps-for-suspicious-computers"></a>Postup šetření pro podezřelé počítače

Chcete-li získat přístup na stránku profil počítače, klikněte na konkrétní počítač uvedený v výstraze, kterou chcete prozkoumat. Pro pomoc s vyšetřováním legitimace výstrah zobrazí seznam všech počítačů (a [uživatelů](investigate-a-user.md)) připojených ke každé podezřelé aktivitě.

Zkontrolujte a prozkoumejte profil počítače s následujícími podrobnostmi a aktivitami:

- Co se stalo kolem času podezřelé aktivity?  
  1. K jakému [uživateli](investigate-a-user.md) byl přihlášen počítač?
  2. Se tento uživatel normálně přihlašuje nebo ke zdrojovému nebo cílovému počítači přistupuje?
  3. K jakým prostředkům se má přistupovat? Podle kterých uživatelů?
      - Pokud byly k prostředkům přistupované, byly to prostředky s vysokou hodnotou?
  4. Měl by uživatel přistupovat k těmto prostředkům?
  5. Měl by [uživatel](investigate-a-user.md) , který získal k počítači, provádět jiné podezřelé aktivity?

- Další podezřelé aktivity k prozkoumání:
    1. Byly se další výstrahy otevíraly přibližně ve stejnou dobu jako tato výstraha v Azure ATP nebo v jiných nástrojích zabezpečení, jako je ochrana ATP v programu Windows Defender, Azure Security Center a/nebo Microsoft CAS?
    2. Došlo k neúspěšným přihlášením?


- Pokud je povolená integrace ochrany ATP v programu Windows Defender, klikněte na označení ATP ATP v programu Windows Defender a prozkoumejte počítač dále. V rámci ochrany ATP v programu Windows Defender vidíte, které procesy a výstrahy vzstaly přibližně ve stejnou dobu jako výstraha.
    1. Byly nějaké nové programy nasazené nebo nainstalované?

## <a name="next-steps"></a>Další postup

- [Prošetřování uživatelů](investigate-a-user.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Práce s cestami k příčnému přesunu](use-case-lateral-movement-path.md)
- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před taktikou lateral movement](atp-lateral-movement-alerts.md)
- [Výstrahy před dominancí v doméně](atp-domain-dominance-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
