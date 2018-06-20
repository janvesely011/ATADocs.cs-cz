---
title: Vyloučení entit z detekce ve službě Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje, jak ve službě ATA zastavit zjišťování aktivit konkrétních entit jako podezřelých
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 21b1d8a4537bb77de120dac4b2f15bc785161749
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010257"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="excluding-entities-from-detections"></a>Vyloučení entit z detekce
Tento článek vysvětluje, jak z aktivován výstrahy, aby bylo možné minimalizovat true neškodné pozitivních, ale ve stejnou dobu, zkontrolujte, zda že catch true pozitivních vyloučit entity. Chcete-li zachovat ATA nebudou aktivní o aktivitách, které z konkrétní uživatele, může být součástí vašeho normální tempo, jakým firmy, můžete quiet – nebo vyloučit - konkrétní entity z vyvolání výstrahy.

Pokud máte například kontrolu zabezpečení, která provádí rekognoskaci DNS, nebo správce, který spouští na dálku skripty na řadiči domény – a jedná se o schválené aktivity, které se provádí jako součást běžného provozu IT ve vaší organizaci.

Vyloučení entit, které nemají vyvolávat výstrahy v rámci služby ATA:

Existují dva způsoby, jak vyloučit entity – v rámci samotné podezřelé aktivity nebo na kartě **Exclusions** (Vyloučení) na stránce **Configuration** (Konfigurace).

- **Z podezřelé aktivity**: V podezřelé aktivity ose, když obdrží výstrahu u aktivit pro uživatele nebo počítače nebo IP adresu, která může provádět konkrétní aktivity a může provádět tak často, klikněte pravým tlačítkem na tři tečky na konci řádku pro podezřelé aktivity na tuto entitu a vyberte **zavřete a vyloučení**. <br></br>Tím přidáte uživatele, počítače nebo IP adresu do seznamu vyloučení pro podezřelé aktivity. Toto okno zavře podezřelé aktivity a je už uvedené v **otevřete** události seznamu v **časová osa podezřelých aktivit**.

    ![Vyloučení entity](./media/exclude-in-sa.png)

- **Na stránce konfigurace**: můžete zkontrolovat nebo změnit jakékoli vyloučení: v části **konfigurace**, klikněte na tlačítko **vyloučení** a pak vyberte podezřelé aktivity, jako například  **Zpřístupnění citlivých účtů přihlašovací údaje jsou zveřejněné**.

    ![Konfigurace vyloučení](./media/exclusions-config-page.png)

Pokud chcete odebrat entitu z konfigurace **Exclusions** (Vyloučení): Klikněte na minus vedle názvu entity a potom klikněte na **Save** (Uložit) v dolní části stránky.

Doporučujeme přidat vyloučení k detekcím až po přijetí upozornění na typ a určení, že se jedná o neškodnou pravdivě pozitivní aktivitu. 

> [!NOTE]
> Abychom vás ochránili, není možné nastavit vyloučení u všech detekcí. 

U některých detekcí jsou k dispozici tipy, které vám pomohou se rozhodnout, co chcete vyloučit. 

Každý vyloučení závisí na kontextu, v některých můžete nastavit uživatelé, zatímco ostatní uživatelé můžete nastavit počítače nebo IP adresy. 

Až budete mít možnost vyloučit IP adresu nebo počítač, můžete vyloučit jeden z nich - nemusíte zadat obě.

> [!NOTE]
> Konfigurační stránky můžou upravovat jenom správci ATA.


## <a name="see-also"></a>Viz také
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Změna konfigurace ATA](modifying-ata-center-configuration.md)
