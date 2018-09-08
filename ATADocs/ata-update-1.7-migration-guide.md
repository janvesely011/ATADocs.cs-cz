---
title: Průvodce migrací pro aktualizaci Advanced Threat Analytics na verzi 1.7 | Dokumentace Microsoftu
description: Postupy aktualizace ATA na verzi 1.7
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8eefcd45-7a4b-4074-ac5b-1ffc48e6654a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b8190552b91aa240b303bbe1a81e68086d19ded7
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166378"
---
# <a name="ata-update-to-17-migration-guide"></a>Průvodce migrací pro aktualizaci ATA na verzi 1.7
Aktualizace ATA na verzi 1.7 přináší vylepšení v následujících oblastech:

-   Nové detekce

-   Vylepšení stávajících detekcí
  

## <a name="updating-ata-to-version-17"></a>Aktualizace ATA na verzi 1.7

> [!NOTE] 
> Pokud ve vašem prostředí neexistuje instalace ATA, stáhněte si úplnou verzi ATA, která zahrnuje verzi 1.7 a postupujte podle pokynů standardní postup instalace popsaný v [instalace ATA](install-ata-step1.md).

Pokud již máte nasazení ATA verze 1.6, tento postup vás provede kroky potřebnými k aktualizaci vašeho nasazení.

> [!NOTE] 
> ATA verze 1.7 se nedá instalovat přímo přes ATA verze 1.4 nebo 1.5. Je nutné nejdřív instalovat ATA verze 1.6. 

Podle těchto kroků provedete aktualizaci ATA na verzi 1.7:

1.  [Stažení aktualizace 1.7](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
V této verzi se k instalaci nového nasazení ATA a upgradu stávajících nasazení používá stejný instalační soubor (Microsoft ATA Center Setup.exe).

2.  Aktualizace ATA Center

4.  Aktualizace komponent ATA Gateway

    > [!IMPORTANT]
    > Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.

### <a name="step-1-update-the-ata-center"></a>Krok 1: Aktualizace ATA Center

1.  Zazálohujte svou databázi: (volitelné)

    -   Pokud ATA Center běží jako virtuální počítač a chcete pořídit kontrolní bod, nejdřív vypnout virtuální počítač.

    -   Pokud ATA Center běží na fyzickém serveru, postupujte podle doporučeného postupu [zálohování MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Spusťte instalační soubor **Microsoft ATA Center Setup.exe** a nainstalujte aktualizaci podle pokynů na obrazovce.

    -  Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**.

    -  Pokud jste nepovolili automatické aktualizace ve verzi 1.6, zobrazí se výzva, abyste používali službu Microsoft Update k zajištění aktuálnosti ATA.  Na stránce služby Microsoft Update zaškrtněte **Při kontrole aktualizací použít službu Microsoft Update (doporučeno)**.
    ![Zachovat aktuální obrázek ATA](media/ata_ms_update.png) tím upraví nastavení Windows tak, aby povolovala aktualizace pro ostatní produkty Microsoftu (včetně ATA), zde. 
     ![Obrázek automatické aktualizace Windows](media/ata_installupdatesautomatically.png)

    -  Na obrazovce **Migrace dat** určete, jestli chcete migrovat všechna data nebo částečná data. Pokud budete chtít migrovat pouze částečná data, nepřesunou se dříve zaznamenané síťové přenosy a profily chování. To znamená, že bude trvat tři týdny, než detekce neobvyklého chování obsahuje kompletní profil, který umožní zjišťování neobvyklé aktivity. Během těchto tří týdnů všechny ostatní detekce ATA fungovat správně. **Částečná** migrace dat trvá mnohem kratší dobu. Pokud si vyberete **úplnou** migraci dat, může dokončení instalace trvat podstatně déle. Odhadovaná doba a požadované místo na disku, které jsou uvedeny na obrazovce **Migrace dat**, závisí na objemu dříve zaznamenaného síťového provozu uloženého v předchozích verzích ATA. Před výběrem **Částečné** nebo **Úplné** migrace zkontrolujte tyto požadavky.  
    
    ![Migrace dat ATA](media/migration-data-migration17.png)

    -  Klikněte na **Aktualizovat**. Po klepnutí na Aktualizovat bude ATA až do dokončení aktualizace offline.

4.  Po úspěšném dokončení aktualizace ATA Center klikněte na tlačítko **Spustit** a na konzole ATA pro komponenty ATA Gateway otevřete obrazovku **Aktualizace**.
    ![Obrazovka úspěšné aktualizace](media/migration-center-success17.png)

5.  V **aktualizace** obrazovky, pokud jste již nastavili automatické aktualizace ATA Gateway se aktualizace v tomto okamžiku, v opačném případě klikněte na tlačítko **aktualizovat** vedle každé ATA Gateway.
  ![Obrázek aktualizace bran](media/migration-update-gw-17.png)

  
> [!IMPORTANT] 
> Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.
> Nakonfigurovaný port naslouchacího procesu Syslog se u všech bran změní na 514.
 
> [!NOTE] 
> Pokud chcete nainstalovat nové brány ATA Gateway, přejděte na obrazovku **Brány** a klikněte na **Stáhnout instalační program brány**. Stáhne se instalační balíček pro ATA 1.7. Dále postupujte podle pokynů k instalaci nové brány, jak je popisuje [Krok 4. Instalace ATA Gateway](install-ata-step4.md).



## <a name="see-also"></a>Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
