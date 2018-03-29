---
title: Advanced Threat Analytics aktualizace na Průvodce migrací 1,9 | Microsoft Docs
description: Postupy aktualizace ATA na verzi 1.9
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 03/25/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0bd4bca536facb9ad4b7fea627f2ef512949728e
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
# <a name="updating-ata-to-version-19"></a>Aktualizace ATA na verzi 1.9

> [!NOTE] 
> Pokud ve vašem prostředí neexistuje instalace ATA, stáhněte si úplnou verzi ATA, která zahrnuje verzi 1.9 a použijte standardní postup instalace popsaný v [instalace ATA](install-ata-step1.md).

Pokud již máte ATA verze 1.8 nasazen, tento postup vás provede kroky potřebnými k aktualizaci vašeho nasazení.

> [!NOTE] 
>  Pouze ATA verze 1.8 (1.8.6645) a aktualizace ATA 1.8 1 (1.8.6765) mohou být aktualizovány na ATA verze 1.9, ATA na verzi 1.9 nelze přímo aktualizovat všechny předchozí verze ATA.

Postupujte podle těchto kroků provedete aktualizaci ATA na verzi 1.9:

1.  [Stáhnout aktualizovanou verzi ATA 1.9 z webu Stažení softwaru](https://www.microsoft.com/download/details.aspx?id=56725) nebo na plnou verzi z [Eval center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
Ve verzi migrace soubor slouží pouze pro aktualizaci z ATA 1.8. Ve verzi z centra vyhodnocení se stejný instalační soubor (Microsoft ATA Center Setup.exe) používá jak k instalaci a novému nasazení ATA, tak k upgradu existujících nasazení.

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

    -  Pokud povolíte nebylo automatické aktualizace v verze 1.8, zobrazí se výzva k nastavení použít službu Microsoft Update pro ATA k zajištění aktuálnosti ATA.  Na stránce služby Microsoft Update zaškrtněte **Při kontrole aktualizací použít službu Microsoft Update (doporučeno)**.
    ![Zachovat aktuální obrázek ATA](media/ata_ms_update.png)
     
     To se upraví nastavení Windows tak, aby povolovala aktualizace pro ATA. 
    
    -  **Částečná data migrace** obrazovky vám oznamuje, že dříve zaznamenaný síťový provoz, události, entit a detekce související data se odstraní. Všechna nalezení okamžitě pracovat s výjimkou zjišťování neobvyklé chování, neobvyklé skupiny změnách, Rekognoskace používání adresářových služeb (SAM-R) a detekce přechod na starší verzi šifrování, které trvat až tři týdny k vytvoření profilu po dokončení požadované learning čas. 
     
      ![Částečná migrace ATA](media/partial-migration.png)

    -  Klikněte na **Aktualizovat**. Po klepnutí na Aktualizovat bude ATA až do dokončení aktualizace offline.

4.  Po úspěšném dokončení aktualizace ATA Center klikněte na tlačítko **Spustit** a na konzole ATA pro komponenty ATA Gateway otevřete obrazovku **Aktualizace**.

     ![Obrazovka Úspěšná aktualizace](media/migration-center-success.png)

5.  V **aktualizace** obrazovky, pokud jste již nastavili vašich komponent ATA Gateway k automatické aktualizaci, jejich aktualizace v tomto okamžiku, v opačném případě klikněte na tlačítko **aktualizace** vedle každé komponenty ATA Gateway.
  
     ![Obrázek aktualizace bran](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.
 
> [!NOTE] 
> K instalaci nových komponent ATA Gateway, přejděte **brány** obrazovky a klikněte na tlačítko **stáhnout instalační program brány** získat instalační balíček ATA 1.9 Gateway a postupujte podle pokynů pro novou instalaci brány jako popsané v [kroku 4. Instalace ATA Gateway](install-ata-step4.md).


## <a name="see-also"></a>Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
