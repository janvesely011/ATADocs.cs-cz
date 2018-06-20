---
title: Vyloučení entity z detekce v Azure Advanced Threat Protection | Microsoft Docs
description: Popisuje zastavení Azure ATP z konkrétní entitu aktivitám v podobě podezřelé zjišťování
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 60a2fae0ef044993786fb3b7e2d21a3ac27bb9f0
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446026"
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="excluding-entities-from-detections"></a>Vyloučení entit z detekce
Tento článek vysvětluje, jak z aktivován výstrahy, aby bylo možné minimalizovat true neškodné pozitivních, ale ve stejnou dobu, zkontrolujte, zda že catch true pozitivních vyloučit entity. Chcete-li zachovat Azure ATP nebudou aktivní o aktivitách, které z konkrétní uživatele, může být součástí vašeho normální tempo, jakým firmy, můžete quiet – nebo vyloučit - konkrétní entity z vyvolání výstrahy.

Pokud máte například kontrolu zabezpečení, která provádí rekognoskaci DNS, nebo správce, který spouští na dálku skripty na řadiči domény – a jedná se o schválené aktivity, které se provádí jako součást běžného provozu IT ve vaší organizaci. Další informace o zjištění Azure ATP vám pomohou rozhodnout entit, které chcete vyloučit, najdete v článku [Průvodce podezřelé aktivity](suspicious-activity-guide.md).

Chcete-li vyloučit entity z vyvolání výstrahy v Azure ATP:

Existují dva způsoby, jak vyloučit entity – v rámci samotné podezřelé aktivity nebo na kartě **Exclusions** (Vyloučení) na stránce **Configuration** (Konfigurace).

- **Z podezřelé aktivity**: V podezřelé aktivity časová osa, když obdrží výstrahu u aktivit pro uživatele nebo počítače nebo IP adresu, která může provádět konkrétní aktivity a může provádět tak často, klikněte pravým tlačítkem na tři tečky na konci řádku pro podezřelé aktivity na tuto entitu a vyberte **zavřete a vyloučení**. <br></br>Tím přidáte uživatele, počítače nebo IP adresu do seznamu vyloučení pro podezřelé aktivity. Toto okno zavře podezřelé aktivity a je už uvedené v **otevřete** události seznamu v **časová osa podezřelých aktivit**.

    ![Vyloučení entity](./media/exclude-in-sa.png)

- **Na stránce konfigurace**: můžete zkontrolovat nebo změnit jakékoli vyloučení: v části **konfigurace**, klikněte na tlačítko **vyloučení** a pak vyberte podezřelé aktivity, jako například **DNS rekognoskace**.

    ![Konfigurace vyloučení](./media/exclusions.png)

Chcete-li přidat entitu z **vyloučení** konfigurace: Zadejte název entity a potom klikněte na tlačítko plus a pak klikněte na tlačítko **Uložit** v dolní části stránky.

Pokud chcete odebrat entitu z konfigurace **Exclusions** (Vyloučení): Klikněte na minus vedle názvu entity a potom klikněte na **Save** (Uložit) v dolní části stránky.

Doporučujeme přidat vyloučení k detekcím až po přijetí upozornění na typ a určení, že se jedná o neškodnou pravdivě pozitivní aktivitu. 

> [!NOTE]
> Abychom vás ochránili, není možné nastavit vyloučení u všech detekcí. 

U některých detekcí jsou k dispozici tipy, které vám pomohou se rozhodnout, co chcete vyloučit. 

Každý vyloučení závisí na kontextu, v některých můžete nastavit uživatelé, zatímco ostatní uživatelé můžete nastavit počítače nebo IP adresy. 

Až budete mít možnost vyloučit IP adresu nebo počítač, můžete vyloučit jeden z nich - nemusíte zadat obě.

> [!NOTE]
> Konfigurační stránky lze upravit pouze správci Azure ATP.


## <a name="see-also"></a>Viz také

- [Integrace s programem Windows Defender ATP](integrate-wd-atp.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)