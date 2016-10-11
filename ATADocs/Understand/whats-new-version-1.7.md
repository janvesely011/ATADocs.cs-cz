---
title: Novinky ATA verze 1.7 | Microsoft ATA
description: "Uvádí novinky ATA verze 1.7 spolu se známými problémy."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 09/20/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 
ms.reviewer: 
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d47d9e7be294c68d764710c15c4bb78539e42f62
ms.openlocfilehash: 62f2aadc978547647a1dc3c27ed3453f7ed15828


---

# Novinky ATA verze 1.7
Tyto poznámky k verzi obsahují informace o známých problémech v této verzi Advanced Threat Analytics.

## Co je nového v aktualizaci ATA 1.7?
Aktualizace ATA na verzi 1.7 přináší vylepšení v následujících oblastech:

-   Nové a aktualizované detekce

-   Řízení přístupu na základě role

-   Podpora systému Windows Server 2016 a jádra serveru Windows

-   Vylepšení uživatelského prostředí

-   Menší změny


### Nové a aktualizované detekce


- **Rekognoskace pomocí výčtu adresářových služeb** V rámci fáze rekognoskace útočníci pomocí různých metod shromažďují informace o entitách v síti. Výčet adresářových služeb pomocí protokolu SAM-R útočníkům umožňuje získat seznam uživatelů a skupin v doméně a pochopit vztahy mezi různými entitami. 

- **Vylepšení proti útoku typu Pass-the-Hash** Abychom zlepšili detekci útoku typu Pass-the-Hash, přidali jsme do ověřovacích vzorců entit další modely chování. Tyto modely umožňují funkci ATA korelaci chování entity s podezřelými ověřeními NTLM a odliší skutečné útoky typu Pass-the-Hash od chování ve falešně pozitivních scénářích.

- **Vylepšení proti útoku typu Pass-the-Ticket** Abychom úspěšně zjistili pokročilé útoky a zejména útoky typu Pass-the-Ticket, musí být korelace mezi IP adresou a účtem počítače přesná. Jedná se o náročný úkol v prostředích, kde se IP adresy zcela normálně rychle mění (například sítě Wi-Fi a skupina virtuálních počítačů, které sdílení stejného hostitele). Abychom tento problém vyřešili a zlepšili přesnost detekce útoků typu Pass-the-Ticket, výrazně jsme vylepšili mechanismus překladu síťového názvu funkce ATA, který teď zaznamenává menší počet falešně pozitivních shod.

- **Vylepšení proti nestandardnímu chování** V ATA verze 1.7 jsme přidali data ověřování NTLM jak zdroj dat pro detekci nestandardního chování a rozšířili jsme pokrytí algoritmu pro chování entit v síti. 

- **Vylepšení proti neobvyklé implementaci protokolu** ATA teď detekuje neobvyklou implementaci protokolu v protokolu Kerberos a také další anomálie v protokolu NTLM. Konkrétně se tyto nové anomálie protokolu Kerberos běžně používají v útocích typu Over-pass-the-Hash.


### Infrastruktura

- **Řízení přístupu na základě role** Možnost řízení přístupu na základě role (RBAC). ATA 1.7 obsahuje tři role: Správce ATA, Analytik ATA a Vedení ATA.

- **Podpora systému Windows Server 2016 a jádra serveru Windows** ATA 1.7 podporuje nasazení součástí Lightweight Gateways v řadičích domény, které používají jádro serveru pro systém Windows Server 2012 a jádro serveru pro systém Windows Server 2012 R2. Kromě toho tato verze podporuje Windows Server 2016 pro součásti ATA Center i ATA Gateway.

### Činnost koncového uživatele
- **Prostředí konfigurace** V této verzi bylo prostředí konfigurace ATA přepracováno, aby bylo uživatelsky vstřícnější a lépe podporovalo prostředí s několika ATA Gateway. Tato verze také zavádí stránku aktualizace ATA Gateway pro jednodušší, lepší správu automatických aktualizací pro různé brány.

## Známé problémy
V této verzi existují následující známé problémy.

### Automatické aktualizace brány se nemusí podařit.
**Příznaky:** V prostředích s pomalým připojením WAN může při aktualizaci ATA Gateway vypršet časový limit pro aktualizaci (100 sekund) a aktualizace se nepodaří.
V konzole ATA může ATA Gateway po dlouhou dobu zobrazovat stav „Probíhá aktualizace (stahování balíčku)“ a nakonec dojde k chybě.
**Alternativní řešení:** Pokud chcete tento problém vyřešit, stáhněte z konzoly ATA nejnovější balíček ATA Gateway a aktualizujte ATA Gateway ručně.

 > [!IMPORTANT]
 Automatické obnovení certifikátu pro certifikáty používané funkcí ATA není podporované. Použití těchto certifikátů po jejich automatickém obnovení může způsobit, že ATA přestane fungovat. 

### Prohlížeče nepodporují kódování JIS
**Příznaky:** Konzola ATA nemusí fungovat dle očekávání v prohlížečích s kódováním JIS. **Řešení:** Změňte kódování prohlížeče na Unicode UTF-8.
 
## Menší změny

- ATA teď pro konzolu ATA používá OWIN místo IIS.
- Pokud nefunguje služba ATA Center, nebudete mít přístup ke konzole ATA.
- Podsítě pro krátkodobé zapůjčení už nejsou potřebné z důvodu změn v ATA NNR.

## Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Aktualizace ATA na verzi 1.7 – průvodce migrací](ata-update-1.7-migration-guide.md)




<!--HONumber=Sep16_HO4-->


