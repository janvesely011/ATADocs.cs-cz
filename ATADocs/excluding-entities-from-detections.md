---
title: "Vyloučení entit z detekce ve službě Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Popisuje, jak ve službě ATA zastavit zjišťování aktivit konkrétních entit jako podezřelých"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 344c0f33-45e1-42e2-a051-f722a4504531
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c185060a4fb889121c6a02b353fb0d176f0c9274
ms.sourcegitcommit: e2cb3af9c1dbb0b75946dc70cc439b19d654541c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/06/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="excluding-entities-from-detections"></a>Vyloučení entit z detekce
Toto téma vysvětluje, jak vyloučit u entit spouštění výstrah, aby bylo možné minimalizovat počty neškodných pravdivě pozitivních aktivit a současně zachytit aktivity pravdivě pozitivní. Aby služba ATA zbytečně neupozorňovala na aktivity určitých uživatelů, které můžou být součástí vaší běžné podnikové činnosti, můžete určité entity potlačit – nebo vyloučit – abyste na jejich aktivity nedostávali upozornění.

Pokud máte například kontrolu zabezpečení, která provádí rekognoskaci DNS, nebo správce, který spouští na dálku skripty na řadiči domény – a jedná se o schválené aktivity, které se provádí jako součást běžného provozu IT ve vaší organizaci.

Vyloučení entit, které nemají vyvolávat výstrahy v rámci služby ATA:

Existují dva způsoby, jak vyloučit entity – v rámci samotné podezřelé aktivity nebo na kartě **Exclusions** (Vyloučení) na stránce **Configuration** (Konfigurace).

- **V rámci podezřelé aktivity**: Na časové ose podezřelé aktivity, když obdržíte výstrahu týkající se aktivity uživatele nebo počítače nebo IP adresy, která má povolenou určitou aktivitu a může ji provádět často, klikněte pravým tlačítkem myši na tři tečky na konci řádku podezřelé aktivity dané entity a zvolte **Close and exclude** (Zavřít a vyloučit). <br></br>Uživatel, počítač nebo IP adresa se pak přidají do seznamu vyloučení pro danou podezřelou aktivitu. Zavře se také podezřelá aktivita a nebude se už dál uvádět v seznamu **otevřených** událostí v části **Suspicious activity timeline** (Časová osa podezřelých aktivit).

    ![Vyloučení entity](./media/exclude-in-sa.png)

- **Na stránce Configuration (Konfigurace)**: Kontrola nebo úprava všech nastavených vyloučení: V části **Configuration** klikněte na **Exclusions** (Vyloučení) a pak vyberte podezřelou aktivitu, jako je například **Sensitive account credentials exposed** (Zveřejnění důvěrných přihlašovacích údajů k účtu).

    ![Konfigurace vyloučení](./media/exclusions-config-page.png)

Pokud chcete odebrat entitu z konfigurace **Exclusions** (Vyloučení): Klikněte na minus vedle názvu entity a potom klikněte na **Save** (Uložit) v dolní části stránky.

Doporučujeme přidat vyloučení k detekcím až po přijetí upozornění na typ a určení, že se jedná o neškodnou pravdivě pozitivní aktivitu. 

> [!NOTE]
> Abychom vás ochránili, není možné nastavit vyloučení u všech detekcí. 

U některých detekcí jsou k dispozici tipy, které vám pomohou se rozhodnout, co chcete vyloučit. 

Každé vyloučení závisí na kontextu, u některých můžete nastavit uživatele a u jiných počítače nebo IP adresy. 

Když máte možnost vyloučit IP adresu nebo počítač, můžete vyloučit jednu z těchto věcí, nemusíte zadávat obě dvě.

> [!NOTE]
> Konfigurační stránky můžou upravovat jenom správci ATA.


## <a name="see-also"></a>Viz také
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Změna konfigurace ATA](modifying-ata-center-configuration.md)
