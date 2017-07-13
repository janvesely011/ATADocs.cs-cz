---
title: "Práce s podezřelými aktivitami v Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Popisuje, jak kontrolovat podezřelé aktivity identifikované ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1ff15a323f461cf8436e1ff7e15738a49bf3973c
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/30/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# Práce s podezřelými aktivitami
<a id="working-with-suspicious-activities" class="xliff"></a>
Toto téma vysvětluje základy pro práci s Advanced Threat Analytics.

## Kontrola podezřelých na časové ose útoku
<a id="review-suspicious-activities-on-the-attack-time-line" class="xliff"></a>
Po přihlášení ke konzole ATA se vám automaticky otevře **Suspicious Activities Time Line** (Časová osa podezřelých aktivit). Podezřelé aktivity jsou uvedené v chronologickém pořadí s nejnovějšími podezřelými aktivita na vrcholu časové osy.
Každá podezřelá aktivita obsahuje následující informace:

-   Účastnící se entity, včetně uživatelů, počítačů, serverů, řadičů domény a prostředků.

-   Časy a časový rámec podezřelých aktivit.

-   Závažnost podezřelé aktivity – Vysoká, Střední nebo Nízká.

-   Stav: otevření, ukončení nebo potlačení

-   Schopnost

    -   Sdílet podezřelou aktivitu s ostatními lidmi ve vaší organizaci prostřednictvím e-mailu.

    -   Exportovat podezřelou aktivitu do Excelu.

    -   Přidat poznámku k podezřelé aktivitě.

    -   Poskytnout vstup k podezřelé aktivitě.

-   Poskytuje doporučení, jak reagovat na podezřelou aktivitu.

> [!NOTE]
> -   Po přesunutí ukazatele myši nad uživatele nebo počítač, zobrazí se zkrácený profil entity, který nabízí další informace o entitě a obsahuje počet podezřelých aktivit, se kterými je entita propojená.
> -   Pokud kliknete na entitu, přejdete na profil entity pro uživatele nebo počítač.

![Obrázek časové osy podezřelých aktivit ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## Filtrování seznamu podezřelých aktivit
<a id="filter-suspicious-activities-list" class="xliff"></a>
Chcete-li filtrovat seznam podezřelých aktivit:

1.  V podokně **Filtrovat podle** na levé straně obrazovky vyberte jednu z následujících položek: **Vše**, **Otevřeno**, **Vyřešeno** nebo **Zamítnuto**.

2.  Chcete-li dál filtrovat seznam, vyberte **Vysoká**, **Střední** nebo **Nízká**.

**Závažnost podezřelé aktivity**

-   **Nízká**

    Označuje podezřelé aktivity, které můžou vést k útokům určeným k tomu, aby software nebo uživatelé se zlými úmysly získali přístup k organizačním datům.

-   **Střední**

    Označuje podezřelé aktivity, které můžou pro konkrétní identity znamenat nebezpečí závažnějších útoků, které by mohly způsobit odcizení identity nebo zvýšení úrovně oprávnění.

-   **Vysoká**

    Označuje podezřelé aktivity, které můžou vést ke krádeži identity, zvýšení úrovně oprávnění nebo jiným vysoce závažným útokům.




## Opravy podezřelých aktivit
<a id="remediating-suspicious-activities" class="xliff"></a>
Stav podezřelé aktivity můžete změnit tak, že klepnete na aktuální stav podezřelé aktivity a vyberete jednu z možností **Open** (Otevřeno), **Suppressed** (Potlačeno), **Closed** (Uzavřeno) nebo **Deleted** (Odstraněno).
Uděláte to tak, že kliknete na tři tečky v pravém horním rohu konkrétní podezřelé aktivity a zobrazíte seznam dostupných akcí.

![Akce ATA pro podezřelé aktivity](./media/sa-actions.png)

**Stav podezřelé aktivity**

-   **Open** (Otevřeno): V tomto seznamu se zobrazí všechny nové podezřelé aktivity.

-   **Closed** (Uzavřeno): Slouží ke sledování podezřelých aktivit, které jste identifikovali, prozkoumali a opravili s cílem zmírnit jejich dopad.

    > [!NOTE]
    > ATA může znovu otevřít vyřešenou aktivitu, pokud se stejná aktivita zjistí během krátké doby znovu.

-   **Suppressed** (Potlačeno): Potlačení aktivity znamená, že ji chcete prozatím ignorovat a upozornění chcete zobrazit, jenom pokud se bude jednat o novou instanci. Znamená to, že pokud se vyskytne podobná výstraha, služba ATA ji neotevře. Pokud se ale výstraha na 7 dní zastaví a pak se znovu objeví, budete znovu upozorněni.

- **Delete** (Odstranit): Pokud výstrahu odstraníte, odstraní se z databáze v systému a NEBUDE možné ji obnovit. Po kliknutí na možnost pro odstranění budete moct odstranit všechny podezřelé aktivity stejného typu.

- **Exclude** (Vyloučit): Možnost vyloučit entitu, aby se už nevyvolávaly další určité typy výstrah. Můžete například nastavit, aby ATA vyloučila určitou entitu (uživatele nebo počítač) a neupozorňovala znovu na určitý typ podezřelé aktivity, jako je například určitý správce, který spouští vzdálený kód, nebo kontrola zabezpečení provádějící rekognoskaci DNS. Kromě toho, že je možné přidávat výjimky přímo k podezřelým aktivitám při jejich zjištění na časové ose, můžete také přejít na možnost **Exclusions** (Vyloučení) na stránce Configuration (Konfigurace) a pro každou podezřelou aktivitu ručně přidat a odebrat vyloučené entity nebo podsítě (například pro Pass-the-Ticket). 
> [!NOTE]
> Konfigurační stránky můžou upravovat jenom správci ATA.


## Viz také
<a id="see-also" class="xliff"></a>
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Práce s nastavením detekce ATA](working-with-detection-settings.md)
- [Změna konfigurace ATA](modifying-ata-center-configuration.md)
