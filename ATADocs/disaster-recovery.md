---
title: "Zotavení po havárii pro Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Popisuje, jak můžete po havárii rychle obnovit funkce ATA."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/26/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7620e171-76d5-4e3f-8b03-871678217a3a
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 819f006ae89960ed8f9494ce36ba4fd7f120357a
ms.sourcegitcommit: 5563c6861bb5db5cb73e058e5a51b4938b9a7d46
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="ata-disaster-recovery"></a>Zotavení po havárii ATA
Tento článek popisuje postup rychlého zotavení komponenty ATA Center a obnovení funkcí ATA v případě, kdy přijdete o funkce ATA Center, ale komponenty ATA Gateways dále fungují. 

>[!NOTE]
> Popsaný postup neobnoví dříve detekované podezřelé aktivity, ale vrátí komponentě ATA Center plnou funkčnost. Také dojde k restartování období učení potřebného pro některé detekce chování, ale většina detekcí nabízených ATA je po zotavení komponenty ATA Center funkční. 

## <a name="back-up-your-ata-center-configuration"></a>Zazálohování konfigurace ATA Center

1. Konfigurace ATA Center se každou hodinu zálohuje do souboru. Vyhledejte nejnovější záložní kopii konfigurace ATA Center a uložte ji na oddělený počítač. Úplné vysvětlení postupu vyhledání těchto souborů najdete v části [Export a import konfigurace ATA](ata-configuration-file.md). 
2. Vyexportujte certifikát ATA Center.
    1. Ve správci certifikátů přejděte na **Certifikáty (místní)** -> **Osobní** ->**Certifikáty** a vyberte **ATA Center**.
    2. Pravým tlačítkem myši klikněte na **ATA Center** a vyberte **Všechny úkoly** a potom **Exportovat**. 
     ![Certifikát ATA Center](media/ata-center-cert.png)
    3. Postupujte podle pokynů pro export certifikátu a nezapomeňte vyexportovat také privátní klíč.
    4. Vyexportovaný soubor certifikátu zazálohujte na oddělený počítač.

  > [!NOTE] 
  > Pokud privátní klíč exportovat nejde, musíte vytvořit nový certifikát a nasadit ho do ATA podle postupu uvedeného v části [Změna certifikátu ATA Center](modifying-ata-center-configuration#the-ata-center-certificate). Pak ho vyexportujte. 

## <a name="recover-your-ata-center"></a>Obnovení vašeho ATA Center

1. Pomocí stejné IP adresy a názvu, jaké měl předchozí počítač ATA Center, vytvořte nový počítač s Windows Serverem.
4. Na nový server naimportujte certifikát, který jste zazálohovali výše.
5. Na nově vytvořeném Windows Serveru postupujte podle pokynů pro [Nasazení ATA Center](install-ata-step1.md). ATA Gateways není potřeba znovu nasazovat. Po zobrazení výzvy k zadání certifikátu zadejte certifikát, který jste vyexportovali při zálohování konfigurace ATA Center. 
![Obnovení ATA Center](media/disaster-recovery-deploymentss.png)
6. Naimportujte zazálohovanou konfiguraci ATA Center:
    1. Z MongoDB odeberte výchozí dokument profilu systému ATA Center: 
        1. Přejděte na **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**. 
        2. Spusťte `mongo.exe ATA` 
        3. Spuštěním tohoto příkazu odeberte výchozí systémový profil: `db.SystemProfile.remove({})`
    2. Spusťte příkaz `mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert` s použitím záložního souboru z kroku 1.</br>
    Úplné vysvětlení postupu vyhledání a importu záložních souborů najdete v části [Export a import konfigurace ATA](ata-configuration-file.md). 
    3. Otevřete konzolu ATA. Všechny komponenty ATA Gateways byste měli vidět propojené na kartě Konfigurace/Brány. 
    5. Nezapomeňte definovat [**uživatele adresářových služeb**](install-ata-step2.md) a zvolit [**synchronizátor řadiče domény**](install-ata-step5.md). 






## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](install-ata-step6.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
