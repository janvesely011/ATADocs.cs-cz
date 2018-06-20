---
title: Azure Advanced Threat Protection role skupiny pro správu přístupu | Microsoft Docs
description: Vás provede procesem práce se skupinami role Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 77a2464634b4286d2f6d35504e9ab7512cf7b612
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/22/2018
ms.locfileid: "34444769"
---
*Platí pro: Azure Advanced Threat Protection*




# <a name="azure-atp-role-groups"></a>Azure skupin rolí ATP

Azure ATP nabízí na základě rolí zabezpečení k ochraně dat podle potřeb konkrétní zabezpečení a dodržování předpisů v organizaci. Azure ATP podporují tři samostatné role: správci, uživatelů a prohlížeče. 

> [!NOTE]
> Pokud vás zajímá zobrazení nebo odstranění osobních údajů, přečtěte si pokyny společnosti Microsoft v [správce dodržování předpisů Microsoft](https://servicetrust.microsoft.com/ComplianceManager) a v [GDPR části webu Microsoft 365 Enterprise dodržování předpisů](https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr). Pokud hledáte obecné informace o GDPR, přečtěte si téma [GDPR části portálu služby důvěřovat](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

Role skupiny umožňují správu přístupu k Azure ATP. Pomocí skupin rolí můžete oddělit úlohy v rámci týmu zabezpečení a udělit přístup pouze v takovém rozsahu, který uživatelé potřebují ke své práci. Tento článek vysvětluje správu přístupu a autorizace Azure ATP role a pomáhá získat spuštěná pomocí skupin rolí v ATP.

> [!NOTE]
> Všechny globální správce nebo správce zabezpečení na klienta Azure Active Directory je automaticky správce Azure ATP.

## <a name="accessing-the-workspace-management-portal"></a>Přístup k portálu pro správu pracovního prostoru

Přístup k portálu pro správu prostoru (portal.atp.azure.com) můžete provést pouze uživatele Azure AD, který má roli adresáře globální správce nebo správce zabezpečení. Po zadání portálu, můžete vytvořit jiný pracovní prostory. Pro každý pracovní prostor služby Azure ATP vytvoří tři skupiny zabezpečení v klientovi služby Azure Active Directory: správci, uživatelé, prohlížečů. 

> [!NOTE]
> Přístup k portálu Azure ATP pracovního prostoru je udělit pouze pro uživatele v rámci skupiny zabezpečení Azure AD pro tento pracovní prostor a globální správci a správci zabezpečení.


## <a name="types-of-azure-atp-security-groups"></a>Typy skupin zabezpečení Azure ATP 

Azure ATP zavádí tři typy skupiny zabezpečení: Azure ATP *název pracovního prostoru* správců, Azure ATP *název pracovního prostoru* uživatelů a Azure ATP *název pracovního prostoru* prohlížečů . Následující tabulka popisuje typ přístupu na portálu Azure ATP prostoru k dispozici na roli. Podle toho, jakou roli přiřadíte, různé obrazovky a možnosti nabídky v Azure ATP prostoru portál nejsou k dispozici, následujícím způsobem:

|Aktivita |Azure ATP *název pracovního prostoru* správci|Azure ATP *název pracovního prostoru* uživatelů|Azure ATP *název pracovního prostoru* prohlížečů|
|----|----|----|----|
|Přihlášení|K dispozici|K dispozici|K dispozici|
|Změna stavu podezřelé aktivity|K dispozici|K dispozici|Není k dispozici|
|Sdílení a export podezřelé aktivity prostřednictvím e-mailu nebo odkazu|K dispozici|K dispozici|K dispozici|
|Změna stavu výstrah monitorování|K dispozici|Není k dispozici|Není k dispozici|
|Aktualizace konfigurace Azure ATP|K dispozici|Není k dispozici|Není k dispozici|
|senzor – přidat|K dispozici|Není k dispozici|Není k dispozici|
|senzor – odstranit |K dispozici|Není k dispozici|Není k dispozici|
|Monitorované DC – přidání |K dispozici|Není k dispozici|Není k dispozici|
|Monitorované DC – odstranění|K dispozici|Není k dispozici|Není k dispozici|
|Zobrazení výstrah a podezřelých aktivit|K dispozici|K dispozici|K dispozici|


Uživatelé se pokusí přistoupit ke stránce, která není k dispozici pro jejich role skupiny, je přesměrován na stránku neoprávněným Azure ATP. 

## <a name="add-and-remove-users"></a>Přidání a odebrání uživatelů 

Azure ATP používá skupiny zabezpečení Azure AD jako základ pro skupin rolí. Skupin rolí lze spravovat z [ https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All skupiny](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All groups).  Pouze AAD uživatele můžete přidat nebo odebrat ze skupiny zabezpečení. 


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti ATA](http://aka.ms/aatpsizingtool)
- [Architektura ATA](atp-architecture.md)
- [Instalace ATA](install-atp-step1.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)

