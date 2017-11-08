---
title: "Průvodce migrací pro aktualizaci Advanced Threat Analytics na verzi 1.8 | Dokumentace Microsoftu"
description: Postupy aktualizace ATA na verzi 1.8
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/20/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e5a9718c-b22e-41f7-a614-f00fc4997682
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 540d1cb0754dc9191a985625a8f988cb44c9f000
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/07/2017
---
# <a name="updating-ata-to-version-18"></a>Aktualizace ATA na verzi 1.8

> [!NOTE] 
> Pokud ve vašem prostředí neexistuje instalace ATA, stáhněte si úplnou verzi ATA, která zahrnuje verzi 1.8 a použijte standardní postup instalace popsaný v [instalace ATA](install-ata-step1.md).

Pokud již máte ATA verze 1.7 nasazen, tento postup vás provede kroky potřebnými k aktualizaci vašeho nasazení.

> [!NOTE] 
>  Na verzi 1.8 je možné aktualizovat jen verze ATA 1.7 Update 1 a 1.7 Update 2. Žádné předchozí verze ATA nelze na verzi ATA 1.8 aktualizovat přímo.

Podle těchto kroků provedete aktualizaci ATA na verzi 1.8:

1.  [Stáhněte aktualizační verzi ATA 1.8 z webu Download Center](https://www.microsoft.com/download/details.aspx?id=55536) nebo úplnou verzi z [centra vyhodnocení](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
V migrační verzi lze soubor použít pouze k aktualizaci z verze ATA 1.7. Ve verzi z centra vyhodnocení se stejný instalační soubor (Microsoft ATA Center Setup.exe) používá jak k instalaci a novému nasazení ATA, tak k upgradu existujících nasazení.

2.  Aktualizace ATA Center

4.  Aktualizace komponent ATA Gateway

    > [!IMPORTANT]
    > Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.

### <a name="step-1-update-the-ata-center"></a>Krok 1: Aktualizace ATA Center

1.  Zazálohujte svou databázi: (volitelné)

    -   Pokud ATA Center běží jako virtuální počítač a chcete pořídit kontrolní bod, nejprve vypnout virtuální počítač.

    -   Pokud ATA Center běží na fyzickém serveru, najdete informace o zálohování databáze v článku [Zotavení po havárii](disaster-recovery.md).

2.  Spusťte instalační soubor **Microsoft ATA Center Setup.exe** a nainstalujte aktualizaci podle pokynů na obrazovce.

    -  Na **uvítací** stránce si zvolte jazyk a klikněte na **Další**.

    -  Pokud povolíte nebylo automatické aktualizace ve verzi 1.7, zobrazí se výzva k nastavení použít službu Microsoft Update pro ATA k zajištění aktuálnosti ATA.  Na stránce služby Microsoft Update zaškrtněte **Při kontrole aktualizací použít službu Microsoft Update (doporučeno)**.
    ![Zachovat aktuální obrázek ATA](media/ata_ms_update.png)
     
     To se upraví nastavení Windows tak, aby povolovala aktualizace pro ATA. 
    
    -  Na obrazovce **Migrace dat** určete, jestli chcete migrovat všechna data nebo částečná data. Pokud zvolíte možnost migrovat pouze částečná data, všechna nalezení okamžitě pracovat s výjimkou zjišťování neobvyklé chování, která přebírá tři týdny k sestavení celého profilu.  
    
    **Částečná** migrace dat se instaluje mnohem kratší dobu. Pokud si vyberete **úplnou** migraci dat, může dokončení instalace trvat podstatně déle. Nezapomeňte se podívat na odhadovanou dobu a požadované místo na disku, které jsou uvedené na obrazovce **Migrace dat**. Tyto údaje závisejí na množství dříve zachyceného síťového provozu, který jste uložili do předchozích verzí ATA. Například na obrazovce níže můžete vidět migraci dat z velké databáze:
         
    ![Migrace dat ATA](media/migration-data-migration.png)

    -  Klikněte na **Aktualizovat**. Po klepnutí na Aktualizovat bude ATA až do dokončení aktualizace offline.

4.  Po úspěšném dokončení aktualizace ATA Center klikněte na tlačítko **Spustit** a na konzole ATA pro komponenty ATA Gateway otevřete obrazovku **Aktualizace**.

    ![Obrazovka Úspěšná aktualizace](media/migration-center-success.png)

5.  V **aktualizace** obrazovky, pokud jste již nastavili vašich komponent ATA Gateway k automatické aktualizaci, jejich aktualizace v tomto okamžiku, v opačném případě klikněte na tlačítko **aktualizace** vedle každé komponenty ATA Gateway.
  
![Obrázek aktualizace bran](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.
 
> [!NOTE] 
> Pokud chcete nainstalovat nové komponenty ATA Gateway, přejděte na obrazovku **Brány** a klikněte na **Stáhnout instalační program brány**. Stáhne se instalační balíček ATA 1.8 Gateway. Dále postupujte podle pokynů k instalaci nové brány, jak je popisuje [Krok 4: Instalace ATA Gateway](install-ata-step4.md).


## <a name="see-also"></a>Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
