---
title: Skupiny rolí Advanced Threat Analytics pro správu přístupu | Dokumentace Microsoftu
description: Provede vás prací se skupinami rolí ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ed4d112cda614053aa20a6a486cb29baa1fed58a
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133629"
---
*Platí pro: Advanced Threat Analytics verze 1.9*




# <a name="ata-role-groups"></a>Skupiny rolí ATA

Skupiny rolí umožňují správu přístupu pro ATA. Pomocí skupin rolí můžete oddělit úlohy v rámci týmu zabezpečení a udělit přístup pouze v takovém rozsahu, který uživatelé potřebují ke své práci. Tento článek vysvětluje správu přístupu a autorizaci rolí ATA a ulehčí vám uvedení skupin rolí v ATA co nejdříve do provozu.

> [!NOTE]
> Každý místní správce v komponentě ATA Center je automaticky správcem Microsoft Advanced Threat Analytics.

## <a name="types-of-ata-role-groups"></a>Typy skupin rolí ATA 

ATA zavádí tři typy skupin rolí: Správci ATA, uživatelé ATA a čtenáři ATA. Následující tabulka popisuje typ přístupu v ATA, který je dostupný pro určitou roli. V závislosti na roli, které můžete přiřadit různé obrazovky a nabídky Možnosti v ATA nejsou k dispozici, následujícím způsobem:

|Aktivita |Správci Microsoft Advanced Threat Analytics|Uživatelé Microsoft Advanced Threat Analytics|Čtenáři Microsoft Advanced Threat Analytics|
|----|----|----|----|
|Přihlášení|K dispozici|K dispozici|K dispozici|
|Poskytnutí vstupu k podezřelým aktivitám|K dispozici|K dispozici|Není k dispozici|
|Změna stavu podezřelé aktivity|K dispozici|K dispozici|Není k dispozici|
|Sdílení a export podezřelé aktivity prostřednictvím e-mailu nebo odkazu|K dispozici|K dispozici|Není k dispozici|
|Změna stavu výstrah monitorování|K dispozici|K dispozici|Není k dispozici|
|Aktualizace konfigurace ATA|K dispozici|Není k dispozici|Není k dispozici|
|Gateway – přidání|K dispozici|Není k dispozici|Není k dispozici|
|Gateway – odstranění |K dispozici|Není k dispozici|Není k dispozici|
|Monitorované DC – přidání |K dispozici|Není k dispozici|Není k dispozici|
|Monitorované DC – odstranění|K dispozici|Není k dispozici|Není k dispozici|
|Zobrazení výstrah a podezřelých aktivit|K dispozici|K dispozici|K dispozici|


Když se uživatelé pokusí získat přístup na stránku, která není k dispozici pro jejich skupinu rolí, bude přesměrován na stránku ATA pro neoprávněné. 

## <a name="add--remove-users---ata-role-groups"></a>Přidávání a odebírání uživatelů – skupiny rolí ATA 

ATA jako základ pro skupiny rolí používá místní skupiny systému Windows. Skupiny rolí je třeba spravovat na serveru ATA Center.
Když chcete přidat nebo odebrat uživatele, použijte konzolu MCC **Místní uživatelé a skupiny** (Lusrmgr.msc). V počítači připojeném k doméně je možné přidávat účty domény i místní účty. 

