---
title: "Instalace ATA – Krok 4 | Microsoft Advanced Threat Analytics"
description: "Čtvrtý krok instalace ATA vám pomůže s instalací ATA Gateway."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: f12e43a6918c0c02bb59e4a093720a805b7dbcfc


---

# Instalace ATA – Krok 4

>[!div class="step-by-step"]
[« Krok 3](install-ata-step3.md)
[Krok 5 »](install-ata-step5.md)

## Krok 4. Instalace ATA Gateway

Před instalací ATA Gateway na vyhrazený server ověřte, že je zrcadlení portů správně nakonfigurované a že ATA Gateway vidí provoz do a z řadičů domény. Další informace najdete v tématu [Ověření zrcadlení portů](validate-port-mirroring.md).


> [!IMPORTANT]
> Ujistěte se, že je nainstalovaná aktualizace [KB2919355](http://support.microsoft.com/kb/2919355/).  Kontrolu instalace opravy hotfix můžete provést spuštěním následující rutiny PowerShellu:
>
> `Get-HotFix -Id kb2919355`

Na serveru ATA Gateway proveďte tento postup.

1.  Extrahujte soubory ze souboru zip. 
> [!NOTE] 
> Instalace přímo ze souboru zip selže.

2.  Z příkazového řádku se zvýšenými oprávněními spusťte soubor **Microsoft ATA Gateway Setup.exe** a postupujte podle pokynů průvodce instalací.

3.  Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**.

4.  V části **Konfigurace ATA Gateway** zadejte následující informace podle vašeho prostředí:

    ![Obrázek konfigurace ATA Gateway](media/ATA-Gateway-Configuration.JPG)

    |Pole|Popis|Komentáře|
    |---------|---------------|------------|
    |Instalační cesta|To je umístění, kam se ATA Gateway nainstaluje. Ve výchozím nastavení to je %programfiles%\Microsoft Advanced Threat Analytics\Gateway.|Ponechte výchozí hodnotu.|
    |Certifikát SSL služby ATA Gateway|To je certifikát, který bude ATA Gateway používat.|Certifikát podepsané svým držitelem používejte jenom pro testovací prostředí.|
    |Registrace ATA Gateway|Zadejte uživatelské jméno a heslo správce ATA.|Aby se služba ATA Gateway registrovala v ATA Center, zadejte uživatelské jméno a heslo pro uživatele, který instaloval ATA Center. Tento uživatel musí být členem jedné z následujících místních skupin v ATA Center.<br /><br />-   Správci<br />-   Správci Microsoft Advanced Threat Analytics **Poznámka:** Tyto přihlašovací údaje se používají jenom pro registraci a neukládají se v ATA.|
    Během instalace ATA Gateway se instalují a konfigurují následující komponenty:

    -   KB 3047154

        > [!IMPORTANT]
        > -   Neinstalujte KB 3047154 na hostiteli virtualizace (na hostiteli, na kterém je spuštěná virtualizace, spuštění na virtuálním počítači je v pořádku). Může způsobit, že zrcadlení portů přestane fungovat správně. 
        > -   Neinstalujte na komponentu ATA Gateway Message Analyzer, Wireshark nebo jiný software pro zachycení dat ze sítě. Pokud potřebujete zachycovat síťový provoz, nainstalujte a používejte Microsoft Network Monitor 3.4.

    -   Služba ATA Gateway

    -   Microsoft Visual C++ 2013 Redistributable

    -   Vlastní sada kolekcí dat Sledování výkonu

5.  Po dokončení instalace pro ATA Gateway kliknutím na **Spustit** otevřete prohlížeč a přihlaste se ke konzole ATA. V případě ATA Lightweight Gateway klikněte na **Dokončit**.


>[!div class="step-by-step"]
[« Krok 3](install-ata-step3.md)
[Krok 5 »](install-ata-step5.md)

## Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jun16_HO4-->


