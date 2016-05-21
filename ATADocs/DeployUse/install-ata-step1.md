---
# required metadata

title: Instalace ATA – Krok 1 | Microsoft Advanced Threat Analytics
description: První krok instalace ATA představuje stažení a instalaci ATA Center na vybraný server.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalace ATA – Krok 1

>[!div class="step-by-step"]
[« Předinstalační kroky](install-ata-preinstall.md)
[Krok 2 »](install-ata-step2.md)

## Krok 1: Stažení a instalace ATA Center
Po ověření, že server splňuje požadavky, můžete pokračovat v instalaci ATA Center.

Na serveru ATA Center proveďte tento postup.

1.  Stáhněte ATA z webu [TechNet Evaluation Center](http://www.microsoft.com/en-us/evalcenter/)..

2.  Přihlaste se pomocí uživatele, který je členem místní skupiny Administrators.

3.  Z příkazového řádku se zvýšenými oprávněními spusťte soubor Microsoft ATA Center Setup.EXE a postupujte podle pokynů průvodce instalací.

4.  Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**..

5.  Přečtěte si licenční smlouvou s koncovým uživatelem, a pokud s podmínkami souhlasíte, klikněte na **Další**..

6.  Na stránce **Center Configuration** (Konfigurace ATA Center) zadejte následující informace podle vašeho prostředí:

    |Pole|Popis|Komentáře|
    |---------|---------------|------------|
    |Instalační cesta|To je umístění, kam se ATA Center nainstaluje. Ve výchozím nastavení to je %programfiles%\Microsoft Advanced Threat Analytics\Center.|Ponechte výchozí hodnotu.|
    |Cesta k datům databáze|Toto je umístění, kde budou umístěné soubory databáze MongoDB. Ve výchozím nastavení to je %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data.|Změňte umístění na místo, kde existuje místo pro růst v závislosti na vaší velikosti. **Poznámka:** <ul><li>V produkčních prostředích byste měli používat jednotku, která má dostatek volného místa na základě plánování kapacity.</li><li>U rozsáhlých nasazení by měla být databáze umístěná na samostatném fyzickém disku.</li></ul>Informace o velikosti najdete v tématu [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).|
    |Cesta k deníku databáze|Toto je umístění, kde budou umístěné soubory deníku databáze. Ve výchozím nastavení to je %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data\journal.|Pro rozsáhlá nasazení by deník databáze měl být samostatně na jiném fyzickém disku, než je databáze a systémová jednotka. Změňte umístění na místo, kde je pro deník databáze místo.|
    |IP adresa a port služby ATA Center|Toto je IP adresa, na které bude služba ATA Center naslouchat komunikaci z komponent ATA Gateway.<br /><br />**Výchozí port:** 443|Klikněte na šipku dolů a vyberte IP adresu, kterou má používat služba ATA Center.<br /><br />IP adresa a port služby ATA Center nemůžou být stejné jako IP adresa a port konzoly ATA. Změňte port konzoly ATA.|
    |Certifikát SSL služby ATA Center|To je certifikát, který bude služba ATA Center používat.|Klikněte na ikonu klíče a vyberte nainstalovaný certifikát, nebo při nasazení v testovacím prostředí zaškrtněte certifikát podepsaný svým držitelem.|
    |IP adresa konzoly ATA|Toto je IP adresa, která se použije pro konzolu ATA službou IIS.|Klikněte na šipku dolů a vyberte IP adresu používanou konzolou ATA. **Poznámka:** Poznamenejte si tuto IP adresu, aby bylo snazší přistupovat ke konzole ATA z ATA Gateway.|
    |Certifikát SSL konzoly ATA|Toto je certifikát pro použití službou IIS.|Klikněte na ikonu klíče a vyberte nainstalovaný certifikát, nebo při nasazení v testovacím prostředí zaškrtněte certifikát podepsaný svým držitelem.|
    ![Obrázek konfigurace ATA Center](media/ATA-Center-Configuration.JPG)

7.  Kliknutím na **Nainstalovat** nainstalujete software ATA a jeho komponenty a vytvoříte připojení mezi komponentami ATA Center a ATA Gateway.

8.  Po dokončení instalace se kliknutím na **Spustit** připojte ke konzole ATA.

    Během instalace ATA Center se instalují a konfigurují následující komponenty:

    -   Internetová informační služba (IIS)

    -   MongoDB

    -   Služba ATA Center a web IIS konzoly ATA

    -   Vlastní sada kolekcí dat Sledování výkonu

    -   Certifikáty podepsané svým držitelem (pokud došlo k výběru během instalace)

> [!NOTE]
> Kvůli usnadnění řešení problémů a vylepšení produktu doporučujeme nainstalovat MongoVue a jakýkoli další doplněk MongoDB, případně jakýkoli jiný nástroj třetí strany podle vašeho výběru. MongoVue vyžaduje instalaci .Net Framework 3.5.

### Ověření instalace

1.  Zkontrolujte, že je služba Microsoft Advanced Threat Analytics Center spuštěná.

2.  Na ploše klikněte na zástupce Microsoft Advanced Threat Analytics a připojte se ke konzole ATA. Přihlaste se pomocí stejných přihlašovacích údajů, které jste použili k instalaci ATA Center. Při prvním přihlášení ke konzole ATA můžete automaticky přejít na stránku **Nastavení připojení k doméně**, abyste pokračovali v konfiguraci a nasazení komponent ATA Gateway.

3.  Prohlédněte si soubor chyb **Microsoft.Tri.Center-Errors.log**, který se nachází v následujícím výchozím umístění: %programfiles%\Microsoft Advanced Threat Analytics\Center\Logs.

>[!div class="step-by-step"]
[« Předinstalační kroky](install-ata-preinstall.md)
[Krok 2 »](install-ata-step2.md)

## Viz také

- [Podporu získáte na našem fóru!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurace shromažďování událostí](/advanced-threat-analytics/plan-design/configure-event-collection)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=Apr16_HO4-->


