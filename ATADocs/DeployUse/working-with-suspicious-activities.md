---
title: "Práce s podezřelými aktivitami | Microsoft Advanced Threat Analytics"
description: "Popisuje, jak kontrolovat podezřelé aktivity identifikované ATA."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 44d7c899-816c-4f7f-91d3-84a09d291a24
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 1214560096227e00af36ff7cb1a0a95988a2ad40


---

# Práce s podezřelými aktivitami
Toto téma vysvětluje základy pro práci s Advanced Threat Analytics.

## Kontrola podezřelých na časové ose útoku
Po přihlášení ke konzole ATA se vám automaticky otevře **Suspicious Activities Time Line** (Časová osa podezřelých aktivit). Podezřelé aktivity jsou uvedené v chronologickém pořadí s nejnovějšími podezřelými aktivita na vrcholu časové osy.
Každá podezřelá aktivita obsahuje následující informace:

-   Účastnící se entity, včetně uživatelů, počítačů, serverů, řadičů domény a prostředků.

-   Časy a časový rámec podezřelých aktivit.

-   Závažnost podezřelé aktivity – Vysoká, Střední nebo Nízká.

-   Stav: Otevřeno, vyřešeno nebo zamítnuto.

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

**Stav podezřelé aktivity**

-   **Otevřenost**

    V tomto seznamu se zobrazí všechny nové podezřelé aktivity.

-   **Vyřešeno**

    Používá se ke sledování podezřelých aktivit, které jste identifikovali, prozkoumali a opravili s cílem zmírnit jejich dopad.

    > [!NOTE]
    > ATA může znovu otevřít vyřešenou aktivitu, pokud se stejná aktivita zjistí během krátké doby znovu.

-   **Zamítnuto**

    Jedná se o aktivity, které ručně zamítnete. Pokud ATA zjistí podobnou podezřelou aktivitu, vytvoří se nové zjištění.

## Poskytnutí vstupu k podezřelé aktivitě
Pro zajištění toho, že se ATA bude o vaší síti učit s vámi, některé podezřelé aktivity (rekognoskace DNS, pass-the-ticket, výčet relací SMB, neobvyklé chování a vzdálené spuštění) vyžadují váš vstup, aby se zlepšila detekce podezřelých aktivit do budoucna.

1.  Pro podezřelé aktivity, které vám umožní zadání vstupu, se automaticky otevře dotaz na vstup. Zobrazí se výzva k zodpovězení otázek týkajících se aktivit ve vaší síti a zda se mají považovat za podezřelé. V následujícím příkladu se zobrazí dotaz, jestli je spuštění nástrojů pro vyhledávání z určitého počítače povolené.

    ![Obrázek poskytnutí vstupu k podezřelým aktivitám ATA](media/ATA-Input.JPG)

2.  Pokud odpovíte záporně, bude se tato aktivita považovat za podezřelou a vždycky, když ATA tuto aktivitu z tohoto počítače zaznamená, budete upozorněni.

3.  Pokud ale odpovíte kladně, může být podezřelá aktivita zamítnuta a budoucí aktivity tohoto typu z tohoto počítače nemusí generovat podezřelou aktivitu nebo budou generovat aktivitu, která se automaticky zamítne.

4.  Pokud si nejste jisti, můžete kliknout na **Zrušit**.

## Změna stavu podezřelé aktivity
Můžete změnit stav podezřelé aktivity klepnutím na aktuální stav podezřelé aktivity a výběrem jedné z možností **Otevřeno**, **Vyřešeno** nebo **Zamítnuto**.

## Viz také
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Práce s nastavením detekce ATA](working-with-detection-settings.md)
- [Změna konfigurace ATA](modifying-ata-configuration.md)



<!--HONumber=Jun16_HO4-->


