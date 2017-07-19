---
title: "Instalace Advanced Threat Analytics – krok 1 | Dokumentace Microsoftu"
description: "První krok instalace ATA představuje stažení a instalaci ATA Center na vybraný server."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 97fa1522ca43cf92416ac845b8886f2905e9981b
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/03/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*


# <a name="install-ata---step-1"></a>Instalace ATA – krok 1

>[!div class="step-by-step"]
[Krok 2 »](install-ata-step2.md)

Tento postup instalace obsahuje pokyny pro novou instalaci ATA 1.8. Informace o aktualizaci stávajícího nasazení ATA ze starší verze najdete v [průvodci migrací ATA pro verzi 1.8](ata-update-1.8-migration-guide.md).

> [!IMPORTANT] 
> Pokud používáte Windows 2012 R2, můžete před začátkem instalace nainstalovat na server ATA Center a na servery ATA Gateway aktualizaci KB2934520, jinak instalace ATA tuto aktualizaci nainstaluje a bude vyžadovat restart uprostřed instalace ATA.

## <a name="step-1-download-and-install-the-ata-center"></a>Krok 1: Stažení a instalace ATA Center
Po ověření, že server splňuje požadavky, můžete pokračovat v instalaci ATA Center.
    
> [!NOTE]
>Pokud jste licenci na Microsoft Enterprise Mobility + Security (EMS) pořídili přímo přes portál Office 365 nebo prostřednictvím licenčního modelu partnera cloudových řešení (CSP) a nemáte k ATA přístup přes centrum multilicencí Microsoftu (VLSC), požádejte zákaznickou podporu Microsoftu o zpracování aktivace řešení ATA (Advanced Threat Analytics).

Na serveru ATA Center proveďte tento postup.

1.  Stáhněte si ATA z webu [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx), [TechNet Evaluation Center](http://www.microsoft.com/evalcenter/) nebo [MSDN](https://msdn.microsoft.com/subscriptions/downloads).

2.  K počítači, do kterého instalujete ATA Center, se přihlaste jako uživatel, který je členem místní skupiny Administrators.

3.  Spusťte **Microsoft ATA Center Setup.EXE** a postupujte podle pokynů průvodce instalací.

> [!NOTE]   
> Ujistěte se, že jste instalační soubor spustili z místního disku, nikoli z připojeného souboru ISO. Vyhnete se tak potížím v případě, že by se v rámci instalace vyžadovalo restartování.   

4.  Pokud není nainstalované rozhraní Microsoft .Net Framework, budete před zahájením instalace vyzváni, abyste ho nainstalovali. Po dokončení instalace rozhraní .NET Framework se může zobrazit výzva k restartování.
5.  Na **Vítejte** vyberte jazyk, který chcete použít pro instalační obrazovky ATA, a klikněte na tlačítko **Další**.

6.  Přečtěte si Licenční podmínky pro software společnosti Microsoft a pokud je přijímáte, zaškrtněte příslušné políčko a potom klikněte na tlačítko **Další**.

7.  Doporučuje se nastavit řešení ATA tak, aby se aktualizovalo automaticky. Pokud systém Windows na vašem počítači není na automatické aktualizace nastavený, zobrazí se obrazovka **Pomocí služby Microsoft Update zajistit, aby byl počítač zabezpečen a aktuální**. 
    ![Obrázek zajištění aktuálnosti ATA](media/ata_ms_update.png)

8. Vyberte **Při vyhledávání aktualizací použít službu Microsoft Update (doporučeno)**. Tímto způsobem se upraví nastavení Windows tak, aby povolovala aktualizace pro ostatní produkty Microsoftu (včetně ATA). 

    ![Obrázek automatické aktualizace Windows](media/ata_installupdatesautomatically.png)

8.  Na stránce **Konfigurace centra** zadejte následující informace podle svého prostředí:

    |Pole|Popis|Komentáře|
    |---------|---------------|------------|
    |Instalační cesta|To je umístění, kam se ATA Center nainstaluje. Ve výchozím nastavení to je %programfiles%\Microsoft Advanced Threat Analytics\Center.|Ponechte výchozí hodnotu.|
    |Cesta k datům databáze|Toto je umístění, kde budou umístěné soubory databáze MongoDB. Ve výchozím nastavení to je %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data.|Změňte umístění na místo, kde existuje místo pro růst v závislosti na vaší velikosti. **Poznámka:** <ul><li>V produkčních prostředích byste měli používat jednotku, která má dostatek volného místa na základě plánování kapacity.</li><li>U rozsáhlých nasazení by měla být databáze umístěná na samostatném fyzickém disku.</li></ul>Informace o velikosti najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md).|
    |Certifikát SSL služby Center|To je certifikát, který bude konzola ATA a služba ATA Center používat.|Klikněte na ikonu klíče a vyberte nainstalovaný certifikát, nebo při nasazení v testovacím prostředí zaškrtněte certifikát podepsaný svým držitelem. Máte možnost si certifikát podepsaný svým držitelem vytvořit.|
        
    ![Obrázek konfigurace ATA Center](media/ATA-Center-Configuration.png)

10.  Kliknutím na **Instalovat** nainstalujete ATA Center a všechny jeho komponenty.
    Během instalace ATA Center se instalují a konfigurují následující komponenty:

    -   Služba ATA Center

    -   MongoDB

    -   Vlastní sada kolekcí dat Sledování výkonu

    -   Certifikáty podepsané svým držitelem (pokud došlo k výběru během instalace)

11.  Po dokončení instalace otevřete kliknutím na **Spustit** konzolu ATA a dokončete instalaci na stránce **Konfigurace**.
Nyní automaticky přejdete na stránku nastavení **Obecné**, abyste pokračovali v konfiguraci a nasazení komponent ATA Gateway.
Protože se k webu přihlašujete pomocí IP adresy, zobrazí se upozornění související s certifikátem. To je normální a měli byste kliknout na **Pokračovat na tento web**.

### <a name="validate-installation"></a>Ověření instalace

1.  Zkontrolujte, že je služba **Microsoft Advanced Threat Analytics Center** spuštěná.
2.  Na ploše klikněte na zástupce **Microsoft Advanced Threat Analytics** a připojte se ke konzole ATA. Přihlaste se pomocí stejných přihlašovacích údajů, které jste použili k instalaci ATA Center.



>[!div class="step-by-step"]
[« Předinstalace](configure-port-mirroring.md)
[Krok 2 »](install-ata-step2.md)

## <a name="see-also"></a>Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

