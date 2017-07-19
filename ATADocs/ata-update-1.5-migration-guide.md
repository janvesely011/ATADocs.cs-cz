---
title: "Průvodce migrací pro aktualizaci Advanced Threat Analytics na verzi 1.5 | Dokumentace Microsoftu"
description: Postupy aktualizace ATA na verzi 1.5
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: daaa2b3d495900d84fe7b61afb8e3bb22b3d7f72
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/30/2017
---
# <a name="ata-update-to-15-migration-guide"></a>Průvodce migrací pro aktualizaci ATA na verzi 1.5
Aktualizace ATA na verzi 1.5 přináší vylepšení v následujících oblastech:

-   Rychlejší detekce

-   Vylepšený algoritmus automatického zjišťování pro zařízení překladu síťových adres (NAT)

-   Vylepšený proces překladu IP adres pro zařízení nepřipojená k doméně

-   Podpora pro migraci dat během aktualizací produktu

-   Lepší odezvy uživatelského rozhraní pro podezřelé aktivity s tisíci entitami

-   Vylepšené automatické řešení výstrah monitorování

-   Další čítače výkonu pro rozšířené monitorování a řešení potíží

## <a name="updating-ata-to-version-15"></a>Aktualizace ATA na verzi 1.5
> [!NOTE]
> Pokud ve vašem prostředí neexistuje instalace ATA, stáhněte si úplnou verzi ATA, která zahrnuje verzi 1.5, a použijte standardní postup instalace popsaný v tématu [Instalace ATA](install-ata-step1.md).

Pokud již máte nasazení ATA verze 1.4, tento postup vás provede kroky potřebnými k aktualizaci instalace.

Podle těchto kroků provedete aktualizaci ATA na verzi 1.5:

1.  ATA verze 1.5 si můžete stáhnout z webu VLSC nebo MSDN.
      > [!NOTE]
         K provedení aktualizace na verzi 1.5 můžete také použít úplnou verzi ATA.


2.  Aktualizace ATA Center

3.  Stažení aktualizovaného balíčku ATA Gateway

4.  Aktualizace komponent ATA Gateway

    > [!IMPORTANT]
    > Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.

### <a name="step-1-update-the-ata-center"></a>Krok 1: Aktualizace ATA Center

1.  Zazálohujte svou databázi: (volitelné)

    -   Pokud ATA Center běží jako virtuální počítač a chcete pořídit kontrolní bod, ukončete nejprve virtuální počítač.

    -   Pokud ATA Center běží na fyzickém serveru, postupujte podle doporučeného postupu [zálohování MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Spusťte soubor aktualizace, Microsoft ATA Center Update.exe, a nainstalujte aktualizaci podle pokynů na obrazovce.

    1.  Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**.

    2.  Přečtěte si licenční smlouvou s koncovým uživatelem, a pokud s podmínkami souhlasíte, klikněte na zaškrtávací políčko a klikněte na **Další**.

    3.  Vyberte, zda chcete spustit úplnou (výchozí) nebo částečnou migraci.

        ![Volba úplné nebo částečné migrace](media/ATA-center-fullpartial.png)

        -   Pokud vyberete **částečnou** migraci, veškerý shromážděný síťový provoz a předávané události Windows, které analyzuje ATA, se odstraní a profily chování uživatelů bude potřeba znovu učit po dobu aspoň tří týdnů. Pokud máte málo místa na disku, pak je vhodné spustit **částečnou** migraci.

        -   Pokud spustíte **úplnou** migraci, budete potřebovat další místo na disku, které je pro vás spočítané na stránce upgradu, a migrace může trvat déle, v závislosti na provoz v síti. Úplná migrace uchovává všechny dříve shromážděná data a zachovají se profily chování uživatelů, což znamená, že ATA nebude potřebovat další čas pro učení profilů chování a neobvyklé chování bude možné zjišťovat okamžitě po aktualizaci.

3.  Klikněte na **Aktualizovat**. Po klepnutí na Aktualizovat bude ATA až do dokončení aktualizace offline.

4.  Po aktualizaci ATA Center budou komponenty ATA Gateway hlásit, že jsou nyní zastaralé.

    ![Obrázek zastaralých bran](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.

### <a name="step-2-download-the-ata-gateway-setup-package"></a>Krok 2: Stažení instalačního balíčku ATA Gateway
Po konfiguraci nastavení připojení k doméně si můžete stáhnout instalační balíček ATA Gateway.

Stažení instalačního balíčku ATA Gateway:

1.  Odstraňte všechny předchozí verze balíčku ATA Gateway, které jste dříve stáhli.

2.  Na počítači ATA Gateway spusťte prohlížeč a zadejte IP adresu, kterou jste nakonfigurovali v ATA Center pro konzolu ATA. Když se konzola ATA otevře, klikněte na ikonu nastavení a vyberte **Konfigurace**.

    ![Ikona nastavení konfigurace](media/ATA-config-icon.png)

3.  Na kartě **ATA Gateway** klikněte na **Download ATA Gateway Setup** (Stáhnout instalaci ATA Gateway).

4.  Uložte balíček místně.

Soubor zip obsahuje následující:

-   Instalační program ATA Gateway

-   Soubor nastavení konfigurace s požadovanými informacemi pro připojení k ATA Center

### <a name="step-3-update-the-ata-gateways"></a>Krok 3: Aktualizace komponent ATA Gateway

1.  Na každém počítači s ATA Gateway extrahujte soubory z balíčku ATA Gateway a spusťte soubor Microsoft ATA Gateway Setup.

    > [!NOTE]
    > Tento balíček ATA Gateway lze použít také k instalaci nových komponent ATA Gateway.

2.  Předchozí nastavení se zachovají, ale může trvat několik minut, než se služba restartuje.

3.  Tento krok opakujte pro všechny nasazené komponenty ATA Gateway.

> [!NOTE]
> Po úspěšné aktualizaci ATA Gateway zastaralé oznámení pro konkrétní ATA Gateway zmizí.

To, že jsou všechny komponenty ATA Gateway úspěšně aktualizované, budete vědět, když všechny ATA Gateway ohlásí, že jsou úspěšně synchronizované, a zpráva, že je k dispozici aktualizovaný balíček ATA Gateway, se už nebude zobrazovat.

![Obrázek aktualizovaných bran](media/ATA-gw-updated.png)

## <a name="see-also"></a>Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
