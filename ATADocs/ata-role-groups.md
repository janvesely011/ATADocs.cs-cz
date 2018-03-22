---
title: "Skupiny rolí Advanced Threat Analytics pro správu přístupu | Dokumentace Microsoftu"
description: "Provede vás prací se skupinami rolí ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3fdee9a98adaaacfa354a4ce95ad45c12b9be548
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/22/2018
---
*Platí pro: Advanced Threat Analytics verze 1.9*




# <a name="ata-role-groups"></a>Skupiny rolí ATA

Role skupiny umožňují správu přístupu k ATA. Pomocí skupin rolí můžete oddělit úlohy v rámci týmu zabezpečení a udělit přístup pouze v takovém rozsahu, který uživatelé potřebují ke své práci. Tento článek vysvětluje správu přístupu a autorizaci rolí ATA a ulehčí vám uvedení skupin rolí v ATA co nejdříve do provozu.

> [!NOTE]
> Každý místní správce v komponentě ATA Center je automaticky správcem Microsoft Advanced Threat Analytics.

## <a name="types-of-ata-role-groups"></a>Typy skupin rolí ATA 

ATA zavádí tři typy Role skupiny: Správci ATA, ATA uživatelů a prohlížeče ATA. Následující tabulka popisuje typ přístupu v ATA, který je dostupný pro určitou roli. Podle toho, jakou roli můžete přiřadit různé obrazovky a nabídce Možnosti v ATA nejsou k dispozici, následujícím způsobem:

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


Uživatelé se pokusí přistoupit ke stránce, která není k dispozici pro jejich role skupiny, je přesměrován na stránku neoprávněným ATA. 

## <a name="add--remove-users---ata-role-groups"></a>Přidávání a odebírání uživatelů – skupiny rolí ATA 

ATA jako základ pro skupiny rolí používá místní skupiny systému Windows. Skupiny rolí je třeba spravovat na serveru ATA Center.
Když chcete přidat nebo odebrat uživatele, použijte konzolu MCC **Místní uživatelé a skupiny** (Lusrmgr.msc). V počítači připojeném k doméně je možné přidávat účty domény i místní účty. 

