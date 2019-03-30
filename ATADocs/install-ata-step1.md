---
title: Instalace Advanced Threat Analytics – krok 1 | Dokumentace Microsoftu
description: První krok instalace ATA představuje stažení a instalaci ATA Center na vybraný server.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/07/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7ff9f08ca231f64076e29250ae8d09f192d8cf4e
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674567"
---
# <a name="install-ata---step-1"></a>Instalace ATA – krok 1

*Platí pro: Advanced Threat Analytics verze 1.9*

> [!div class="step-by-step"]
> [Krok 2 »](install-ata-step2.md)


Tento instalační postup uvádí pokyny pro novou instalaci ATA 1.9. Informace o aktualizaci stávajícího nasazení ATA ze starší verze najdete v tématu [Průvodci migrací ATA pro verze 1.9](ata-update-1.9-migration-guide.md).

> [!IMPORTANT] 
> Pokud používáte Windows 2012 R2, aktualizaci KB2934520 můžete nainstalovat na server ATA Center a na serverech ATA Gateway před začátkem instalace, jinak instalace ATA tuto aktualizaci nainstaluje a vyžaduje restart uprostřed instalace ATA.

## <a name="step-1-download-and-install-the-ata-center"></a>Krok 1. Stažení a instalace ATA Center
Po ověření, že server splňuje požadavky, můžete pokračovat v instalaci ATA Center.
    
> [!NOTE]
>Pokud jste získali licenci pro Enterprise Mobility + Security (EMS) přímo přes portál Microsoft 365 nebo prostřednictvím licenčního modelu partnera CSP (Cloud Solution) a nemáte přístup k ATA prostřednictvím Microsoft Volume Licensing Center (VLSC), obraťte se na Zákaznická podpora Microsoftu získat zpracování aktivace Advanced Threat Analytics (ATA).

Na serveru ATA Center proveďte tento postup.

1.  Stáhněte si ATA z webu [Microsoft Volume Licensing Service Center](https://www.microsoft.com/Licensing/servicecenter/default.aspx), [TechNet Evaluation Center](http://www.microsoft.com/evalcenter/) nebo [MSDN](https://msdn.microsoft.com/subscriptions/downloads).

2.  Přihlaste se k počítači, do kterého instalujete ATA Center jako uživatel, který je členem místní skupiny administrators.

3.  Spusťte **Microsoft ATA Center Setup.EXE** a postupujte podle pokynů průvodce instalací.

> [!NOTE]   
> Ujistěte se, že jste instalační soubor spustili z místního disku, nikoli z připojeného souboru ISO. Vyhnete se tak potížím v případě, že by se v rámci instalace vyžadovalo restartování.   

4. Pokud není nainstalované rozhraní Microsoft .net Framework, zobrazí se výzva k jeho instalaci, když spustíte instalaci. Po dokončení instalace rozhraní .NET Framework se může zobrazit výzva k restartování.
5. Na **Vítejte** vyberte jazyk, který chcete použít pro instalační obrazovky ATA, a klikněte na tlačítko **Další**.

6. Přečtěte si licenční podmínky softwaru společnosti Microsoft po přijetí podmínek, klikněte na zaškrtávací políčko pro přijetí a potom klikněte na **Další**.

7. Doporučujeme nastavit řešení ATA možnost automaticky aktualizovat. Pokud Windows není nastavena automaticky aktualizovat v počítači, zobrazí se vám **pomocí Microsoft Update zajistit, aby byl váš počítač, zabezpečené a aktuální** obrazovky. 
   ![Obrázek zajištění aktuálnosti ATA](media/ata_ms_update.png)

8. Vyberte **Při vyhledávání aktualizací použít službu Microsoft Update (doporučeno)**. Tím se upraví nastavení Windows tak, aby povolovala aktualizace pro ostatní produkty Microsoftu (včetně ATA). 

    ![Obrázek automatické aktualizace Windows](media/ata_installupdatesautomatically.png)

9. Na stránce **Konfigurace centra** zadejte následující informace podle svého prostředí:

   |Pole|Popis|Komentáře|
   |---------|---------------|------------|
   |Instalační cesta|Toto je umístění, kde je nainstalován na ATA Center. Ve výchozím nastavení to je %programfiles%\Microsoft Advanced Threat Analytics\Center|Ponechte výchozí hodnotu.|
   |Cesta k datům databáze|Toto je umístění, kde jsou uložené soubory databáze MongoDB. Ve výchozím nastavení to je %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data.|Změňte umístění na místo, kde existuje místo pro růst v závislosti na vaší velikosti. **Poznámka:** <ul><li>V produkčním prostředí měli používat jednotku, která má dostatek místa na základě plánování kapacity.</li><li>U rozsáhlých nasazení by měla být databáze umístěná na samostatném fyzickém disku.</li></ul>Informace o velikosti najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md).|
   |Certifikát SSL služby Center|Jedná se o certifikát, který je používán službou konzole ATA a komponenty ATA Center.|Klikněte na ikonu klíče a vyberte nainstalovaný certifikát nebo vytvořit certifikát podepsaný svým držitelem pomocí zaškrtávacího políčka.|
        
   ![Obrázek konfigurace ATA Center](media/ATA-Center-Configuration.png)

