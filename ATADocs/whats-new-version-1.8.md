---
title: Novinky ATA verze 1.8 | Dokumentace Microsoftu
description: "Tento článek obsahuje seznam novinek ATA verze 1.8 spolu se známými problémy."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: f2a4ed151db38497a6cec977f1090faf2eb4133e
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/05/2017
---
# Novinky ATA verze 1.8
<a id="whats-new-in-ata-version-18" class="xliff"></a>
Tato zpráva k vydání verze obsahuje informace o aktualizacích, nových funkcích, opravách chyb a známých problémech v této verzi Advanced Threat Analytics.



## Nové a aktualizované detekce
<a id="new--updated-detections" class="xliff"></a>

- Neobvyklá implementace protokolu byla vylepšena tak, aby byla schopna odhalit malware WannaCry.

- NOVINKA! **Neobvyklá úprava citlivých skupin** – jako součást fáze eskalace oprávnění upravují útočníci skupiny s vysokými oprávněními, aby získali přístup k citlivým prostředkům. ATA teď detekuje, pokud dojde u skupiny se zvýšenými oprávněními k neobvyklé změně.
- NOVINKA! **Podezřelé chyby ověřování** (behaviorální hrubá síla) – útočníci se pokoušejí prolomit účty hrubou silou s využitím přihlašovacích údajů. ATA teď při detekci neobvyklého chování při neúspěšném ověření zobrazí upozornění.   

- **Pokus o vzdálené spuštění – WMI exec** – útočníci se mohou pokusit o ovládnutí sítě vzdáleným spouštěním kódu na vašem řadiči domény. ATA má vylepšenou detekci vzdáleného spuštění obsahující detekci vzdáleného spuštění kódu pomocí metod WMI.

- Rekognoskace využívající dotazy adresářové služby – tato detekce byla vylepšena a je schopna odchytit dotazy na jedinou citlivou entitu a snížit počet falešně pozitivních událostí, které byly generovány v předchozí verzi. Pokud jste tuto funkci ve verzi 1.7 zakázali, při instalaci verze 1.8 se teď automaticky povolí.

- Aktivita zlatého lístku Kerberos – ATA 1.8 obsahuje další techniku pro detekci útoků pomocí zlatého lístku.
    - ATA teď detekuje podezřelé aktivity, kdy vyprší doba života zlatého lístku Kerberos. Pokud se lístek Kerberos používá déle než je povolená doba života, detekuje to ATA jako podezřelou aktivitu, že byl pravděpodobně vytvořen zlatý lístek Kerberos.
- Vylepšením následujících detekcí byly eliminovány falešně pozitivní události:  
    - Detekce eskalace oprávnění (zfalšovaný certifikát PAC) 
    - Aktivita související s oslabením šifrování (Skeleton Key)
    - Neobvyklá implementace protokolu
    - Porušení vztahu důvěryhodnosti

## Vylepšené posouzení podezřelých aktivit
<a id="improved-triage-of-suspicious-activities" class="xliff"></a>

-   NOVINKA! Během posuzování podezřelých událostí umožňuje ATA 1.8 provést následující akce: 
    - **Vyloučit entity** z vyvolávání budoucích podezřelých aktivit a zabránit tak upozorněním při detekci neškodných pravdivě pozitivních událostí (například správce spouštějící vzdálený kód nebo detekování kontrol zabezpečení).
    - **Potlačit upozornění na opakované** podezřelé aktivity.
    - **Odstranit podezřelé aktivity** z časové osy útoků.
-   Reakce na upozornění na podezřelou aktivitu je teď mnohem efektivnější. Časová osa podezřelých aktivit byla přepracována. Ve verzi ATA 1.8 uvidíte na jedné obrazovce mnohem více podezřelých aktivit a lepších informací pro účely posouzení a prošetření. 

## Nové sestavy, které pomáhají s prošetřením
<a id="new-reports-to-help-you-investigate" class="xliff"></a> 
-   NOVINKA! Byla přidána **souhrnná sestava**, ve které vidíte veškerá sumarizovaná data z ATA včetně podezřelých aktivit, problémů se stavem a dalších údajů. Můžete dokonce definovat přizpůsobenou sestavu, která se pravidelně automaticky generuje.
-   NOVINKA! Byla přidána **sestava citlivých skupin**, která umožňuje zjistit všechny změny provedené v citlivých skupinách za určité období.


## Vylepšení infrastruktury
<a id="infrastructure-improvements" class="xliff"></a>

-   Byl zvýšen výkon komponenty ATA Center. Ve verzi ATA 1.8 dokáže ATA Center zpracovat přes 1 milión paketů za sekundu.
-   ATA Lightweight Gateway teď dokáže číst události místně bez nutnosti konfigurace předávání událostí.
-   Vylepšení přístupnosti – s řešením ATA teď Microsoft poskytuje produkt, který je přístupný každému. 
-   Teď můžete zvlášť nakonfigurovat e-mail pro monitorovací upozornění a podezřelé aktivity.

## Vylepšení zabezpečení
<a id="security-improvements" class="xliff"></a>

-   NOVINKA! **Jednotné přihlašování při správě ATA**. ATA podporuje jednotné přihlašování integrované s ověřováním Windows – pokud jste už přihlášení ke svému počítači, použije ATA tento token pro přihlášení ke konzole ATA. K přihlášení můžete použít také čipovou kartu. Skripty pro tichou instalaci komponent ATA Gateway a ATA Lightweight Gateway teď používají kontext přihlášeného uživatele bez nutnosti zadávání přihlašovacích údajů.
-   Oprávnění Local System byla z procesu ATA Gateway odebrána, takže ke spuštění procesu ATA Gateway teď můžete použít virtuální účty (dostupné jen u samostatných komponent ATA Gateway), účty spravované služby a skupinové účty spravované služby.   
-   Byly přidány protokoly auditování komponent ATA Center a ATA Gateway a všechny akce jsou teď protokolované v protokolu událostí Windows.
-   Komponenta ATA Center byla doplněna o podporu certifikátů KSP.




## Viz také
<a id="see-also" class="xliff"></a>
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizace ATA na verzi 1.8 – průvodce migrací](ata-update-1.8-migration-guide.md)

