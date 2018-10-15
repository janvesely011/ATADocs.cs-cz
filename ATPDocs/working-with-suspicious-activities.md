---
title: Práce s výstrahami zabezpečení v rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Popisuje, jak kontrolovat výstrahy zabezpečení vydané služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 59bc8cdb995b1f7473efb7c0e601aca50a9ccafe
ms.sourcegitcommit: 58c75026e5ec4dcab3b0852a41f9f0a0ad6f22eb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/14/2018
ms.locfileid: "49315825"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="working-with-security-alerts"></a>Práce s výstrahami zabezpečení
Tento článek vysvětluje základní informace o tom, jak pracovat s rozšířené ochrany před internetovými útoky pro Azure.

## Kontrola upozornění zabezpečení na časové ose útoku <a name="review-suspicious-activities-on-the-attack-time-line"></a>
Po přihlášení na portál ochrany ATP v programu Azure, budete automaticky přesměrováni na otevřeném **časovou osu výstrahy zabezpečení**. Výstrahy zabezpečení jsou uvedené v chronologickém pořadí s nejnovějšími upozornění nahoře na časové ose.
Každá výstraha zabezpečení obsahuje následující informace:

-   Účastnící se entity, včetně uživatelů, počítačů, serverů, řadičů domény a prostředků.

-   Časy a časový rámec podezřelých aktivit, které iniciovala dané výstraze zabezpečení.

-   Závažnost výstrahy: Vysoká, střední nebo Nízká.

-   Stav: otevření, ukončení nebo potlačení

-   Schopnost

    -   Výstraha zabezpečení sdílejte s ostatními lidmi ve vaší organizaci prostřednictvím e-mailu.

    -   Exportujte do Excelu dané výstraze zabezpečení.

> [!NOTE]
> -   Když najedete myší nad uživatele nebo počítač, se zobrazí zkrácený profil entity, která poskytuje další informace o entitě a zahrnuje počet výstrah zabezpečení, které je entita propojená.
> -   Pokud kliknete na entitu, tím přejdete na profil entity pro uživatele nebo počítače.

![Obrázek časové osy výstrahy zabezpečení sady Azure ochrany ATP v programu](media/atp-sa-timeline.png)

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


## <a name="filter-security-alerts-list"></a>Filtrování seznamu výstrah zabezpečení
Chcete-li filtrovat seznam výstrah zabezpečení:

1.  V **filtrovat podle** podokna na levé straně obrazovky vyberte jednu z následujících možností: **všechny**, **otevřít**, **uzavřeno**, nebo **Potlačené**.

2.  Chcete-li dál filtrovat seznam, vyberte **vysokou**, **střední**, nebo **nízká**.

**Závažnost podezřelé aktivity**

-   **Nízká**

    Označuje aktivity, které může vést k útokům, které jsou navržené pro kyberzločincům nebo škodlivému softwaru získat přístup k datům organizace.

-   **Střední**

    Označuje aktivity, které můžou pro konkrétní identity hrozí nebezpečí závažnějších útoků, které by mohly způsobit odcizení identity nebo zvýšení úrovně oprávnění.

-   **Vysoká**

    Označuje aktivity, které mohou vést ke krádeži identity, zvýšení úrovně oprávnění nebo jiným vysoce závažným útokům


## <a name="managing-security-alerts"></a>Správa výstrah zabezpečení
Klepnutím na aktuální stav výstrahy zabezpečení a výběrem jedné z následujících akcí můžete změnit stav výstrahy zabezpečení **otevřít**, **Potlačená**, **uzavřeno**, nebo **Odstranit**.
Chcete-li to provést, klikněte na tlačítko tří teček v pravém horním rohu konkrétní výstrahu zobrazíte seznam dostupných akcí.

![Azure akce ochrany ATP v programu pro výstrahy zabezpečení](./media/atp-sa-actions.png)

**Stav výstrahy zabezpečení**

-   **Otevřít**: v tomto seznamu se zobrazí všechny nové výstrahy zabezpečení.

-   **Zavřít**: slouží ke sledování výstrah zabezpečení, které identifikovali, prozkoumali a opravili zmírnit.

    > [!NOTE]
    > Pokud se stejná aktivita zjistí během krátké doby znovu, ochrana ATP v programu Azure může znovu otevřít zavřenou výstrahu.

-   **Potlačit**: potlačení aalert znamená, že chcete prozatím ignorovat a pouze znovu upozorněni při novou instanci. To znamená, že, pokud je podobná upozornění Azure ATP nebude ho znovu otevřít. Ale pokud výstrahy po dobu sedmi dní zastaví a pak se znovu objeví, budete upozorněni znovu.

- **Odstranit**: Pokud výstrahu odstraníte, odstraní se ze systému, z databáze a nebudete moci obnovit. Po kliknutí na odstranit, budete moct odstranit všechny výstrahy zabezpečení stejného typu.

- **Exclude** (Vyloučit): Možnost vyloučit entitu, aby se už nevyvolávaly další určité typy výstrah. Můžete například nastavit ochrana ATP v programu Azure k vyloučila určitou entitu (uživatele nebo počítače) neupozorňovala znovu na určitý typ aktivity, jako je například určitý správce, který spouští vzdálený kód nebo kontrola zabezpečení provádějící rekognoskaci DNS. Kromě toho, že možnost přidávat výjimky přímo na dané výstraze zabezpečení při jejich zjištění na časové ose, můžete také přejít na stránku konfigurace, abyste **vyloučení**a pro jednotlivé výstrahy zabezpečení můžete ručně přidat a odebrat vyloučené entity nebo podsítě (například pro Pass-the-Ticket). 

> [!NOTE]
> Konfigurační stránky můžou upravovat jenom správci služby Azure ATP.


## <a name="see-also"></a>Viz také

- [Práce s portálem Azure ATP](workspace-portal.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)