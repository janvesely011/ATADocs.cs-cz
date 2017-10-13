---
title: "Instalace Advanced Threat Analytics – krok 4 | Dokumentace Microsoftu"
description: "Čtvrtý krok instalace ATA vám pomůže s instalací ATA Gateway."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/9/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 66e910c1d6d11781fa66f8386b4b3939fd49ebf7
ms.sourcegitcommit: e9f2bfd610b7354ea3fef749275f16819d60c186
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/09/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="install-ata---step-4"></a>Instalace ATA – krok 4

>[!div class="step-by-step"]
[« Krok 3](install-ata-step3.md)
[Krok 5 »](install-ata-step5.md)

## <a name="step-4-install-the-ata-gateway"></a>Krok 4. Instalace ATA Gateway

Před instalací ATA Gateway na vyhrazený server ověřte, že je zrcadlení portů správně nakonfigurované a že ATA Gateway vidí provoz do a z řadičů domény. Další informace najdete v tématu [Ověření zrcadlení portů](validate-port-mirroring.md).


> [!IMPORTANT]
> Ujistěte se, že je nainstalovaná aktualizace [KB2919355](http://support.microsoft.com/kb/2919355/).  Kontrolu instalace opravy hotfix můžete provést spuštěním následující rutiny PowerShellu:
>
> `Get-HotFix -Id kb2919355`

Na serveru ATA Gateway proveďte tento postup.

1.  Extrahujte soubory ze souboru zip. 
> [!NOTE] 
> Instalace přímo ze souboru zip selže.

2.  Spusťte **Microsoft ATA Gateway Setup.exe** a postupujte podle pokynů průvodce instalací.

3.  Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**.

4.  Průvodce instalací automaticky zjistí, jestli je server řadič domény nebo vyhrazený server. Pokud se jedná o řadič domény, nainstaluje se komponenta ATA Lightweight Gateway, pokud se jedná o vyhrazený server, nainstaluje se ATA Gateway. 
    
    V případě komponenty ATA Gateway se například zobrazí následující obrazovka s oznámením, že se na vyhrazeném serveru nainstaluje ATA Gateway:
    
    ![Instalace ATA Gateway](media/ata-gw-install.png) Klikněte na **Další**.

    > [!NOTE] 
    > Pokud řadič domény nebo vyhrazený server nesplňuje minimální hardwarové požadavky na instalaci, zobrazí se upozornění. Přesto můžete kliknout na tlačítko **Další** a pokračovat v instalaci. Může to být správná volba pro instalaci ATA v malém prostředí testovací laboratoře, ve kterém nebudete potřebovat tolik místa pro ukládání dat. V případě provozních prostředí důrazně doporučujeme pracovat s průvodcem pro [plánování kapacity](ata-capacity-planning.md) ATA, ve kterém zjistíte, jestli řadiče domény nebo vyhrazené servery splňují nezbytné požadavky.

4.  V části **Configure the Gateway** (Konfigurace Gateway) zadejte následující informace podle daného prostředí:

    ![Obrázek konfigurace ATA Gateway](media/ata-gw-configure.png)

    > [!NOTE]
    > Při nasazení ATA Gateway nebudete muset zadávat přihlašovací údaje. Pokud se při instalaci ATA Gateway nepovede načíst vaše přihlašovací údaje pomocí jednotného přihlašování (například k tomu může dojít, pokud ATA Center není v doméně, pokud ATA Gateway není v doméně, když nemáte přihlašovací údaje správce ATA), zobrazí se výzva k zadání přihlašovacích údajů, jako na následující obrazovce. 

  ![Zadání přihlašovacích údajů pro ATA Gateway](media/ata-install-credentials.png)

   - Instalační cesta: Jedná se o umístění, kam se nainstaluje ATA Gateway. Ve výchozím nastavení je to %programfiles%\Microsoft Advanced Threat Analytics\Gateway. Nechte nastavenou výchozí hodnotu.
    
5. Klikněte na tlačítko **Nainstalovat**. Během instalace ATA Gateway se instalují a konfigurují následující komponenty:

    -   KB 3047154 (pouze pro Windows Server 2012 R2)

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


## <a name="related-videos"></a>Související videa
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Výběr správné typu ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

