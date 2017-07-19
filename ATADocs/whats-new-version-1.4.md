---
title: Novinky Advanced Threat Analytics verze 1.4 | Dokumentace Microsoftu
description: "Uvádí novinky ATA verze 1.4 spolu se známými problémy."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: cbea47f9-34c1-42b6-ae9e-6a472b49e1a5
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 69127773d9c3130bd07dee0b65956b93848ec399
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/30/2017
---
# <a name="what39s-new-in-ata-version-14"></a>Novinky ATA verze 1.4
Tyto poznámky k verzi obsahují informace o známých problémech ve verzi 1.4 Advanced Threat Analytics.

## <a name="whats-new-in-this-version"></a>Co je nového v této verzi?

-   Podpora předávání událostí Windows (WEF) pro odesílání událostí komponentě ATA Gateway přímo z řadičů domény.

-   Vylepšení detekce útoků Pass-the-Hash na podnikové prostředky kombinováním hloubkové kontroly paketů (DPI) a protokolů událostí Windows.

-   Vylepšení podpory zařízení nepřipojených k doméně a zařízení s jiným systémem než Windows z hlediska zjišťování a viditelnosti.

-   Vylepšení výkonu kvůli podpoře většího provozu pro komponenty ATA Gateway.

-   Vylepšení výkonu kvůli podpoře většího počtu komponent ATA Gateway na ATA Center.

-   Byl přidán nový proces automatického překladu IP adres, který páruje názvy počítačů a IP adresy. Tato jedinečná funkce ušetří během procesu šetření drahocenný čas a poskytne silné důkazy analytikům zabezpečení.

-   Vylepšená možnost shromažďovat vstup od uživatelů, aby se automaticky vyladil proces zjišťování.

-   Automatické zjišťování zařízení NAT.

-   Automatické převzetí služeb při selhání, když řadiče domény nejsou dostupné.

-   Sledování stavu systému a oznámení nyní poskytují celkový stav nasazení a taky konkrétní problémy související s konfigurací a připojením.

-   Náhled do jednotlivých webů a umístění, kde entity operují.

-   Podpora víc domén.

-   Podpora domén s názvem bez přípony (SDL).

-   Podpora pro úpravu IP adres a certifikátů komponent ATA Gateway a ATA Center.

-   Telemetrie pomáhající zlepšovat prostředí zákazníků.

## <a name="known-issues"></a>Známé problémy
V této verzi existují následující známé problémy.

### <a name="network-capture-software"></a>Software pro zachycení dat ze sítě
Jediný podporovaný software pro zachycení dat ze sítě, který můžete v ATA Gateway instalovat, je [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865). Neinstalujte Microsoft Message Analyzer nebo jiný software pro zachycení dat ze sítě. Instalace jiného softwaru způsobí, že ATA Gateway přestane fungovat správně.

### <a name="installation-from-zip-file"></a>Instalace ze souboru zip
Při instalaci ATA Gateway se ujistěte, že jste extrahovali soubory ze souboru zip do místního adresáře a odtud provádíte instalaci. Neinstalujte ATA Gateway přímo ze souboru zip, jinak se instalace nezdaří.

### <a name="uninstalling-previous-versions-of-ata"></a>Odinstalování předchozích verzí ATA
Pokud jste nainstalovali předchozí verzi ATA, Public Preview nebo Private Preview, je nutné před instalací této verze ATA odinstalovat komponenty ATA Center a ATA Gateway.

Musíte také odstranit soubory databáze a soubory protokolu. Databáze z předchozí verze ATA nejsou kompatibilní s verzí GA ATA.

Pokud se při pokusu o odinstalaci komponenty ATA Center nebo ATA Gateway otevře instalace ATA místo odinstalace, budete muset přidat následující klíč registru a pak odinstalovat ATA znovu.

**ATA Center**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center

-   Přidejte novou řetězcovou hodnotu s názvem `InstallationPath` a hodnotou `C:\Program Files\Microsoft Advanced Threat Analytics\Center`. Toto je výchozí instalační složka. Pokud jste instalační složku změnili, zadejte cestu k instalaci ATA.

    ![Editor registru pro cestu instalace ATA Center](media/ATA-uninstall-center-bug.jpg)

**ATA Gateway**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Gateway

-   Přidejte novou řetězcovou hodnotu s názvem `InstallationPath` a hodnotou `C:\Program Files\Microsoft Advanced Threat Analytics\Gateway`. Toto je výchozí instalační složka.  Pokud jste instalační složku změnili, zadejte cestu k instalaci ATA.

    ![Editor registru pro cestu instalace ATA Gateway](media/ATA-GW-uninstall-bug.jpg)

Po odinstalaci odstraňte instalační složku pro komponentu ATA Center i ATA Gateway.  Pokud jste nainstalovali databázi do samostatné složky, odstraňte složku databáze v ATA Center.

### <a name="health-alert---disconnected-ata-gateway"></a>Výstraha stavu – odpojená ATA Gateway
Pokud máte více než jednu komponentu ATA Gateway a obdržíte výstrahu o odpojení ATA Gateway, automatické řešení bude fungovat pouze pro jednu z nich, přičemž zbývající zůstanou v otevřeném stavu. Je potřeba ručně potvrdit, že ATA Gateway běží a že je služba spuštěná, a vyřešit výstrahu ručně.

### <a name="kb-on-virtualization-host"></a>Aktualizace KB na hostiteli virtualizace
Neinstalujte na hostiteli virtualizace aktualizaci KB 3047154. Může způsobit, že zrcadlení portů přestane fungovat správně.

## <a name="see-also"></a>Viz také

[Aktualizace ATA na verzi 1.6 – průvodce migrací](ata-update-1.6-migration-guide.md)

[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)