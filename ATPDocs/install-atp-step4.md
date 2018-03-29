---
title: Instalace Azure Advanced Threat Protection – krok 4 | Microsoft Docs
description: Čtvrtý krok instalace Azure ATP vám pomůže s instalací senzoru samostatné Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 51911e39-76c7-4dcd-bc0b-ec6235d0403f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 56b3cea2089c64e2c78361c44d049d6de67764b6
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-4"></a>Nainstalovat Azure ATP – krok 4

>[!div class="step-by-step"]
[« Krok 3](install-atp-step3.md)
[Krok 5 »](install-atp-step5.md)

## <a name="step-4-install-the-azure-atp-sensor"></a>Krok 4: Nainstalovat Azure ATP senzoru

Před instalací senzoru samostatné Azure ATP na vyhrazený server ověřte, že je zrcadlení portů správně nakonfigurované a že senzoru samostatné Azure ATP vidí provoz do a z řadičů domény. 


> [!IMPORTANT]
>Ujistěte se, že rozhraní .net Framework 4.7 je nainstalován na počítači. Pokud je rozhraní .net Framework 4.7 není nainstalován Azure ATP senzor instalační balíček nainstaluje, který vyžaduje restartování serveru.

Proveďte následující kroky v Azure ATP senzor serveru nebo řadiče domény.

1. Ověřte, zda je počítač připojen k příslušné koncový bod Azure ATP cloudové služby:
  - https://triprd1wceuw1sensorapi.atp.azure.com (pro Evropu)  
  - https://triprd1wcuse1sensorapi.atp.azure.com (pro USA)
  - https://triprd1wcasse1sensorapi.atp.azure.com (pro Asii)

2. Rozbalte instalační soubory ze souboru zip. 
> [!NOTE] 
> Instalace přímo ze souboru zip selže.

2.  Spustit **Azure ATP senzor setup.exe** a postupujte podle pokynů Průvodce instalací.

3.  Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**.

     ![Azure ATP samostatné senzor instalace jazyka](media/sensor-install-language.png)


4.  Průvodce instalací automaticky kontroluje, zda je server řadičem domény nebo vyhrazený server. Pokud je řadič domény, je nainstalovaná senzoru Azure ATP, pokud je vyhrazený server, je nainstalována senzoru samostatné Azure ATP. 
    
    Pro samostatné senzor Azure ATP, například následující obrazovka se zobrazí pokaždé senzor samostatné Azure ATP je nainstalovaný na vyhrazený server:
    
    ![Azure ATP samostatná senzor instalace](media/sensor-install-deployment-type.png)

    Klikněte na **Další**.

    > [!NOTE] 
    > Pokud řadič domény nebo vyhrazený server nesplňuje minimální požadavky na hardware pro instalaci, zobrazí se upozornění. Přesto můžete kliknout na tlačítko **Další** a pokračovat v instalaci. To může být správné volby pro instalaci v testovacím prostředí malé testovacím ve kterém nepotřebujete tolik místo pro uložení dat v Azure ATP. Pro produkční prostředí, důrazně doporučujeme pro práci s Azure ATP [plánování kapacity](atp-capacity-planning.md) průvodce zajistěte, aby řadiče domény nebo vyhrazené servery splňují požadavky.

4.  V části **Konfigurace senzoru**, zadejte cestu instalace a přístupový klíč, který jste zkopírovali v předchozím kroku, podle vašeho prostředí:

    ![Obrázek konfigurace senzor samostatné sady Azure ATP](media/sensor-install-config.png)

      - Instalační cesta: Toto je umístění, kde je nainstalován senzoru samostatné Azure ATP. Ve výchozím nastavení je to senzor %programfiles%\Azure Advanced Threat Protection. Nechte nastavenou výchozí hodnotu.

      - Přístupový klíč: to je načíst z portálu prostoru v předchozím kroku.
    
5. Klikněte na tlačítko **Nainstalovat**. Následující součásti jsou nainstalovaná a nakonfigurovaná v průběhu instalace senzoru Azure ATP:

    -   KB 3047154 (pouze pro Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Neinstalujte KB 3047154 na hostiteli virtualizace (na hostiteli, na kterém je spuštěná virtualizace, spuštění na virtuálním počítači je v pořádku). Může způsobit, že zrcadlení portů přestane fungovat správně. 
        > -   Pokud Wireshark je nainstalovaná na počítači senzor ATP po spuštění Wireshark budete muset restartovat ATP senzoru, protože používá stejné ovladače.

    -   Služba Azure senzor ATP a Azure ATP senzor aktualizační službu
    -   Microsoft Visual C++ 2013 Redistributable

5.  Po dokončení instalace, klikněte na tlačítko **spusťte** otevřete prohlížeč a přihlaste se k portálu Azure ATP pracovního prostoru.


>[!div class="step-by-step"]
[« Krok 3](install-atp-step3.md)
[Krok 5 »](install-atp-step5.md)


## <a name="see-also"></a>Viz také

- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)

- [Konfigurace shromažďování událostí](configure-event-collection.md)

- [Požadavky služby Azure ATP](atp-prerequisites.md)

- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)