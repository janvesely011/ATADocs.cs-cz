---
title: Průvodce migrací pro aktualizaci Advanced Threat Analytics na verzi 1.6 | Dokumentace Microsoftu
description: Postupy aktualizace ATA na verzi 1.6
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: barbkess
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 0756ef64-3aef-4a69-8981-24fa8f285c6a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7142c944ab0eacd299d4db720a08cc6705f564dc
ms.sourcegitcommit: 62b631f64a639f5df04bf805755f26c69b40e8e4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638945"
---
# <a name="ata-update-to-16-migration-guide"></a>Průvodce migrací pro aktualizaci ATA na verzi 1.6
Aktualizace ATA na verzi 1.6 přináší vylepšení v následujících oblastech:

-   Nové detekce

-   Vylepšení stávajících detekcí

-   ATA Lightweight Gateway

-   Automatické aktualizace

-   Vylepšený výkon komponenty ATA Center

-   Menší požadavky na úložiště

-   Podpora IBM QRadar

## <a name="updating-ata-to-version-16"></a>Aktualizace ATA na verzi 1.6
> [!NOTE] 
> Pokud ve vašem prostředí neexistuje instalace ATA, stáhněte si úplnou verzi ATA, která zahrnuje verzi 1.6 a postupujte podle pokynů standardní postup instalace popsaný v [instalace ATA](install-ata-step1.md).

Pokud již máte nasazení ATA verze 1.5, tento postup vás provede kroky potřebnými k aktualizaci vašeho nasazení.

> [!NOTE] 
> ATA verze 1.6 se nedá instalovat přímo přes ATA verze 1.4. Je nutné nejdřív instalovat ATA verze 1.5. Pokud se omylem pokusíte nainstalovat ATA 1.6 bez instalace ATA 1.5, zobrazí se chyba o tom, že **na vašem počítači je již nainstalovaná novější verze.** I když instalace se nezdařila - před instalací ATA verze 1.5 musíte odinstalovat zbytky ATA 1.6, které zůstávají ve vašem počítači.

Podle těchto kroků provedete aktualizaci ATA na verzi 1.6:

1. Pokud se chcete vyhnout potížím s upgrady, použijte kroky 8 až 10 v části **Selhání migrace při aktualizaci na ATA verze 1.6** uvedené v tématu [Novinky ATA verze 1.6](whats-new-version-1.6.md).
2. Ujistěte se, že máte nezbytné volné místo k dokončení upgradu. Můžete instalaci provést až po kontrolu připravenosti, získat tak odhad, kolik volného místa je potřeba, a po přidělení nezbytného místa na disku spustit upgrade znovu.
1.  [Stažení aktualizace 1.6](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
V této verzi se k instalaci nového nasazení ATA a upgradu stávajících nasazení používá stejný instalační soubor (Microsoft ATA Center Setup.exe).

2.  Aktualizace ATA Center

3.  Stažení aktualizovaného balíčku ATA Gateway

4.  Aktualizace komponent ATA Gateway

    > [!IMPORTANT]
    > Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.

### <a name="step-1-update-the-ata-center"></a>Krok 1: Aktualizace ATA Center

1.  Zazálohujte svou databázi: (volitelné)

    -   Pokud ATA Center běží jako virtuální počítač a chcete pořídit kontrolní bod, nejdřív vypnout virtuální počítač.

    -   Pokud ATA Center běží na fyzickém serveru, postupujte podle doporučeného postupu [zálohování MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Spusťte instalační soubor Microsoft ATA Center Setup.exe a nainstalujte aktualizaci podle pokynů na obrazovce.

    1.  ATA 1.6 vyžaduje instalaci rozhraní .Net Framework 4.6.1. Pokud ještě není nainstalované, instalace ATA nainstaluje rozhraní .net Framework 4.6.1 jako součást instalace.
    
        > [!NOTE] 
        > Instalace rozhraní .Net Framework 4.6.1 může vyžadovat restartování serveru. Instalace ATA bude pokračovat až po restartování serveru.
    
    2.  Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**.

    3.  Přečtěte si licenční smlouvou s koncovým uživatelem a pokud souhlasíte s podmínkami, klikněte na tlačítko **Další**.

    4.  Teď je k zajištění aktuálnosti ATA možné použít službu Microsoft Update.  Na stránce služby Microsoft Update zaškrtněte **Při kontrole aktualizací použít službu Microsoft Update (doporučeno)**.
    ![Zachovat aktuální obrázek ATA](media/ata_ms_update.png) tím upraví nastavení Windows tak, aby povolovala aktualizace pro ostatní produkty Microsoftu (včetně ATA), zde. 
     ![Obrázek automatické aktualizace Windows](media/ata_installupdatesautomatically.png)

    5.  Před zahájením instalace ATA provede kontrolu připravenosti. Zkontrolovat výsledky kontroly a ujistěte se, že požadované součásti jsou správně a že máte alespoň minimální množství místa na disku. 
    ![Obrázek kontroly připravenosti ATA](media/ata_install_readinesschecks.png)

    6.  Klikněte na tlačítko **aktualizace**. Po klepnutí na Aktualizovat bude ATA až do dokončení aktualizace offline.

3.  Po aktualizaci ATA Center budou komponenty ATA Gateway hlásit, že jsou nyní zastaralé.

    ![Obrázek zastaralých bran](media/ATA-center-outdated.png)

> [!IMPORTANT] 
> Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.

### <a name="step-2-download-the-ata-gateway-setup-package"></a>Krok 2. Stažení instalačního balíčku ATA Gateway
Po konfiguraci nastavení připojení k doméně si můžete stáhnout instalační balíček ATA Gateway.

Stažení instalačního balíčku ATA Gateway:

1.  Odstraňte všechny předchozí verze balíčku ATA Gateway, které jste dříve stáhli.

2.  Na počítači ATA Gateway spusťte prohlížeč a zadejte IP adresu, kterou jste nakonfigurovali v ATA Center pro konzolu ATA. Když se konzola ATA otevře, klikněte na ikonu nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace](media/ATA-config-icon.png)

3.  Na kartě **ATA Gateway** klikněte na **Download ATA Gateway Setup** (Stáhnout instalaci ATA Gateway).

4.  Uložte balíček místně.

Soubor zip obsahuje následující soubory:

-   Instalační program ATA Gateway

-   Soubor nastavení konfigurace s požadovanými informacemi pro připojení k ATA Center

### <a name="step-3-update-the-ata-gateways"></a>Krok 3: Aktualizace komponent ATA Gateway

1.  Na každém počítači s ATA Gateway extrahujte soubory z balíčku ATA Gateway a spusťte soubor **Microsoft ATA Gateway Setup**.

    > [!NOTE] 
    > Tento balíček ATA Gateway lze použít také k instalaci nových komponent ATA Gateway.

2.  Předchozí nastavení se zachovají, ale může trvat několik minut, než se služba restartuje.

3.  Tento krok opakujte pro všechny nasazené komponenty ATA Gateway.

> [!NOTE] 
> Po úspěšné aktualizaci ATA Gateway zastaralé oznámení pro konkrétní ATA Gateway zmizí.

Víte, že všechny komponenty ATA Gateway se úspěšně aktualizovaly při všechny komponenty ATA Gateway hlásit, že jsou úspěšně synchronizované a zpráva, že je k dispozici aktualizovaný balíček ATA Gateway zmizí.

![Obrázek aktualizovaných bran](media/ATA-gw-updated.png)


## <a name="see-also"></a>Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
