---
title: Azure Advanced Threat Protection role skupin pro správu přístupu | Dokumentace Microsoftu
description: Provede vás práce se skupinami rolí služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/07/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7ae3f0adca3137664f0a89c15e8feee71d0cd915
ms.sourcegitcommit: c4978be196e0039c7a5d5887bec4cbc5c01d64f9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/07/2018
ms.locfileid: "48848609"
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

Ochrana ATP v programu Azure nabízí tři typy skupin zabezpečení: ochrana ATP v programu Azure *(název pracovního prostoru)* Administrators, ochrana ATP v programu Azure *(název pracovního prostoru)* uživatele a služby Azure ATP *(název pracovního prostoru)* Prohlížeče. Následující tabulka popisuje typ přístupu na portálu ochrany ATP v programu Azure k dispozici pro jednotlivé role. V závislosti na roli, které přiřadíte, různé obrazovky a možnosti nabídky v ochrany ATP v programu Azure portal nejsou k dispozici pro uživatele, následujícím způsobem:

|Aktivita |Ochrana ATP v programu Azure *(název pracovního prostoru)* správci|Ochrana ATP v programu Azure *(název pracovního prostoru)* uživatelů|Ochrana ATP v programu Azure *(název pracovního prostoru)* prohlížeče|
|----|----|----|----|
|Přihlášení|K dispozici|K dispozici|K dispozici|
|Změna stavu výstrah zabezpečení (potlačení znovu otevřete, zavřete, vyloučení)|K dispozici|K dispozici|Není k dispozici|
|Sdílení a Export výstrahy zabezpečení (e-mailem, získejte odkaz, stáhněte si podrobnosti)|K dispozici|K dispozici|K dispozici|
|Stažení sestavy|K dispozici|K dispozici|K dispozici|
|Změna stavu výstrah monitorování|K dispozici|Není k dispozici|Není k dispozici|
|Aktualizace konfigurace ochrany ATP v programu Azure - senzorů (stáhnout, znovu vygenerovat klíč, konfigurace a odstranění)|K dispozici|Není k dispozici|Není k dispozici|
|Aktualizace konfigurace Azure ATP – zdroje dat (adresářové služby, SIEM, VPN WD – ochrana ATP v programu)|K dispozici|Není k dispozici|Není k dispozici|
|Aktualizace konfigurace ochrany ATP v programu –|K dispozici|Není k dispozici|Není k dispozici|
|Aktualizace konfigurace ochrany ATP v programu-Naplánované sestavy|K dispozici|K dispozici|Není k dispozici|
|Aktualizace konfigurace ochrany ATP v programu – značky entit (citlivé a honeytoken)|K dispozici|K dispozici|Není k dispozici|
|Aktualizace konfigurace ochrany ATP v programu-vyloučení|K dispozici|K dispozici|Není k dispozici|
|Aktualizace konfigurace ochrany ATP v programu – jazyk|K dispozici|K dispozici|Není k dispozici|
|Aktualizace konfigurace ochrany ATP v programu – upozornění (e-mailu a syslog)|K dispozici|K dispozici|Není k dispozici|
|Aktualizace konfigurace ochrany ATP v programu – ve verzi Preview detekce|K dispozici|K dispozici|Není k dispozici|
|Zobrazit výstrahy zabezpečení a profily entit|K dispozici|K dispozici|K dispozici|


Uživatelé se pokusí otevřít stránku, která není k dispozici pro jejich skupinu rolí, je přesměrován na stránku neoprávněné ochrany ATP v programu Azure. 

## <a name="add-and-remove-users"></a>Přidávat a odebírat uživatele 


Ochrana ATP v programu Azure používá skupiny zabezpečení Azure AD jako základ pro skupiny rolí. Skupiny rolí je možné spravovat z [ https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups ](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups). Uživatelé pouze Azure AD můžete přidat nebo odebrat ze skupiny zabezpečení. 

## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti ochrany ATP v programu](http://aka.ms/aatpsizingtool)
- [Architektura ochrany ATP v programu](atp-architecture.md)
- [Instalace služby Azure ATP](install-atp-step1.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

