---
title: Práce s podezřelými aktivitami v Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje, jak kontrolovat podezřelé aktivity identifikované ATA.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 4/29/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b6ace439075324140decf8e0a3ea416f31913f78
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077180"
---
# <a name="working-with-suspicious-activities"></a>Práce s podezřelými aktivitami

*Platí pro: Advanced Threat Analytics verze 1.9*

Tento článek vysvětluje základy pro práci s Advanced Threat Analytics.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Kontrola podezřelých na časové ose útoku
Po přihlášení ke konzole ATA se vám automaticky otevře **Suspicious Activities Time Line** (Časová osa podezřelých aktivit). Podezřelé aktivity jsou uvedené v chronologickém pořadí s nejnovějšími podezřelými aktivita na vrcholu časové osy.
Každá podezřelá aktivita obsahuje následující informace:

-   Účastnící se entity, včetně uživatelů, počítačů, serverů, řadičů domény a prostředků.

-   Časy a časový rámec podezřelých aktivit.

-   Závažnost podezřelé aktivity – Vysoká, Střední nebo Nízká.

-   Stav: Otevření, ukončení nebo potlačení.

-   Schopnost

    -   Sdílet podezřelou aktivitu s ostatními lidmi ve vaší organizaci prostřednictvím e-mailu.

    -   Exportovat podezřelou aktivitu do Excelu.

> [!NOTE]
> -   Po přesunutí ukazatele myši nad uživatele nebo počítač, zobrazí se zkrácený profil entity, který nabízí další informace o entitě a obsahuje počet podezřelých aktivit, se kterými je entita propojená.
> -   Pokud kliknete na entitu, tím přejdete na profil entity pro uživatele nebo počítače.

![Obrázek časové osy podezřelých aktivit ATA](media/ATA-Suspicious-Activity-Timeline.JPG)

## <a name="filter-suspicious-activities-list"></a>Filtrování seznamu podezřelých aktivit
Chcete-li filtrovat seznam podezřelých aktivit:

1.  V **filtrovat podle** podokna na levé straně obrazovky vyberte jednu z následujících možností: **Všechny**, **otevřít**, **uzavřeno**, nebo **Potlačené**.

2.  Chcete-li dál filtrovat seznam, vyberte **vysokou**, **střední**, nebo **nízká**.

**Závažnost podezřelé aktivity**

-   **Nízká**

    Označuje podezřelé aktivity, které můžou vést k útokům určeným k tomu, aby software nebo uživatelé se zlými úmysly získali přístup k organizačním datům.

-   **Střední**

    Označuje podezřelé aktivity, které můžou pro konkrétní identity znamenat nebezpečí závažnějších útoků, které by mohly způsobit odcizení identity nebo zvýšení úrovně oprávnění.

-   **Vysoká**

    Označuje podezřelé aktivity, které mohou vést ke krádeži identity, zvýšení úrovně oprávnění nebo jiným vysoce závažným útokům


## <a name="remediating-suspicious-activities"></a>Opravy podezřelých aktivit
Můžete změnit stav podezřelé aktivity klepnutím na aktuální stav podezřelé aktivity a výběrem jedné z následujících **otevřít**, **Potlačená**, **uzavřeno**, nebo **odstranit**.
Uděláte to tak, že kliknete na tři tečky v pravém horním rohu konkrétní podezřelé aktivity a zobrazíte seznam dostupných akcí.

![Akce ATA pro podezřelé aktivity](./media/sa-actions.png)

**Stav podezřelé aktivity**

- **Otevřít**: V tomto seznamu se zobrazí všechny nové podezřelé aktivity.

- **Zavřít**: Slouží ke sledování podezřelých aktivit, které identifikovali, prozkoumali a opravili zmírnit.

  > [!NOTE]
  > Pokud se stejná aktivita zjistí během krátké doby znovu, ATA může znovu otevřít uzavřené aktivitu.

- **Potlačit**: Potlačení aktivity znamená, že chcete prozatím ignorovat a pouze znovu upozorněni při novou instanci. To znamená, že, pokud je podobná upozornění ATA nebude ho znovu otevřít. Ale pokud výstrahy po dobu sedmi dní zastaví a pak se znovu objeví, budete upozorněni znovu.

- **Odstranit**: Pokud výstrahu odstraníte, odstraní se ze systému, z databáze a nebudete moci obnovit. Po kliknutí na možnost pro odstranění budete moct odstranit všechny podezřelé aktivity stejného typu.

- **Vyloučit**: Možnost vyloučit entitu nevyvolávaly další určité typy výstrah. Můžete například nastavit, aby ATA vyloučila určitou entitu (uživatele nebo počítač) a neupozorňovala znovu na určitý typ podezřelé aktivity, jako je například určitý správce, který spouští vzdálený kód, nebo kontrola zabezpečení provádějící rekognoskaci DNS. Kromě toho, že je možné přidávat výjimky přímo k podezřelým aktivitám při jejich zjištění na časové ose, můžete také přejít na možnost **Exclusions** (Vyloučení) na stránce Configuration (Konfigurace) a pro každou podezřelou aktivitu ručně přidat a odebrat vyloučené entity nebo podsítě (například pro Pass-the-Ticket). 
  > [!NOTE]
  > Konfigurační stránky můžou upravovat jenom správci ATA.


## <a name="related-videos"></a>Související videa
- [Připojení k zabezpečení komunitě](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)


## <a name="see-also"></a>Viz také
- [Playbook podezřelé aktivity ATA](http://aka.ms/ataplaybook)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Změna konfigurace ATA](modifying-ata-center-configuration.md)
