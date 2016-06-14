---
# required metadata

title: Instalace ATA – Krok 4 | Microsoft Advanced Threat Analytics
description: Čtvrtý krok instalace ATA vám pomůže s instalací ATA Gateway.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalace ATA – Krok 4

>[!div class="step-by-step"]

## « Krok 3 Krok 5 »

Krok 4. Instalace ATA Gateway


> [!IMPORTANT]
> Před instalací ATA Gateway na vyhrazený server ověřte, že je zrcadlení portů správně nakonfigurované a že ATA Gateway vidí provoz do a z řadičů domény.  Další informace najdete v tématu [Ověření zrcadlení portů](validate-port-mirroring.md).
>
> `Get-HotFix -Id kb2919355`

Ujistěte se, že je nainstalovaná aktualizace [KB2919355](http://support.microsoft.com/kb/2919355/).

1.  Kontrolu instalace opravy hotfix můžete provést spuštěním následující rutiny PowerShellu: 
> [!NOTE] Na serveru ATA Gateway proveďte tento postup.

2.  Extrahujte soubory ze souboru zip.

3.  Instalace přímo ze souboru zip selže.

4.  Z příkazového řádku se zvýšenými oprávněními spusťte soubor **Microsoft ATA Gateway Setup.exe** a postupujte podle pokynů průvodce instalací.

    ![Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**.](media/ATA-Gateway-Configuration.JPG)

    |V části **Konfigurace ATA Gateway** zadejte následující informace podle vašeho prostředí:|Obrázek konfigurace ATA Gateway|Pole|
    |---------|---------------|------------|
    |Popis|Komentáře Instalační cesta|To je umístění, kam se ATA Gateway nainstaluje.|
    |Ve výchozím nastavení to je %programfiles%\Microsoft Advanced Threat Analytics\Gateway.|Ponechte výchozí hodnotu.|Certifikát SSL služby ATA Gateway|
    |To je certifikát, který bude ATA Gateway používat.|Certifikát podepsané svým držitelem používejte jenom pro testovací prostředí.|Registrace ATA Gateway Zadejte uživatelské jméno a heslo správce ATA.<br /><br />Aby se služba ATA Gateway registrovala v ATA Center, zadejte uživatelské jméno a heslo pro uživatele, který instaloval ATA Center.<br />Tento uživatel musí být členem jedné z následujících místních skupin v ATA Center.|
    -   Správci

    -   -   Správci Microsoft Advanced Threat Analytics **Poznámka:** Tyto přihlašovací údaje se používají jenom pro registraci a neukládají se v ATA.

        > [!IMPORTANT]
        > -   Během instalace ATA Gateway se instalují a konfigurují následující komponenty: KB 3047154 
        > -   Neinstalujte KB 3047154 na hostiteli virtualizace (na hostiteli, na kterém je spuštěná virtualizace, spuštění na virtuálním počítači je v pořádku). Může způsobit, že zrcadlení portů přestane fungovat správně.

    -   Neinstalujte na komponentu ATA Gateway Message Analyzer, Wireshark nebo jiný software pro zachycení dat ze sítě.

    -   Pokud potřebujete zachycovat síťový provoz, nainstalujte a používejte Microsoft Network Monitor 3.4.

    -   Služba ATA Gateway

5.  Microsoft Visual C++ 2013 Redistributable


>Vlastní sada kolekcí dat Sledování výkonu

## Po dokončení instalace pro ATA Gateway kliknutím na **Spustit** otevřete prohlížeč a přihlaste se ke konzole ATA. V případě ATA Lightweight Gateway klikněte na **Dokončit**.

- [[!div class="step-by-step"]](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [« Krok 3](configure-event-collection.md)
- [Krok 5 »](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jun16_HO1-->


