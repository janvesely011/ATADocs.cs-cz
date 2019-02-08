---
title: Instalace senzoru služby Azure ATP rychlý start | Dokumentace Microsoftu
description: Čtvrtý krok instalace ochrany ATP v programu Azure vám pomůže s instalací senzoru služby Azure ATP.
author: mlottner
ms.author: mlottner
ms.date: 02/06/2019
ms.topic: quickstart
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3a166a1bd820437d92510e3274e4591f41d80edf
ms.sourcegitcommit: 96752da28f43896e7b8e5945947b32c4810bdff6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/07/2019
ms.locfileid: "55831459"
---
# <a name="quickstart-install-the-azure-atp-sensor"></a>Rychlý start: Instalace senzoru služby Azure ATP

V tomto rychlém startu budete instalace senzoru služby Azure ATP na řadiči domény. Pokud dáváte přednost tichou instalaci, najdete v článku [tichou instalaci](atp-silent-installation.md) článku.

## <a name="prerequisites"></a>Požadavky

- [Instance služby Azure ATP](install-atp-step1.md) to [připojeným ke službě Active Directory](install-atp-step2.md).
- Stažený kopie vašeho [ochrany ATP v programu senzor instalační balíček](install-atp-step3.md) a přístupový klíč.
- Ujistěte se, že na počítači je nainstalované rozhraní Microsoft .net Framework 4.7. Pokud rozhraní .net Framework 4.7 není nainstalovaná, instalačního balíčku senzoru služby Azure ATP ho nainstaluje, která může vyžadovat restartování serveru.

## <a name="install-the-sensor"></a>Instalace senzoru

Proveďte následující kroky na řadiči domény.

1. Ověřte, zda že je počítač připojen k příslušné koncových bodů služby Azure ATP cloudové služby:
   - Evropa
      - [https://triprd1wceuw1sensorapi.atp.azure.com](https://triprd1wceuw1sensorapi.atp.azure.com) 
      - [https://triprd1wceun1sensorapi.atp.azure.com](https://triprd1wceun1sensorapi.atp.azure.com)
   - USA 
      - [https://triprd1wcuse1sensorapi.atp.azure.com](https://triprd1wcuse1sensorapi.atp.azure.com)
      - [https://triprd1wcusw1sensorapi.atp.azure.com](https://triprd1wcusw1sensorapi.atp.azure.com)
      - [https://triprd1wcuswb1sensorapi.atp.azure.com](https://triprd1wcuswb1sensorapi.atp.azure.com)
   - Asie
      - [https://triprd1wcasse1sensorapi.atp.azure.com](https://triprd1wcasse1sensorapi.atp.azure.com)

2. Rozbalte instalační soubory ze souboru zip. Instalace přímo ze souboru zip selže.

3. Spustit **setup.exe senzoru služby Azure ATP** a postupujte podle pokynů Průvodce instalací.

4. Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**.

    ![Azure jazyk instalace samostatného senzoru ochrany ATP v programu](media/sensor-install-language.png)


5. Průvodce instalací automaticky kontroluje, zda je server řadičem domény nebo vyhrazený server. Pokud je řadič domény, nainstaluje se senzoru služby Azure ATP. Pokud se jedná o vyhrazený server, Azure ATP samostatný senzor je nainstalovaný.
    
    Například senzoru Azure ATP se zobrazí následující obrazovka s oznámením, že Azure ATP senzor je nainstalovaný na vyhrazeném serveru:
    
    ![Instalace senzoru služby Azure ochrany ATP v programu](media/sensor-install-deployment-type.png)

   Klikněte na **Další**.

    > [!NOTE] 
    > Pokud řadič domény nebo vyhrazený server nesplňuje minimální požadavky na hardware pro instalaci, objeví se upozornění. Upozornění nezabrání kliknutím **Další**a pokračovat v instalaci. Správná volba pro instalaci služby Azure ATP v testovacím prostředí malé lab, ve kterém jsou vyžadována méně místa pro ukládání dat může být stále. Pro produkční prostředí, důrazně doporučujeme pro práci s Azure ATP [plánování kapacity](atp-capacity-planning.md) Průvodce Ujistěte se, že řadiče domény nebo vyhrazené servery splňují nezbytné požadavky.

6. V části **Konfigurace senzoru**, zadejte instalační cestu a přístupový klíč, který jste zkopírovali v předchozím kroku, podle vašeho prostředí:

    ![Obrázek Konfigurace senzoru Azure ochrany ATP v programu](media/sensor-install-config.png)

      - Instalační cesta: Umístění, kde je nainstalován senzoru služby Azure ATP. Ve výchozím nastavení je cesta %programfiles%\Azure Advanced Threat Protection senzoru. Nechte nastavenou výchozí hodnotu.

     - Přístupový klíč: Získané z portálu služby Azure ATP v předchozím kroku.
    
7. Klikněte na tlačítko **nainstalovat**. Následující komponenty jsou nainstalovaná a nakonfigurovaná v průběhu instalace senzoru služby Azure ATP:

    - KB 3047154 (pouze pro Windows Server 2012 R2)

        > [!IMPORTANT]
        > - Neinstalujte KB 3047154 na hostiteli virtualizace (na hostiteli, na kterém je spuštěná virtualizace, spuštění na virtuálním počítači je v pořádku). Může způsobit, že zrcadlení portů přestane fungovat správně. 
        > - Pokud Wireshark je nainstalovaná na počítači senzor ochrany ATP v programu, až spustíte Wireshark budete muset restartovat senzor ochrany ATP v programu, protože používá stejné ovladače.

    - Azure službu sensor ochrany ATP v programu a službu updater senzoru služby Azure ATP
    - Microsoft Visual C++ 2013 Redistributable

8. Po dokončení instalace klikněte na tlačítko **spuštění** otevřete prohlížeč a přihlaste se k portálu ochrany ATP v programu Azure.

## <a name="next-steps"></a>Další postup

> [!div class="step-by-step"]
> [«Krok 3: stáhnout instalaci senzoru](install-atp-step3.md)
> [krok 5 – Konfigurace nastavení senzor»](install-atp-step5.md)

## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://aka.ms/azureatpcommunity) ještě dnes!