> [!NOTE]   
> Ujistěte se, že je potřeba věnovat pozornost monitorování výstrahy týkající se upozornění stavu a vypršení platnosti certifikátu SSL služby Center. Pokud platnost certifikátu vyprší, bude nutné zcela konfiguraci znovu nasaďte ATA. 

10. Kliknutím na **Instalovat** nainstalujete ATA Center a všechny jeho komponenty.
   Během instalace ATA Center se instalují a konfigurují následující komponenty:

   -   Služba ATA Center

   -   MongoDB

   -   Vlastní sada kolekcí dat Sledování výkonu

   -   Certifikáty podepsané svým držitelem (pokud došlo k výběru během instalace)

11. Po dokončení instalace klikněte na tlačítko **spuštění** otevřete konzolu ATA a dokončete instalaci z **konfigurace** stránky.
   **Obecné** nastavení stránka se otevře automaticky pokračovat v konfiguraci a nasazení komponent ATA Gateway.
   Vzhledem k tomu, že se přihlašujete na web pomocí IP adresy, zobrazí se upozornění související s certifikátem, to je normální a měli byste kliknout na **pokračovat na tento web**.

### <a name="validate-installation"></a>Ověření instalace

1.  Zkontrolujte, zda služba **Microsoft Advanced Threat Analytics Center**, běží.
2.  Na ploše klikněte na zástupce **Microsoft Advanced Threat Analytics** a připojte se ke konzole ATA. Přihlaste se pomocí přihlašovacích údajů uživatele, který jste použili k instalaci ATA Center.

### <a name="set-anti-virus-exclusions"></a>Nastavte antivirový program výjimky

Po instalaci komponenty ATA Center, vyloučíte adresáře databáze MongoDB z je průběžně skenovalo antivirové aplikace. Výchozím umístěním databáze je: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data**.

Ujistěte se, že mají také vyloučit následující složky a procesy z kontroly antivirová ochrana v programu:

**Folders** C:\Program Files\Microsoft Advanced Threat Analytics\Center\ParentKerberosAsBloomFilters
<br>C:\Program Files\Microsoft Advanced Threat Analytics\Center\ParentKerberosTgsBloomFilters
<br>C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup
<br>C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs

**Procesy**
<br>mongod.exe
<br>Microsoft.Tri.Center.exe


Pokud jste nainstalovali ATA v jiném adresáři, ujistěte se, že chcete-li změnit cesty složky podle vaší instalaci. 

> [!div class="step-by-step"]
> [« Předinstalace](configure-port-mirroring.md)
> [Krok 2 »](install-ata-step2.md)

## <a name="related-videos"></a>Související videa
- [Volba správného typu komponenty ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)


## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

