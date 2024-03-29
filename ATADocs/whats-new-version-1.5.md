---
title: Novinky Advanced Threat Analytics verze 1.5 | Dokumentace Microsoftu
description: Uvádí novinky ATA verze 1.5 spolu se známými problémy.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c0658b0d9320116bf8a752ce360994946300947a
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65195732"
---
# <a name="whats-new-in-ata-version-15"></a>Novinky ATA verze 1.5
Tyto poznámky k verzi obsahují informace o známých problémech v této verzi Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-15-update"></a>Co je nového v aktualizaci ATA 1.5?
Aktualizace ATA 1.5 obsahuje vylepšení v následujících oblastech:

-   Rychlejší detekce

-   Vylepšený algoritmus automatického zjišťování pro zařízení překladu síťových adres (NAT)

-   Vylepšený proces překladu IP adres pro zařízení nepřipojená k doméně

-   Podpora pro migraci dat během aktualizací produktu

-   Lepší odezvy uživatelského rozhraní pro podezřelé aktivity s tisíci entitami

-   Vylepšené automatické řešení výstrah monitorování

-   Další čítače výkonu pro rozšířené monitorování a řešení potíží

## <a name="known-issues"></a>Známé problémy
V této verzi existují následující známé problémy.

### <a name="new-ata-gateway-installation-fails"></a>Instalace nové ATA Gateway se nezdaří
Po aktualizaci nasazení ATA na verzi 1.5 se při instalaci nové ATA Gateway zobrazí následující chyba: Microsoft Advanced Threat Analytics Gateway se nenainstalovala

![Chyba ATA GS](media/ata-install-error.png)

<b>Alternativní řešení:</b> Odeslání e-mailu <ataeval@microsoft.com> se žádost o kroky alternativního řešení.
### <a name="deployment"></a>Nasazení
Složka zadaná pro cestu k datům databáze a cestu k deníku databáze musí být prázdná (bez souborů a podsložek).
Pokud není prázdná, nepostupuje nasazení.

### <a name="installation-from-zip-file"></a>Instalace ze souboru zip
Při instalaci ATA Gateway se ujistěte, že jste extrahovali soubory ze souboru zip do místního adresáře a odtud provádíte instalaci. Neinstalujte ATA Gateway přímo v souboru zip nebo instalace se nezdaří.

### <a name="configuration"></a>Konfigurace
Po nastavení konfigurace služby ATA Gateway při jejím prvním spuštění se bude zobrazovat zpráva, že neproběhla synchronizace, dokud se služba úplně nespustí. To může při prvním spuštění služby trvat až 10 minut.

### <a name="network-capture-software"></a>Software pro zachycení dat ze sítě
Jediný podporovaný software pro zachycení dat ze sítě, který můžete v ATA Gateway instalovat, je [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865). Neinstalujte Microsoft Message Analyzer nebo jiný software pro zachycení dat ze sítě. Instalace jiného softwaru způsobí, že ATA Gateway přestane fungovat správně.

### <a name="kb-on-virtualization-host"></a>Aktualizace KB na hostiteli virtualizace
Neinstalujte na hostiteli virtualizace aktualizaci KB 3047154. Může způsobit, že zrcadlení portů přestane fungovat správně.

## <a name="see-also"></a>Viz také

[Aktualizace ATA na verzi 1.5 – průvodce migrací](ata-update-1.5-migration-guide.md)

[Aktualizace ATA na verzi 1.6 – průvodce migrací](ata-update-1.6-migration-guide.md)

[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
