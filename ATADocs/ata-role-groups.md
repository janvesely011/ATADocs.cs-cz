---
title: "Skupiny rolí Advanced Threat Analytics pro správu přístupu | Dokumentace Microsoftu"
description: "Provede vás prací se skupinami rolí ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/16/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1f531db341f442d135b802af965f714b37f69e3a
ms.sourcegitcommit: 3cd268cf353ff8bc3d0b8f9a8c10a34353d1fcf1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/16/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*




# <a name="ata-role-groups"></a>Skupiny rolí ATA

Skupiny rolí umožňují správu přístupu pro ATA. Pomocí skupin rolí můžete oddělit úlohy v rámci týmu zabezpečení a udělit přístup pouze v takovém rozsahu, který uživatelé potřebují ke své práci. Tento článek vysvětluje správu přístupu a autorizaci rolí ATA a ulehčí vám uvedení skupin rolí v ATA co nejdříve do provozu.

> [!NOTE]
> Každý místní správce v komponentě ATA Center je automaticky správcem Microsoft Advanced Threat Analytics.

## <a name="types-of-ata-role-groups"></a>Typy skupin rolí ATA 

ATA zavádí 3 typy skupin rolí: Správci ATA, uživatelé ATA a čtenáři ATA. Následující tabulka popisuje typ přístupu v ATA, který je dostupný pro určitou roli. V závislosti na přiřazené roli budou v ATA k dispozici různé obrazovky a možnosti nabídky, a to následovně:

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


Když se uživatelé pokusí získat přístup na stránku, která pro jejich skupinu rolí není k dispozici, budou přesměrováni na stránku ATA pro neoprávněné uživatele. 

## <a name="add--remove-users---ata-role-groups"></a>Přidávání a odebírání uživatelů – skupiny rolí ATA 

ATA jako základ pro skupiny rolí používá místní skupiny systému Windows. Skupiny rolí je třeba spravovat na serveru ATA Center.
Když chcete přidat nebo odebrat uživatele, použijte konzolu MCC **Místní uživatelé a skupiny** (Lusrmgr.msc). V počítači připojeném k doméně je možné přidávat účty domény i místní účty. 

