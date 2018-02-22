---
title: "Práce s podezřelými aktivitami v Azure Advanced Threat Protection | Microsoft Docs"
description: "Popisuje, jak zkontrolovat podezřelé aktivity, které se identifikovanou pomocí Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a5e7598e94e1d6d4b09c827770e062be9fefd1c4
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="working-with-suspicious-activities"></a>Práce s podezřelými aktivitami
Tento článek vysvětluje základní informace o tom, jak pracovat s Azure Advanced Threat Protection.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Kontrola podezřelých na časové ose útoku
Po přihlášení k portálu Azure ATP pracovního prostoru se automaticky otevře otevře **podezřelé aktivity časová osa**. Podezřelé aktivity jsou uvedené v chronologickém pořadí s nejnovějšími podezřelými aktivita na vrcholu časové osy.
Každá podezřelá aktivita obsahuje následující informace:

-   Účastnící se entity, včetně uživatelů, počítačů, serverů, řadičů domény a prostředků.

-   Časy a časový rámec podezřelých aktivit.

-   Závažnost podezřelé aktivity – Vysoká, Střední nebo Nízká.

-   Stav: otevření, ukončení nebo potlačení

-   Schopnost

    -   Sdílet podezřelou aktivitu s ostatními lidmi ve vaší organizaci prostřednictvím e-mailu.

    -   Exportovat podezřelou aktivitu do Excelu.

> [!NOTE]
> -   Po přesunutí ukazatele myši nad uživatele nebo počítač, zobrazí se zkrácený profil entity, který nabízí další informace o entitě a obsahuje počet podezřelých aktivit, se kterými je entita propojená.
> -   Pokud kliknete na entitu, budete přejdete do entity profil uživatele nebo počítače.

![Obrázek časové osy podezřelých aktivit Azure ATP](media/atp-sa-timeline.png)

## <a name="filter-suspicious-activities-list"></a>Filtrování seznamu podezřelých aktivit
Chcete-li filtrovat seznam podezřelých aktivit:

1.  V **filtrovat podle** na levé straně obrazovky vyberte jednu z následujících možností: **všechny**, **otevřete**, **uzavřeno**, nebo **Potlačené**.

2.  Chcete-li dál filtrovat seznam, vyberte **vysokou**, **střední**, nebo **nízká**.

**Závažnost podezřelé aktivity**

-   **Nízká**

    Označuje podezřelé aktivity, které můžou vést k útokům určeným k tomu, aby software nebo uživatelé se zlými úmysly získali přístup k organizačním datům.

-   **Střední**

    Označuje podezřelé aktivity, které můžou pro konkrétní identity znamenat nebezpečí závažnějších útoků, které by mohly způsobit odcizení identity nebo zvýšení úrovně oprávnění.

-   **Vysoká**

    Označuje podezřelé aktivity, které může vést ke krádeži identity, zvýšení úrovně oprávnění nebo jiných vysoce závažným útokům.




## <a name="managing-suspicious-activities"></a>Správa podezřelé aktivity
Můžete změnit stav podezřelé aktivity klepnutím na aktuální stav podezřelé aktivity a výběrem jedné z následujících **otevřete**, **Suppressed**, **uzavřeno**, nebo **odstranit**.
Uděláte to tak, že kliknete na tři tečky v pravém horním rohu konkrétní podezřelé aktivity a zobrazíte seznam dostupných akcí.

![Azure ATP akce pro podezřelé aktivity](./media/atp-sa-actions.png)

**Stav podezřelé aktivity**

-   **Open** (Otevřeno): V tomto seznamu se zobrazí všechny nové podezřelé aktivity.

-   **Zavřít**: slouží ke sledování podezřelých aktivit, které určili, prozkoumali a opravili omezeny.

    > [!NOTE]
    > Pokud se stejná aktivita zjistí během krátké doby znovu, Azure ATP může znovu otevřít uzavřené aktivitu.

-   **Suppressed** (Potlačeno): Potlačení aktivity znamená, že ji chcete prozatím ignorovat a upozornění chcete zobrazit, jenom pokud se bude jednat o novou instanci. To znamená, že, pokud je podobné výstrahy ATP Azure nepodporuje ho znovu otevřít. Ale pokud výstrahu zastaví sedm dní a potom je opět zobrazit, budete upozorněni znovu.

- **Odstranit**: Pokud odstraníte výstrahu, je odstraněn ze systému, z databáze a nebudete moci obnovit. Po kliknutí na možnost pro odstranění budete moct odstranit všechny podezřelé aktivity stejného typu.

- **Exclude** (Vyloučit): Možnost vyloučit entitu, aby se už nevyvolávaly další určité typy výstrah. Například můžete nastavit Azure ATP vyloučit konkrétní entitu (uživatele nebo počítače) z výstrahy znovu pro určitý typ podezřelé aktivity, jako je například konkrétní správce, který spouští vzdálenou kódu nebo kontrolu zabezpečení, která provádí rekognoskace DNS. Kromě toho, že je možné přidávat výjimky přímo k podezřelým aktivitám při jejich zjištění na časové ose, můžete také přejít na možnost **Exclusions** (Vyloučení) na stránce Configuration (Konfigurace) a pro každou podezřelou aktivitu ručně přidat a odebrat vyloučené entity nebo podsítě (například pro Pass-the-Ticket). 

> [!NOTE]
> Konfigurační stránky lze upravit pouze správci Azure ATP.


## <a name="see-also"></a>Viz také

- [Práce s portálem Azure ATP pracovního prostoru](workspace-portal.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)