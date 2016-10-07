---
title: "Práce se skupinami rolí – kompletní | Microsoft ATA"
description: "Provede vás prací se skupinami rolí ATA."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 869d8f830d5dc70c927f172d77642b0c97bdcd84


---

*Platí pro: Advanced Threat Analytics verze 1.7*




# Skupiny rolí ATA

Skupiny rolí umožňují správu přístupu pro ATA. Pomocí skupin rolí můžete oddělit úlohy v rámci týmu zabezpečení a udělit přístup pouze v takovém rozsahu, který uživatelé potřebují ke své práci. Tento článek vysvětluje správu přístupu a autorizaci rolí ATA a ulehčí vám uvedení skupin rolí v ATA co nejdříve do provozu.
## Typy skupin rolí ATA 

ATA zavádí 3 typy skupiny rolí: Správce ATA, Analytik ATA a Vedoucí ATA. Následující tabulka popisuje typ přístupu v ATA, který je dostupný pro určitou roli. V závislosti na přiřazené roli budou v ATA k dispozici různé obrazovky a možnosti nabídky, a to následovně:

|Aktivita |Správce Microsoft Advanced Threat Analytics|Analytik Microsoft Advanced Threat Analytics|Vedoucí Microsoft Advanced Threat Analytics|
|----|----|----|----|
|Přihlášení|K dispozici|K dispozici|K dispozici|
|Poskytnutí vstupu k podezřelým aktivitám|K dispozici|K dispozici|Není k dispozici|
|Změna stavu podezřelé aktivity|K dispozici|K dispozici|Není k dispozici|
|Sdílení a export podezřelé aktivity prostřednictvím e-mailu nebo odkazu|K dispozici|K dispozici|Není k dispozici|
|Přidávání a úprava poznámek k podezřelým aktivitám|K dispozici|K dispozici|Není k dispozici|
|Změna stavu výstrah monitorování|K dispozici|K dispozici|Není k dispozici|
|Aktualizace konfigurace ATA|K dispozici|Není k dispozici|Není k dispozici|
|Gateway – přidání|K dispozici|Není k dispozici|Není k dispozici|
|Gateway – odstranění |K dispozici|Není k dispozici|Není k dispozici|
|Monitorované DC – přidání |K dispozici|Není k dispozici|Není k dispozici|
|Monitorované DC – odstranění|K dispozici|Není k dispozici|Není k dispozici|

Když se uživatelé pokusí získat přístup na stránku, která pro jejich skupinu rolí není k dispozici, budou přesměrováni na stránku ATA pro neoprávněné uživatele. 

## Přidávání a odebírání uživatelů – skupiny rolí ATA 

ATA jako základ pro skupiny rolí používá místní skupiny systému Windows. Když chcete přidat nebo odebrat uživatele, použijte konzolu MCC **Místní uživatelé a skupiny** (Lusrmgr.msc). V počítači připojeném k doméně je možné přidávat účty domény i místní účty. 




<!--HONumber=Sep16_HO4-->


