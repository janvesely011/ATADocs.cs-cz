---
title: Kurz Azure šetření uživatele ochrany ATP v programu | Dokumentace Microsoftu
d|Description: This article explains how to user Azure ATP security alerts to investigate a suspicious user.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/14/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 126653dd2831e0e3dbd9c777d84d32b1c2e74bd9
ms.sourcegitcommit: 1ee052c4c6b04b290e2d5384c24b65a108b1f1f3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/14/2019
ms.locfileid: "54253397"
---
# <a name="tutorial-investigate-a-user"></a>Kurz: Prozkoumat uživatele

Došlo k napadení legitimaci a cesty taktiky Lateral Movement poskytnout jasné údaje při provedení podezřelé aktivity uživatele nebo údaje, které existují jeho účet Azure výstrah ochrany ATP v programu. Pomocí návrhy šetření určit rizika pro vaši organizaci, rozhodněte se, jak opravit a určit nejlepší způsob, jak zabránit budoucím útokům. podobné.  

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

- [Prozkoumat počítače](investigate-a-computer.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Práce s cesty taktiky Lateral Movement](use-case-lateral-movement-path.md)
- [Rekognoskace výstrahy](atp-reconnaissance-alerts.md)
- [Upozornění ohrožení zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Upozornění taktiky Lateral Movement](atp-lateral-movement-alerts.md)
- [Upozornění dominance v doméně](atp-domain-dominance-alerts.md)
- [Upozornění průsak ven](atp-exfiltration-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
