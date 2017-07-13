---
title: "Skupiny rolí Advanced Threat Analytics pro správu přístupu | Dokumentace Microsoftu"
description: "Provede vás prací se skupinami rolí ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/13/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3715b69e-e631-449b-9aed-144d0f9bcee7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1afb8e728fa359721d78833f8220cae3f65bd896
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/30/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*




# Skupiny rolí ATA
<a id="ata-role-groups" class="xliff"></a>

Skupiny rolí umožňují správu přístupu pro ATA. Pomocí skupin rolí můžete oddělit úlohy v rámci týmu zabezpečení a udělit přístup pouze v takovém rozsahu, který uživatelé potřebují ke své práci. Tento článek vysvětluje správu přístupu a autorizaci rolí ATA a ulehčí vám uvedení skupin rolí v ATA co nejdříve do provozu.

> [!NOTE]
> Každý místní správce v komponentě ATA Center je automaticky správcem Microsoft Advanced Threat Analytics.

## Typy skupin rolí ATA
<a id="types-of-ata-role-groups" class="xliff"></a> 

ATA zavádí 3 typy skupin rolí: Správci ATA, uživatelé ATA a čtenáři ATA. Následující tabulka popisuje typ přístupu v ATA, který je dostupný pro určitou roli. V závislosti na přiřazené roli budou v ATA k dispozici různé obrazovky a možnosti nabídky, a to následovně:

|Aktivita |Správci Microsoft Advanced Threat Analytics|Uživatelé Microsoft Advanced Threat Analytics|Čtenáři Microsoft Advanced Threat Analytics|
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
|Zobrazení výstrah a podezřelých aktivit|K dispozici|K dispozici|K dispozici|


Když se uživatelé pokusí získat přístup na stránku, která pro jejich skupinu rolí není k dispozici, budou přesměrováni na stránku ATA pro neoprávněné uživatele. 

## Přidávání a odebírání uživatelů – skupiny rolí ATA
<a id="add--remove-users---ata-role-groups" class="xliff"></a> 

ATA jako základ pro skupiny rolí používá místní skupiny systému Windows. Skupiny rolí je třeba spravovat na serveru ATA Center.
Když chcete přidat nebo odebrat uživatele, použijte konzolu MCC **Místní uživatelé a skupiny** (Lusrmgr.msc). V počítači připojeném k doméně je možné přidávat účty domény i místní účty. 

