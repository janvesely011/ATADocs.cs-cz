---
title: Vyloučení entit z detekce ve službě Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje, jak ve službě ATA zastavit zjišťování aktivit konkrétních entit jako podezřelých
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e15a4ab34b0389b2c69d8cdf2e5ac04771a24fc9
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165775"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="excluding-entities-from-detections"></a>Vyloučení entit z detekce
Tento článek vysvětluje, jak vyloučení entit, která aktivuje upozornění, pokud chcete minimalizovat neškodné pravdivě pozitivní, ale ve stejnou dobu, ujistěte se, že při zachycení pravdivě pozitivní. Aby služba ATA nebudou hlučného o aktivitách, které určitých uživatelů, může být součástí vaší běžné podnikové činnosti, můžete potlačit – nebo vyloučit – konkrétní entity nemají vyvolávat výstrahy.

Pokud máte například kontrolu zabezpečení, která provádí rekognoskaci DNS, nebo správce, který spouští na dálku skripty na řadiči domény – a jedná se o schválené aktivity, které se provádí jako součást běžného provozu IT ve vaší organizaci.

Vyloučení entit, které nemají vyvolávat výstrahy v rámci služby ATA:

Existují dva způsoby, jak vyloučit entity – v rámci samotné podezřelé aktivity nebo na kartě **Exclusions** (Vyloučení) na stránce **Configuration** (Konfigurace).

- **V rámci podezřelé aktivity**: V časové ose podezřelé aktivity, když obdržíte výstrahu týkající se aktivity uživatele nebo počítače nebo IP adresu, kterou smí provádět určitou aktivitu a můžou Uděláte to tak často, klikněte pravým tlačítkem na tři tečky na konci řádku pro podezřelé aktivity dané entity a vyberte **zavřít a vyloučit**. <br></br>Tím přidáte uživatele, počítače nebo IP adresu do seznamu vyloučení pro podezřelé aktivity. Zavře podezřelé aktivity a už nejsou uvedení v **otevřít** v seznamu událostí **časová osa podezřelých aktivit**.

    ![Vyloučení entity](./media/exclude-in-sa.png)

- **Na stránce konfigurace**: Kontrola nebo úprava jakékoli vyloučení: v části **konfigurace**, klikněte na tlačítko **vyloučení** a pak vyberte podezřelou aktivitu, jako je například  **Přihlašovací údaje k účtu vystavený**.

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
