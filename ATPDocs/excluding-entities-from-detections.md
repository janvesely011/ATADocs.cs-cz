---
title: Vyloučení entit z detekce ve službě Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Popisuje, jak zastavit zjišťování aktivit konkrétních entit jako podezřelých služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 432f55891440975e511ab5cd3e2972a1c7a33f37
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782926"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="excluding-entities-from-detections"></a>Vyloučení entit z detekce
Tento článek vysvětluje, jak vyloučit entity z aktivace za účelem minimalizace neškodné pravdivě pozitivní během provádění, je možné zachytit pravdivě pozitivní upozornění. Aby bylo možné zachovat ochrany ATP v programu Azure nebudou hlučného o aktivitách, které určitých uživatelů, může být součástí vaší běžné podnikové činnosti, můžete potlačit – nebo vyloučit – konkrétní entity nemají vyvolávat výstrahy.

Pokud máte například kontrolu zabezpečení, která provádí rekognoskaci DNS, nebo správce, který spouští na dálku skripty na řadiči domény – a jedná se o schválené aktivity, které se provádí jako součást běžného provozu IT ve vaší organizaci. Další informace o zjištění ochrany ATP v programu Azure vám pomohou rozhodnout entit, které chcete vyloučit, najdete v článku [Průvodce podezřelými aktivitami](suspicious-activity-guide.md).

Vyloučení entit z vyvolávání výstrah ve službě ochrana ATP v programu Azure:

Existují dva způsoby, jak vyloučit entity – v rámci samotné podezřelé aktivity nebo na kartě **Exclusions** (Vyloučení) na stránce **Configuration** (Konfigurace).

- **V rámci podezřelé aktivity**: V podezřelé aktivity časovou osu, když obdržíte výstrahu týkající se aktivity uživatele nebo počítače nebo IP adresu, kterou smí provádět určitou aktivitu a můžou Uděláte to tak často, klikněte pravým tlačítkem na tři tečky na konci řádku pro podezřelé aktivity dané entity a vyberte **zavřít a vyloučit**. <br></br>Tím přidáte uživatele, počítače nebo IP adresu do seznamu vyloučení pro podezřelé aktivity. Zavře podezřelé aktivity a už nejsou uvedení v **otevřít** v seznamu událostí **časová osa podezřelých aktivit**.

    ![Vyloučení entity](./media/exclude-in-sa.png)

- **Na stránce konfigurace**: Kontrola nebo úprava jakékoli vyloučení: v části **konfigurace**, klikněte na tlačítko **vyloučení** a pak vyberte podezřelou aktivitu, jako je například **DNS rekognoskace**.

    ![Konfigurace vyloučení](./media/exclusions.png)

Chcete-li přidat entitu z **vyloučení** konfigurace: Zadejte název entity a potom klikněte na tlačítko plus a potom klikněte na **Uložit** v dolní části stránky.

Pokud chcete odebrat entitu z konfigurace **Exclusions** (Vyloučení): Klikněte na minus vedle názvu entity a potom klikněte na **Save** (Uložit) v dolní části stránky.

Doporučujeme přidat vyloučení k detekcím až po přijetí upozornění na typ a určení, že se jedná o neškodnou pravdivě pozitivní aktivitu. 

> [!NOTE]
> Abychom vás ochránili, není možné nastavit vyloučení u všech detekcí. 

U některých detekcí jsou k dispozici tipy, které vám pomohou se rozhodnout, co chcete vyloučit. 

Každé vyloučení závisí na kontextu, v některých můžete nastavit uživatele a pro ostatní uživatele můžete nastavit počítače nebo IP adresy. 

Až budete mít možnost vyloučit IP adresu nebo počítač, můžete vyloučit jednu z nich – nemusíte zadávat obě dvě.

> [!NOTE]
> Konfigurační stránky můžou upravovat jenom správci služby Azure ATP.


## <a name="see-also"></a>Viz také

- [Integraci se službou ochrana ATP v programu Windows Defender](integrate-wd-atp.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)