---
title: Kontrola Azure Advanced Threat ochrany rozšířené zásady auditu | Dokumentace Microsoftu
description: Tento článek obsahuje přehled služby Azure ATP pokročilé zásady auditu kontroly.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: ab1e8dd9-a6c2-4c68-89d5-343b8ec56142
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d2dbd84cf771e86a5615a081b6e8500247ee2026
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674669"
---
# <a name="azure-atp-advanced-audit-policy-check"></a>Kontrola zásad auditu rozšířené ochrany ATP v programu Azure

Azure ATP detekce spoléhá na konkrétní Windows protokoly událostí pro viditelnost v některých scénářích, jako je například přihlašování, úpravy skupin zabezpečení a podobné události protokolu NTLM. Pro správné události, které mají být auditovat a zahrnuty v protokolu událostí Windows řadiče domény vyžadují nastavení přesné pokročilé zásady auditu. Nesprávné nastavení Pokročilé zásady auditu ponechte kritické události z protokolů a výsledků v pokrytí nebudou úplná ochrany ATP v programu Azure.

Aby bylo snazší a ověřit aktuální stav každé ze zásad auditu Advanced řadič domény, ochrana ATP v programu Azure automaticky kontroluje existující upozornění stavu pokročilé zásady auditu a problémy pro nastavení zásad, které vyžadují úpravu. Jednotlivé výstrahy stavu poskytuje konkrétní podrobnosti řadič domény, problematický zásady stejně jako návrhy nápravu.

![Upozornění na stav zásad auditu Upřesnit](media/atp-health-alert-audit-policy.png)


Pokročilé zásady auditu zabezpečení povolená přes **výchozí zásada řadičů domény** objektu zásad skupiny. Tyto auditování, události se zaznamenávají v řadiči domény Windows události. 

## <a name="modify-audit-policies"></a>Upravit zásady auditu 

Upravte zásady auditu Upřesnit vaše řadiče domény pomocí následujících pokynů:

1. Přihlaste se k serveru jako **správce domény**.
2. Načíst Editor správy zásad skupiny z **správce serveru** > **nástroje** > **Správa zásad skupiny**. 
3. Rozbalte **organizační jednotky řadiče domény**, klikněte pravým tlačítkem na **výchozí zásada řadičů domény** a vyberte **upravit**. 

    ![Upravit zásady řadiče domény](media/atp-advanced-audit-policy-check-step-1.png)

4. V okně, které se otevře, přejděte na **konfigurace počítače** > **zásady** > **nastavení Windows**  >  **Nastavení zabezpečení** > **Upřesnit konfiguraci zásad auditování**.

    ![Upřesnit konfiguraci zásad auditování](media/atp-advanced-audit-policy-check-step-2.png)

5. Přejděte k přihlášení k účtu, dvakrát klikněte na **auditovat ověřování pověření** a vyberte **konfigurovat následující události auditu** pro události úspěchy a chyby. 

    ![Ověřování přihlašovacích údajů](media/atp-advanced-audit-policy-check-step-3.png)

6. Přejděte na správu účtů, dvakrát klikněte na **Auditovat správu skupiny zabezpečení** a vyberte **konfigurovat následující události auditu** pro události úspěchy a chyby.

    ![Auditovat správu skupiny zabezpečení](media/atp-advanced-audit-policy-check-step-4.png)

    > [!NOTE]
    > Pokud se rozhodnete použít místní zásady, nezapomeňte přidat **přihlášení k účtu** a **správu účtů** protokoly v místních zásad auditu. Pokud konfigurujete zásady auditu pokročilé, ujistěte se, že chcete vynutit [podkategorie zásad auditu](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/audit-force-audit-policy-subcategory-settings-to-override).

7. Po použití pomocí objektu zásad skupiny, nové události jsou viditelné v rámci vaší **protokoly událostí Windows**.

## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
