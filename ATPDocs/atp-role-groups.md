---
title: Azure Advanced Threat Protection role skupin pro správu přístupu | Dokumentace Microsoftu
description: Provede vás práce se skupinami rolí služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 11/29/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 25901bada4175cf019f886b5739aa1b5ab0e3fe1
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077265"
---
# <a name="azure-atp-role-groups"></a>Skupiny rolí Azure ATP

Ochrana ATP v programu Azure nabízí zabezpečení na základě rolí na trhu při ochraně dat podle konkrétního zabezpečení a dodržování předpisů v organizaci. Ochrana ATP v programu Azure podporují tři samostatné role: Správci, uživatelé a čtenáři. 

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Skupiny rolí umožňují správu přístupu pro služby Azure ATP. Pomocí skupin rolí můžete oddělit úlohy v rámci týmu zabezpečení a udělit přístup pouze v takovém rozsahu, který uživatelé potřebují ke své práci. Tento článek vysvětluje správu přístupu, ochrany ATP v programu Azure autorizaci rolí a pomůže vám začít pracovat se skupinami rolí v Azure ATP.

> [!NOTE]
> Všechny globální správce nebo správce zabezpečení do vašeho tenanta Azure Active Directory je automaticky správcem služby Azure ATP.

## <a name="accessing-the-azure-atp-portal"></a>Přístup k portálu služby Azure ATP

Přístup k portálu ochrany ATP v programu Azure (portal.atp.azure.com) můžete provést pouze uživatele Azure AD, který má role adresáře globální správce nebo správce zabezpečení. Jakmile zadáte portál, požadované role, můžete vytvořit instanci služby Azure ATP. Služba Ochrana ATP v programu Azure vytvoří tři skupiny zabezpečení ve vašem tenantovi Azure Active Directory: Správci, uživatelé, prohlížeče. 

> [!NOTE]
> Přístup k portálu ochrany ATP v programu Azure poskytována pouze pro uživatele ve skupinách zabezpečení služby Azure ATP v rámci služby Azure Active Directory, stejně jako globální a zabezpečení Správci klienta.


## <a name="types-of-azure-atp-security-groups"></a>Typy skupin zabezpečení služby Azure ATP 

Ochrana ATP v programu Azure nabízí tři typy skupin zabezpečení: Ochrana ATP v programu Azure *(název instance)* Administrators, ochrana ATP v programu Azure *(název instance)* uživatele a služby Azure ATP *(název instance)* prohlížeče. Následující tabulka popisuje typ přístupu na portálu ochrany ATP v programu Azure k dispozici pro jednotlivé role. V závislosti na roli, které přiřadíte, různé obrazovky a možnosti nabídky v ochrany ATP v programu Azure portal nejsou k dispozici pro uživatele, následujícím způsobem:

|Aktivita |Ochrana ATP v programu Azure *(název instance)* správci|Ochrana ATP v programu Azure *(název instance)* uživatelů|Ochrana ATP v programu Azure *(název instance)* prohlížeče|
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

