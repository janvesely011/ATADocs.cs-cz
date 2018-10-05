---
title: Azure Advanced Threat Protection role skupin pro správu přístupu | Dokumentace Microsoftu
description: Provede vás práce se skupinami rolí služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2a5bc4ca940eef36911480b821e99b46749e1379
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783606"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*




# <a name="azure-atp-role-groups"></a>Skupiny rolí Azure ATP

Ochrana ATP v programu Azure nabízí zabezpečení na základě rolí na trhu při ochraně dat podle konkrétního zabezpečení a dodržování předpisů v organizaci. Ochrana ATP v programu Azure podporují tři samostatné role: správci, uživatelé a čtenáři. 

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Skupiny rolí umožňují správu přístupu pro služby Azure ATP. Pomocí skupin rolí můžete oddělit úlohy v rámci týmu zabezpečení a udělit přístup pouze v takovém rozsahu, který uživatelé potřebují ke své práci. Tento článek vysvětluje správu přístupu, ochrany ATP v programu Azure autorizaci rolí a pomůže vám začít pracovat se skupinami rolí v Azure ATP.

> [!NOTE]
> Všechny globální správce nebo správce zabezpečení do vašeho tenanta Azure Active Directory je automaticky správcem služby Azure ATP.

## <a name="accessing-the-azure-atp-portal"></a>Přístup k portálu služby Azure ATP

Přístup k portálu ochrany ATP v programu Azure (portal.atp.azure.com) můžete provést pouze uživatele Azure AD, který má role adresáře globální správce nebo správce zabezpečení. Po zadání na portálu, můžete vytvořit pracovní prostor. Služba Ochrana ATP v programu Azure vytvoří tři skupiny zabezpečení ve vašem tenantovi Azure Active Directory: správci, uživatelé, prohlížeče. 

> [!NOTE]
> Přístup k portálu ochrany ATP v programu Azure poskytována pouze pro uživatele v rámci skupiny zabezpečení služby Azure ATP v rámci Azure Active Directory a globální správci a správci zabezpečení nástroje klienta.


## <a name="types-of-azure-atp-security-groups"></a>Typy skupin zabezpečení služby Azure ATP 

Zavádí tři typy skupiny zabezpečení, ochrany ATP v programu Azure: ochrana ATP v programu Azure *(název pracovního prostoru)* Administrators, ochrana ATP v programu Azure *(název pracovního prostoru)* uživatele a služby Azure ATP *(název pracovního prostoru)* Prohlížeče. Následující tabulka popisuje typ přístupu na portálu ochrany ATP v programu Azure pro každou roli k dispozici. V závislosti na jakou roli můžete přiřadit různé obrazovky a možnosti nabídky v ochrany ATP v programu Azure portal nejsou k dispozici, následujícím způsobem:

|Aktivita |Ochrana ATP v programu Azure *(název pracovního prostoru)* správci|Ochrana ATP v programu Azure *(název pracovního prostoru)* uživatelů|Ochrana ATP v programu Azure *(název pracovního prostoru)* prohlížeče|
|----|----|----|----|
|Přihlášení|K dispozici|K dispozici|K dispozici|
|Změna stavu výstrah zabezpečení|K dispozici|K dispozici|Není k dispozici|
|Sdílení a Export výstrahy zabezpečení prostřednictvím e-mailu nebo odkazu|K dispozici|K dispozici|K dispozici|
|Změna stavu výstrah monitorování|K dispozici|Není k dispozici|Není k dispozici|
|Aktualizace konfigurace ochrany ATP v programu Azure|K dispozici|Není k dispozici|Není k dispozici|
|Snímač – přidat|K dispozici|Není k dispozici|Není k dispozici|
|Snímač – odstranit |K dispozici|Není k dispozici|Není k dispozici|
|Monitorované DC – přidání |K dispozici|Není k dispozici|Není k dispozici|
|Monitorované DC – odstranění|K dispozici|Není k dispozici|Není k dispozici|
|Zobrazení výstrah a výstrahy zabezpečení|K dispozici|K dispozici|K dispozici|


Uživatelé se pokusí otevřít stránku, která není k dispozici pro jejich skupinu rolí, je přesměrován na stránku neoprávněné ochrany ATP v programu Azure. 

## <a name="add-and-remove-users"></a>Přidávat a odebírat uživatele 


Ochrana ATP v programu Azure používá skupiny zabezpečení Azure AD jako základ pro skupiny rolí. Skupiny rolí je možné spravovat z [ https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups ](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups). Uživatelé pouze Azure AD můžete přidat nebo odebrat ze skupiny zabezpečení. 

## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti ochrany ATP v programu](http://aka.ms/aatpsizingtool)
- [Architektura ochrany ATP v programu](atp-architecture.md)
- [Instalace služby Azure ATP](install-atp-step1.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

