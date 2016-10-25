---
title: "Průvodce migrací pro aktualizaci ATA na verzi 1.7 | Microsoft ATA"
description: Postupy aktualizace ATA na verzi 1.7
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 3a821bf1479af529fd65e2153f8b722999c83a4f
ms.openlocfilehash: 444bc4744834219d9db7bc8c209f33c039f90dad


---

# Průvodce migrací pro aktualizaci ATA na verzi 1.7
Aktualizace ATA na verzi 1.7 přináší vylepšení v následujících oblastech:

-   Nové detekce

-   Vylepšení stávajících detekcí
  

## Aktualizace ATA na verzi 1.7

> [!NOTE] 
> Pokud ve vašem prostředí neexistuje instalace ATA, stáhněte si úplnou verzi ATA, která zahrnuje verzi 1.7, a použijte standardní postup instalace popsaný v tématu [Instalace ATA](/advanced-threat-analytics/deploy-use/install-ata).

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

### Krok 1: Aktualizace ATA Center

1.  Zazálohujte svou databázi: (volitelné)

    -   Pokud ATA Center běží jako virtuální počítač a chcete pořídit kontrolní bod, ukončete nejprve virtuální počítač.

    -   Pokud ATA Center běží na fyzickém serveru, postupujte podle doporučeného postupu [zálohování MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Spusťte instalační soubor **Microsoft ATA Center Setup.exe** a nainstalujte aktualizaci podle pokynů na obrazovce.

    -  Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**.

    -  Pokud jste ve verzi 1.6 nepovolili automatické aktualizace, zobrazí se výzva, abyste k zajištění aktuálnosti ATA používali službu Microsoft Update.  Na stránce služby Microsoft Update zaškrtněte **Při kontrole aktualizací použít službu Microsoft Update (doporučeno)**.
    ![Obrázek zajištění aktuálnosti ATA](media/ata_ms_update.png) Tímto způsobem se upraví nastavení Windows tak, aby povolovala aktualizace pro ostatní produkty Microsoftu (včetně ATA). 
     ![Obrázek automatické aktualizace Windows](media/ata_installupdatesautomatically.png)

    -  Na obrazovce **Migrace dat** určete, jestli chcete provést migraci všech dat nebo jejich části. Pokud budete chtít migrovat pouze částečná data, nepřesunou se dříve zaznamenané síťové přenosy a profily chování. To znamená, že bude trvat tři týdny, než bude mít detekce neobvyklého chování k dispozici kompletní profil, který umožní zjišťování neobvyklé aktivity. Během těchto tří týdnů budou všechny ostatní funkce detekce ATA fungovat správně. **Částečná** migrace dat trvá mnohem kratší dobu. Pokud si vyberete **úplnou** migraci dat, může dokončení instalace trvat podstatně déle. Odhadovaná doba a požadované místo na disku, které jsou uvedeny na obrazovce **Migrace dat**, závisí na objemu dříve zaznamenaného síťového provozu uloženého v předchozích verzích ATA. Před výběrem **Částečné** nebo **Úplné** migrace zkontrolujte tyto požadavky.  
    
    ![Migrace dat ATA](media/migration data migration.png)

    -  Klikněte na **Aktualizovat**. Po klepnutí na Aktualizovat bude ATA až do dokončení aktualizace offline.

4.  Po úspěšném dokončení aktualizace ATA Center klikněte na tlačítko **Spustit** a na konzole ATA pro komponenty ATA Gateway otevřete obrazovku **Aktualizace**.
    ![Obrazovka Úspěšná aktualizace](media/migration center success.png)

5.  Na obrazovce **Aktualizace** se ATA Gateway teď aktualizují (pokud jste již nastavili automatické aktualizace). V opačném případě klikněte na tlačítko **Aktualizovat** vedle každé ATA Gateway.
  ![Obrázek aktualizace bran](media/migration update gw.png)

  
> [!IMPORTANT] 
> Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.
> Nakonfigurovaný port naslouchacího procesu Syslog se u všech bran změní na 514.
 
> [!NOTE] 
> Pokud chcete nainstalovat nové brány ATA Gateway, přejděte na obrazovku **Brány** a klikněte na **Stáhnout instalační program brány**. Stáhne se instalační balíček pro ATA 1.7. Dále postupujte podle pokynů k instalaci nové brány, jak je popisuje [Krok 4. Instalace ATA Gateway](/advanced-threat-analytics/deploy-use/install-ata-step4).



## Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Oct16_HO3-->


