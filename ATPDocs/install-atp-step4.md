---
title: Nainstalovat Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Čtvrtý krok instalace ochrany ATP v programu Azure vám pomůže s instalací senzoru služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/28/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 51911e39-76c7-4dcd-bc0b-ec6235d0403f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fd2a2316f63b5324e7869878104bd663e48b2771
ms.sourcegitcommit: e2a89030c31376c6798697a62b484f45ed54e679
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2018
ms.locfileid: "52501095"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="install-azure-atp---step-4"></a>Instalace služby Azure ATP – krok 4

> [!div class="step-by-step"]
> [« Krok 3](install-atp-step3.md)
> [Krok 5 »](install-atp-step5.md)

## <a name="step-4-install-the-azure-atp-sensor"></a>Krok 4: Instalace senzoru služby Azure ATP

> [!IMPORTANT]
>Ujistěte se, že rozhraní .net Framework 4.7 je nainstalovaná na počítači. Pokud je rozhraní .net Framework 4.7 není nainstalovaná instalačního balíčku senzoru služby Azure ATP ho nainstaluje, která může vyžadovat restartování serveru.

Proveďte následující kroky na řadiči domény.

1. Ověřte, zda je počítač připojen k relevantní koncový bod cloudu služby ochrany ATP v programu Azure:
  - https://triprd1wceuw1sensorapi.atp.azure.com (pro Evropa)  
  - https://triprd1wcuse1sensorapi.atp.azure.com (pro USA)
  - https://triprd1wcasse1sensorapi.atp.azure.com (pro Asie)

2. Rozbalte instalační soubory ze souboru zip. 
> [!NOTE] 
> Instalace přímo ze souboru zip selže.

3.  Spustit **setup.exe senzoru služby Azure ATP** a postupujte podle pokynů Průvodce instalací.

4.  Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**.

     ![Azure jazyk instalace samostatného senzoru ochrany ATP v programu](media/sensor-install-language.png)


5.  Průvodce instalací automaticky kontroluje, zda je server řadičem domény nebo vyhrazený server. Pokud je řadič domény, nainstaluje se senzoru služby Azure ATP, pokud se jedná o vyhrazený server, Azure ATP samostatný senzor je nainstalovaný. 
    
    Například pro Azure ATP samostatný senzor, se zobrazí následující obrazovka s oznámením, že Azure ATP samostatný senzor je nainstalovaný na vyhrazeném serveru:
    
    ![Instalace samostatné senzoru služby Azure ochrany ATP v programu](media/sensor-install-deployment-type.png)

    Klikněte na **Další**.

    > [!NOTE] 
    > Pokud řadič domény nebo vyhrazený server nesplňuje minimální požadavky na hardware pro instalaci, zobrazí se upozornění. Přesto můžete kliknout na tlačítko **Další** a pokračovat v instalaci. To může být správná volba pro instalaci služby Azure ATP v testovacím prostředí malé lab, ve kterém není třeba tolik místa pro ukládání dat. Pro produkční prostředí, důrazně doporučujeme pro práci s Azure ATP [plánování kapacity](atp-capacity-planning.md) Průvodce Ujistěte se, že řadiče domény nebo vyhrazené servery splňují nezbytné požadavky.

6.  V části **Konfigurace senzoru**, zadejte instalační cestu a přístupový klíč, který jste zkopírovali v předchozím kroku, podle vašeho prostředí:

    ![Azure ochrany ATP v programu samostatný senzor konfigurace image](media/sensor-install-config.png)

      - Instalační cesta: Toto je umístění, kde je nainstalován samostatného senzoru služby Azure ATP. Ve výchozím nastavení to je %programfiles%\Azure Advanced Threat Protection senzoru. Nechte nastavenou výchozí hodnotu.

      - Přístupový klíč: to je načten z ochrany ATP v programu Azure portal v předchozím kroku.
    
7. Klikněte na tlačítko **Nainstalovat**. Následující komponenty jsou nainstalovaná a nakonfigurovaná v průběhu instalace senzoru služby Azure ATP:

    -   KB 3047154 (pouze pro Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   Neinstalujte KB 3047154 na hostiteli virtualizace (na hostiteli, na kterém je spuštěná virtualizace, spuštění na virtuálním počítači je v pořádku). Může způsobit, že zrcadlení portů přestane fungovat správně. 
        > -   Pokud Wireshark je nainstalovaná na počítači senzor ochrany ATP v programu, až spustíte Wireshark budete muset restartovat senzor ochrany ATP v programu, protože používá stejné ovladače.

    -   Azure službu sensor ochrany ATP v programu a službu updater senzoru služby Azure ATP
    -   Microsoft Visual C++ 2013 Redistributable

8.  Po dokončení instalace klikněte na tlačítko **spuštění** otevřete prohlížeč a přihlaste se k portálu ochrany ATP v programu Azure.


> [!div class="step-by-step"]
> [« Krok 3](install-atp-step3.md)
> [Krok 5 »](install-atp-step5.md)


## <a name="see-also"></a>Viz také

- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)

- [Konfigurace shromažďování událostí](configure-event-collection.md)

- [Požadavky služby Azure ATP](atp-prerequisites.md)

- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
