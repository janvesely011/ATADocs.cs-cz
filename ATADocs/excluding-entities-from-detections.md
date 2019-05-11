---
title: Vyloučení entit z detekce ve službě Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje, jak ve službě ATA zastavit zjišťování aktivit konkrétních entit jako podezřelých
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 41f7d2e17d45e931c9472df2225f46f460f03a95
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65195638"
---
# <a name="excluding-entities-from-detections"></a>Vyloučení entit z detekce

*Platí pro: Advanced Threat Analytics verze 1.9*

Tento článek vysvětluje, jak vyloučení entit, která aktivuje upozornění, pokud chcete minimalizovat neškodné pravdivě pozitivní, ale ve stejnou dobu, ujistěte se, že při zachycení pravdivě pozitivní. Aby služba ATA nebudou hlučného o aktivitách, které určitých uživatelů, může být součástí vaší běžné podnikové činnosti, můžete potlačit – nebo vyloučit – konkrétní entity nemají vyvolávat výstrahy.

Pokud máte například kontrolu zabezpečení, která provádí rekognoskaci DNS, nebo správce, který spouští na dálku skripty na řadiči domény – a jedná se o schválené aktivity, které se provádí jako součást běžného provozu IT ve vaší organizaci.

Vyloučení entit, které nemají vyvolávat výstrahy v rámci služby ATA:

Existují dva způsoby, jak vyloučit entity – v rámci samotné podezřelé aktivity nebo na kartě **Exclusions** (Vyloučení) na stránce **Configuration** (Konfigurace).

- **V rámci podezřelé aktivity**: V rámci podezřelé aktivity časové osy, když obdržíte výstrahu týkající se aktivity uživatele nebo počítače nebo IP adresu, kterou může určitou aktivitu a může se tak často, klikněte pravým tlačítkem na tři tečky na konci řádku podezřelé aktivity th v entitě a vyberte **zavřít a vyloučit**. <br></br>Tím přidáte uživatele, počítače nebo IP adresu do seznamu vyloučení pro podezřelé aktivity. Zavře podezřelé aktivity a už nejsou uvedení v **otevřít** v seznamu událostí **časová osa podezřelých aktivit**.

    ![Vyloučení entity](./media/exclude-in-sa.png)

- **Na stránce konfigurace**:  Kontrola nebo úprava jakékoli vyloučení: v části **konfigurace**, klikněte na tlačítko **vyloučení** a pak vyberte podezřelou aktivitu, jako je například **k citlivým účtům pověření**.

    ![Konfigurace vyloučení](./media/exclusions-config-page.png)

Pokud chcete odebrat entitu z konfigurace **Exclusions** (Vyloučení): Klikněte na minus vedle názvu entity a potom klikněte na **Save** (Uložit) v dolní části stránky.

Doporučujeme přidat vyloučení k detekcím až po přijetí upozornění na typ a určení, že se jedná o neškodnou pravdivě pozitivní aktivitu. 

> [!NOTE]
> Abychom vás ochránili, není možné nastavit vyloučení u všech detekcí. 

U některých detekcí jsou k dispozici tipy, které vám pomohou se rozhodnout, co chcete vyloučit. 

Každé vyloučení závisí na kontextu, v některých můžete nastavit uživatele a pro ostatní uživatele můžete nastavit počítače nebo IP adresy. 

Až budete mít možnost vyloučit IP adresu nebo počítač, můžete vyloučit jednu z nich – nemusíte zadávat obě dvě.

> [!NOTE]
> Konfigurační stránky můžou upravovat jenom správci ATA.


## <a name="see-also"></a>Viz také
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Změna konfigurace ATA](modifying-ata-center-configuration.md)
