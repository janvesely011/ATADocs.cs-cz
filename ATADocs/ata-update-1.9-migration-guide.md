---
title: Aktualizaci Advanced Threat Analytics na Průvodce migrací 1.9 | Dokumentace Microsoftu
description: Postupy aktualizace ATA verze 1.9
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 03/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: bd96cf2b2048aa37e559649d15565c3244684e35
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165995"
---
# <a name="updating-ata-to-version-19"></a>Aktualizace ATA na verzi 1.9

> [!NOTE] 
> Pokud ve vašem prostředí neexistuje instalace ATA, stáhněte si úplnou verzi ATA, která zahrnuje verze 1.9 a postupujte podle pokynů standardní postup instalace popsaný v [instalace ATA](install-ata-step1.md).

Pokud již máte ATA verze 1.8 nasazení, tento postup vás provede kroky potřebnými k aktualizaci vašeho nasazení.

> [!NOTE] 
>  Jenom komponenty ATA verze 1.8 (1.8.6645) a je možné aktualizovat verzi ATA 1.8 update 1 (1.8.6765) na ATA verze 1.9, všechny předchozí verze ATA nelze přímo aktualizovat ATA verze 1.9.

Postupujte podle těchto kroků provedete aktualizaci ATA verze 1.9:

1.  [Stáhněte aktualizační verzi ATA 1.9 ze služby Stažení softwaru](https://www.microsoft.com/download/details.aspx?id=56725) nebo úplnou verzi z [Eval center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
V migrační verzi lze soubor pouze pro aktualizaci z ATA 1.8. Ve verzi z centra vyhodnocení se stejný instalační soubor (Microsoft ATA Center Setup.exe) používá jak k instalaci a novému nasazení ATA, tak k upgradu existujících nasazení.

2.  Aktualizace ATA Center

4.  Aktualizace komponent ATA Gateway

    > [!IMPORTANT]
    > Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.

### <a name="step-1-update-the-ata-center"></a>Krok 1: Aktualizace ATA Center

1.  Zazálohujte svou databázi: (volitelné)

    -   Pokud ATA Center běží jako virtuální počítač a chcete pořídit kontrolní bod, nejdřív vypnout virtuální počítač.

    -   Pokud ATA Center běží na fyzickém serveru, najdete informace o zálohování databáze v článku [Zotavení po havárii](disaster-recovery.md).

2.  Spusťte instalační soubor **Microsoft ATA Center Setup.exe** a nainstalujte aktualizaci podle pokynů na obrazovce.

    -  Na **uvítací** stránce si zvolte jazyk a klikněte na **Další**.

    -  Pokud jste nepovolili automatické aktualizace ve verzi 1.8, zobrazí se výzva, abyste používali službu Microsoft Update k zajištění aktuálnosti ATA.  Na stránce služby Microsoft Update zaškrtněte **Při kontrole aktualizací použít službu Microsoft Update (doporučeno)**.
    ![Zachovat aktuální obrázek ATA](media/ata_ms_update.png)
     
     Tím se upraví nastavení Windows tak, aby povolovala aktualizace pro ATA. 
    
    -  **Částečná data migrace** obrazovky vám umožňuje vědět, že dříve zaznamenané síťové přenosy, události, entit a zjišťování související data se odstraní. Všechna nalezení okamžitě pracovat s výjimkou detekce neobvyklého chování, neobvyklá skupiny změny, Rekognoskace pomocí adresářových služeb (SAM-R) a detekcí oslabení šifrování, které trvat až tři týdny sestavit kompletní profil po požadovaných studijních čas. 
     
      ![ATA částečné migrace](media/partial-migration.png)

    -  Klikněte na **Aktualizovat**. Po klepnutí na Aktualizovat bude ATA až do dokončení aktualizace offline.

4.  Po úspěšném dokončení aktualizace ATA Center klikněte na tlačítko **Spustit** a na konzole ATA pro komponenty ATA Gateway otevřete obrazovku **Aktualizace**.

     ![Obrazovka Úspěšná aktualizace](media/migration-center-success.png)

5.  V **aktualizace** obrazovky, pokud jste již nastavili automatické aktualizace ATA Gateway se aktualizace v tomto okamžiku, v opačném případě klikněte na tlačítko **aktualizovat** vedle každé ATA Gateway.
  
     ![Obrázek aktualizace bran](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Aktualizujte všechny komponenty ATA Gateway, aby se zajistila správná funkce ATA.
 
> [!NOTE] 
> K instalaci nových komponent ATA Gateway, přejděte **brány** obrazovku a klikněte na tlačítko **stáhnout instalační program brány** instalační balíček ATA 1.9 Gateway a postupujte podle pokynů k instalaci nové brány jako popsané v [kroku 4. Instalace ATA Gateway](install-ata-step4.md).


## <a name="see-also"></a>Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
