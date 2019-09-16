---
title: Práce s výstrahami zabezpečení v Rozšířené ochraně před internetovými útoky Azure | Microsoft Docs
description: Popisuje, jak zkontrolovat výstrahy zabezpečení vydané službou Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d8070102bf5136ef8918f6fca2e7571e969148a5
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71004857"
---
# <a name="working-with-security-alerts"></a>Práce s výstrahami zabezpečení

> [!NOTE]
> Funkce ATP Azure, které jsou na této stránce popsané, jsou dostupné taky pomocí nového [portálu](https://portal.cloudappsecurity.com).

Tento článek vysvětluje základní informace o tom, jak pracovat s výstrahami zabezpečení Azure ATP.

## Kontrola výstrah zabezpečení na časové ose útoků<a name="review-suspicious-activities-on-the-attack-time-line"></a>

Po přihlášení k portálu Azure ATP automaticky přejdete na otevřenou **časovou osu výstrah zabezpečení**. Výstrahy zabezpečení jsou uvedeny v chronologickém pořadí s nejnovější výstrahou v horní části časové osy.

Každé upozornění zabezpečení má následující informace:

- Účastnící se entity, včetně uživatelů, počítačů, serverů, řadičů domény a prostředků.

- Časy a časové rámce podezřelých aktivit, které výstrahu zabezpečení iniciovaly.

- Závažnost výstrahy: Vysoká, střední nebo nízká.

- Stav: Otevřené, uzavřené nebo potlačené.

- Možnost:

    - Pomocí e-mailu sdílejte upozornění zabezpečení s ostatními lidmi ve vaší organizaci.

    - Stáhněte si výstrahu zabezpečení ve formátu aplikace Excel.

> [!NOTE]
> - Když najedete myší na uživatele nebo počítač, zobrazí se malý profil entity. Tento mini profil obsahuje další informace o entitě a obsahuje počet výstrah zabezpečení, se kterými je entita propojena.
> - Kliknutím na entitu přejdete do profilu entity uživatele nebo počítače.

![Obrázek časové osy výstrah zabezpečení Azure ATP](media/atp-sa-timeline.png)

## <a name="security-alert-categories"></a>Kategorie výstrah zabezpečení

Výstrahy zabezpečení Azure ATP jsou rozdělené do následujících kategorií nebo fází, jako jsou například fáze zobrazené v typickém dezaktivačním řetězu internetového útoku. 

- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před taktikou lateral movement](atp-lateral-movement-alerts.md)
- [Výstrahy před dominancí v doméně](atp-domain-dominance-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)

## Zjišťování verze Preview<a name="preview-detections"></a>

Výzkumný tým Azure ATP neustále funguje na implementaci nových detekcí nově zjištěných útoků. Vzhledem k tomu, že Azure ATP je cloudová služba, jsou nové detekce vydávány rychle, aby zákazníci Azure ATP mohli využívat nové zjišťování co nejdříve.

Tyto detekce jsou označeny příznakem verze Preview, který vám usnadní identifikaci nových zjišťování a víte, že jsou pro produkt nové. Pokud zjistíte, že se rozpoznávání ve verzi Preview vypne, nezobrazí se v konzole Azure ATP – ne v časové ose ani v profilech entit – a nové výstrahy se neotevřou.

![síť VPN pro zjišťování verze Preview](./media/preview-detection-vpn.png)

Ve výchozím nastavení jsou detekce ve verzi Preview zapnutá v Azure ATP. 

Zakázání zjišťování ve verzi Preview:

1. V konzole Azure ATP klikněte na nastavení ozubeného kola.
2. V nabídce vlevo v části Náhled klikněte na **detekce**.
3. Pomocí posuvníku zapněte nebo vypněte zjišťování verze Preview.
 
![zjišťování verze Preview](./media/preview-detections.png) 


## <a name="filter-security-alerts-list"></a>Filtrovat seznam výstrah zabezpečení
Filtrování seznamu výstrah zabezpečení:

1. V podokně **filtrovat podle** na levé straně obrazovky vyberte jednu z následujících možností: **Všechna**, **otevřená**, **uzavřená**nebo **potlačení**.

2. Chcete-li dále filtrovat seznam, vyberte **Vysoká**, **střední**nebo **Nízká**.

**Závažnost podezřelé aktivity**

- **Nízká**

    Označuje aktivity, které mohou vést k útokům, které jsou určeny pro uživatele se zlými úmysly nebo softwaru k získání přístupu k datům organizace.

- **Střední**

    Označuje aktivity, které můžou ohrozit konkrétní identity v případě závažnějších útoků, které by mohly způsobit odcizení identity nebo zvýšení úrovně oprávnění.

- **Vysoká**

    Označuje aktivity, které můžou vést k krádeži identity, eskalaci oprávnění nebo jiným útokům s vysokým dopadem.


## <a name="managing-security-alerts"></a>Správa výstrah zabezpečení

Stav výstrahy zabezpečení můžete změnit tak, že kliknete na aktuální stav výstrahy zabezpečení a vyberete jednu z následujících možností **otevřít**, **potlačit**, **Uzavřeno**nebo **odstraněno**.
Chcete-li zobrazit seznam dostupných akcí, klikněte na tři tečky v pravém horním rohu konkrétní výstrahy.

![Akce ATP Azure pro výstrahy zabezpečení](./media/atp-sa-actions.png)

**Stav výstrahy zabezpečení**

- **Otevřete**: V tomto seznamu se zobrazí všechny nové výstrahy zabezpečení.

- **Zavřít**: Se používá ke sledování výstrah zabezpečení, které jste identifikovali, prohledali a opravili pro zmírnění.

    > [!NOTE]
    > Pokud se stejná aktivita zjistí znovu v krátké době, může Azure ATP znovu otevřít zavřenou výstrahu.

- **Potlačit**: Potlačení výstrahy znamená, že ji chcete nyní ignorovat a pouze v případě, že je k dispozici nová instance. To znamená, že pokud existuje podobná výstraha Azure ATP, neotevře se. Pokud se ale upozornění zastaví na sedm dní a pak se znovu zobrazí, budete upozorněni.

- **Odstranit**: Odstraníte-li výstrahu, bude odstraněna ze systému z databáze a nebude možné ji obnovit. Po kliknutí na Odstranit budete moct odstranit všechny výstrahy zabezpečení stejného typu.

- **Vyloučit**: Možnost vyloučit entitu z vyvolávání většího množství určitých typů výstrah. Můžete například nastavit ATP Azure tak, aby pro určitý typ aktivity vyloučila konkrétní entitu (uživatele nebo počítač), třeba konkrétního správce, který spouští vzdálený kód nebo bezpečnostní skener, který provádí DNS rekognoskace. Kromě toho, že je možné přidat vyloučení přímo na výstrahu zabezpečení, jak je detekována v časovém intervalu, můžete také přejít na konfigurační stránku a **vyloučit**z každé výstrahy zabezpečení, které můžete ručně přidat a odebrat vyloučené entity nebo podsítě (pro Příklad pro Pass-The-Ticket).

> [!NOTE]
> Konfigurační stránky můžou upravovat jenom správci ATP Azure.


## <a name="see-also"></a>Viz také

- [Práce s portálem Azure ATP](workspace-portal.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
