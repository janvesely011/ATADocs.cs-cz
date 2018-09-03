---
title: Práce s podezřelými aktivitami v rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje, jak kontrolovat podezřelé aktivity identifikované služby Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4cf099faae920f23eeeaacdc8f10129005fdc896
ms.sourcegitcommit: 93a133430ac85d6db7afad5f6f2583b3a39c423a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/02/2018
ms.locfileid: "43469664"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="working-with-suspicious-activities"></a>Práce s podezřelými aktivitami
Tento článek vysvětluje základní informace o tom, jak pracovat s rozšířené ochrany před internetovými útoky pro Azure.

## Kontrola podezřelých na časové ose útoku <a name="review-suspicious-activities-on-the-attack-time-line"></a>
Po přihlášení na portálu ochrany ATP v programu Azure pracovního prostoru, budete automaticky přesměrováni na otevřeném **časové osy podezřelých**. Podezřelé aktivity jsou uvedené v chronologickém pořadí s nejnovějšími podezřelými aktivita na vrcholu časové osy.
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
> -   Pokud kliknete na entitu, tím přejdete na profil entity pro uživatele nebo počítače.

![Azure obrázek časové osy podezřelých aktivit ochrany ATP v programu](media/atp-sa-timeline.png)

## Detekce ve verzi Preview<a name="preview-detections"></a>

Výzkumným týmem služby Azure ATP neustále pracuje na implementaci nové detekce pro nově zjištěné útoky. Protože ochrany ATP v programu Azure je Cloudová služba, nové detekce, jsou vydávány rychle tak, aby zákazníci služby Azure ATP těžit z nové detekce co nejdříve.

Tyto detekce jsou označené náhled odznáčku, které vám pomohou identifikovat nové detekce a vědět, že jsou v produktu novinkami. Pokud vypnete detekce ve verzi preview, se nezobrazí v konzole služby Azure ATP – není na časové ose nebo profily entit – a nové výstrahy se neotevře.

![Zobrazit náhled zjišťování sítě vpn](./media/preview-detection-vpn.png) 

Ve výchozím nastavení jsou povoleny ve verzi preview detekce v ochrany ATP v programu Azure. 

Chcete-li zakázat detekce ve verzi preview:

1. V konzole služby Azure ATP klikněte na ikonu.
2. V nabídce vlevo v verzi Preview, klikněte na tlačítko **detekce**.
3. Pomocí posuvníku zapnutí a vypnutí detekce ve verzi preview.
 
![Detekce ve verzi Preview](./media/preview-detections.png) 


## <a name="filter-suspicious-activities-list"></a>Filtrování seznamu podezřelých aktivit
Chcete-li filtrovat seznam podezřelých aktivit:

1.  V **filtrovat podle** podokna na levé straně obrazovky vyberte jednu z následujících možností: **všechny**, **otevřít**, **uzavřeno**, nebo **Potlačené**.

2.  Chcete-li dál filtrovat seznam, vyberte **vysokou**, **střední**, nebo **nízká**.

**Závažnost podezřelé aktivity**

-   **Nízká**

    Označuje podezřelé aktivity, které můžou vést k útokům určeným k tomu, aby software nebo uživatelé se zlými úmysly získali přístup k organizačním datům.

-   **Střední**

    Označuje podezřelé aktivity, které můžou pro konkrétní identity znamenat nebezpečí závažnějších útoků, které by mohly způsobit odcizení identity nebo zvýšení úrovně oprávnění.

-   **Vysoká**

    Označuje podezřelé aktivity, které mohou vést ke krádeži identity, zvýšení úrovně oprávnění nebo jiným vysoce závažným útokům




## <a name="managing-suspicious-activities"></a>Správa podezřelé aktivity
Můžete změnit stav podezřelé aktivity klepnutím na aktuální stav podezřelé aktivity a výběrem jedné z následujících **otevřít**, **Potlačená**, **uzavřeno**, nebo **odstranit**.
Uděláte to tak, že kliknete na tři tečky v pravém horním rohu konkrétní podezřelé aktivity a zobrazíte seznam dostupných akcí.

![Azure akce ochrany ATP v programu pro podezřelé aktivity](./media/atp-sa-actions.png)

**Stav podezřelé aktivity**

-   **Open** (Otevřeno): V tomto seznamu se zobrazí všechny nové podezřelé aktivity.

-   **Zavřít**: slouží ke sledování podezřelých aktivit, které identifikovali, prozkoumali a opravili zmírnit.

    > [!NOTE]
    > Pokud se stejná aktivita zjistí během krátké doby znovu, ochrana ATP v programu Azure může znovu otevřít uzavřené aktivitu.

-   **Suppressed** (Potlačeno): Potlačení aktivity znamená, že ji chcete prozatím ignorovat a upozornění chcete zobrazit, jenom pokud se bude jednat o novou instanci. To znamená, že, pokud je podobná upozornění Azure ATP nebude ho znovu otevřít. Ale pokud výstrahy po dobu sedmi dní zastaví a pak se znovu objeví, budete upozorněni znovu.

- **Odstranit**: Pokud výstrahu odstraníte, odstraní se ze systému, z databáze a nebudete moci obnovit. Po kliknutí na možnost pro odstranění budete moct odstranit všechny podezřelé aktivity stejného typu.

- **Exclude** (Vyloučit): Možnost vyloučit entitu, aby se už nevyvolávaly další určité typy výstrah. Můžete například nastavit ochrana ATP v programu Azure k vyloučila určitou entitu (uživatele nebo počítače) neupozorňovala znovu na určitý typ podezřelé aktivity, jako je například určitý správce, který spouští vzdálený kód nebo kontrola zabezpečení provádějící rekognoskaci DNS. Kromě toho, že je možné přidávat výjimky přímo k podezřelým aktivitám při jejich zjištění na časové ose, můžete také přejít na možnost **Exclusions** (Vyloučení) na stránce Configuration (Konfigurace) a pro každou podezřelou aktivitu ručně přidat a odebrat vyloučené entity nebo podsítě (například pro Pass-the-Ticket). 

> [!NOTE]
> Konfigurační stránky můžou upravovat jenom správci služby Azure ATP.


## <a name="see-also"></a>Viz také

- [Práce s portálem pracovních prostorů služby Azure ATP](workspace-portal.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)