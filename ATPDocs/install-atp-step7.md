---
title: Azure Advanced Threat Protection konfigurovat vyloučení detekcí a účty honeytoken | Dokumentace Microsoftu
description: Konfigurace vyloučení detekcí a uživatelské účty honeytokenu.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 45858f80efb18060a845da47bfac3353946d18e0
ms.sourcegitcommit: f4f2a1b2c674c4dba7a46ece0624f5ea10c4865e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/02/2018
ms.locfileid: "52744400"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>Konfigurace vyloučení detekcí a účty honeytoken

Ochrana ATP v programu Azure umožňuje vyloučení konkrétních IP adres nebo uživatelů z řady detekcí. 

Například při **vyloučení DNS Reconnaissance** se může jednat o kontrolu zabezpečení, která jako mechanismus pro prohledávání používá službu DNS. Vyloučení pomáhá službě Azure ATP takové kontroly ignorovat.  

Ochrana ATP v programu Azure také umožňuje konfigurovat účty honeytokenu, které se používají jako depeše pro útočníky – jakákoliv autorizace přidružená tyto účty honeytokenu (obvykle neaktivnímu), aktivuje výstrahu.

Pokud chcete nakonfigurovat, postupujte podle těchto kroků:

1.  Z ochrany ATP v programu Azure portal, klikněte na ikonu nastavení a vyberte **konfigurace**.

    ![Konfigurace nastavení služby Azure ATP](media/atp-config-menu.png)

2.  V části **detekce**, klikněte na tlačítko **značky entit**.

3. V části **účty Honeytokenu**, zadejte název účtu Honeytoken a klikněte na tlačítko **+** přihlašování. Pole účtu Honeytokenu lze prohledávat a automaticky zobrazí entity ve vaší síti. Klikněte na **Uložit**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Klikněte na **Vyloučení**. Zadejte uživatelský účet nebo IP adresy, které se mají vyloučit z detekce pro jednotlivé typy hrozeb. 
5. Klikněte na tlačítko *plus* přihlašování. Pole **Add entity** (Přidat entitu) (uživatele nebo počítač) je možné prohledávat a automaticky se vyplní entitami ve vaší síti. Další informace najdete v tématu [vyloučení entit z detekce](excluding-entities-from-detections.md) a [Průvodce výstrah zabezpečení](suspicious-activity-guide.md).

   ![Vyloučení](media/exclusions.png)

6.  Klikněte na **Uložit**.


Blahopřejeme, úspěšně jste nasadili rozšířené ochrany před internetovými útoky pro Azure.

Zkontrolujte na časové ose útoku na zobrazení zjistil výstrah zabezpečení a vyhledejte uživatele nebo počítače a zobrazili jejich profily.

Kontrola Azure ATP okamžitě spustí. Některé způsoby detekce, jako je například neobvyklých změny skupiny vyžadují období učení a nejsou k dispozici okamžitě po nasazení služby Azure ATP.


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum zure ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
