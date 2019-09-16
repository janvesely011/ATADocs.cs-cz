---
title: Nainstalovat rychlý Start snímačů pro Azure ATP | Microsoft Docs
description: Krok 4 pro instalaci Azure ATP vám pomůže nainstalovat senzor Azure ATP.
author: mlottner
ms.author: mlottner
ms.date: 03/03/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f3af1034b73d1fc058a966c5d90eaf24dd282140
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71004877"
---
# <a name="quickstart-install-the-azure-atp-sensor"></a>Rychlý Start Instalace senzoru služby Azure ATP

V tomto rychlém startu nainstalujete senzor Azure ATP na řadič domény. Pokud dáváte přednost tiché instalaci, přečtěte si článek o [tiché instalaci](atp-silent-installation.md) .

## <a name="prerequisites"></a>Požadavky

- [Instance ATP Azure](install-atp-step1.md) , která je [připojená ke službě Active Directory](install-atp-step2.md).
- Stažená kopie balíčku pro [instalaci senzoru ATP](install-atp-step3.md) a přístupový klíč.
- Ujistěte se, že je v počítači nainstalováno rozhraní Microsoft .NET Framework 4,7. Pokud není nainstalované rozhraní .NET Framework 4,7, instalační balíček senzoru ATP Azure ho nainstaluje, což může vyžadovat restartování serveru.

## <a name="install-the-sensor"></a>Nainstalovat senzor

Na řadiči domény proveďte následující kroky.

1. Ověřte, že počítač má připojení ke relevantním koncovým službám cloudových služeb Azure ATP:
   - Evropa
      - [https://triprd1wceuw1sensorapi.atp.azure.com](https://triprd1wceuw1sensorapi.atp.azure.com) 
      - [https://triprd1wceun1sensorapi.atp.azure.com](https://triprd1wceun1sensorapi.atp.azure.com)
   - USA 
      - [https://triprd1wcuse1sensorapi.atp.azure.com](https://triprd1wcuse1sensorapi.atp.azure.com)
      - [https://triprd1wcusw1sensorapi.atp.azure.com](https://triprd1wcusw1sensorapi.atp.azure.com)
      - [https://triprd1wcuswb1sensorapi.atp.azure.com](https://triprd1wcuswb1sensorapi.atp.azure.com)
   - Asie
      - [https://triprd1wcasse1sensorapi.atp.azure.com](https://triprd1wcasse1sensorapi.atp.azure.com)

2. Extrahujte instalační soubory ze souboru ZIP. Instalace přímo ze souboru zip selže.

3. Spusťte soubor **Setup. exe pro senzory Azure ATP** a postupujte podle pokynů Průvodce instalací.

4. Na stránce **Vítejte** vyberte svůj jazyk a klikněte na **Další**.

    ![Jazyk instalace samostatného senzoru Azure ATP](media/sensor-install-language.png)


5. Průvodce instalací automaticky zkontroluje, jestli je server řadič domény nebo vyhrazený server. Pokud se jedná o řadič domény, je nainstalovaný senzor Azure ATP. Pokud se jedná o vyhrazený server, nainstaluje se samostatný senzor Azure ATP.
    
    Například pro senzor ATP Azure se zobrazí následující obrazovka, která vás upozorní na to, že je na vyhrazeném serveru nainstalovaný senzor Azure ATP:
    
    ![Instalace senzoru ATP Azure](media/sensor-install-deployment-type.png)

   Klikněte na **Další**.

    > [!NOTE] 
    > Vydá se upozornění, pokud řadič domény nebo vyhrazený server nesplňuje minimální požadavky na hardware pro instalaci. Upozornění nebrání kliknutí na tlačítko **Další**a pokračování v instalaci. Může se jednat o správnou možnost pro instalaci Azure ATP v testovacím prostředí malého testovacího prostředí, kde je potřeba méně místa pro úložiště dat. V produkčních prostředích se důrazně doporučuje pracovat s průvodcem [plánováním kapacity](atp-capacity-planning.md) ve službě Azure ATP a ujistit se, že řadiče domény nebo vyhrazené servery splňují nezbytné požadavky.

6. V části **Konfigurovat senzor**zadejte instalační cestu a přístupový klíč, který jste zkopírovali z předchozího kroku, a to na základě vašeho prostředí:

    ![Obrázek konfigurace senzoru ATP Azure](media/sensor-install-config.png)

      - Instalační cesta: Místo, kde je nainstalovaný senzor Azure ATP. Ve výchozím nastavení je cesta%programfiles%\Azure Advanced Threat Protection snímač. Nechte nastavenou výchozí hodnotu.

     - Přístupový klíč: Načtená z portálu Azure ATP v předchozím kroku.
    
7. Klikněte na tlačítko **nainstalovat**. Při instalaci senzoru ATP Azure jsou nainstalované a nakonfigurované následující komponenty:

    - KB 3047154 (pouze pro Windows Server 2012 R2)

        > [!IMPORTANT]
        > - Neinstalujte KB 3047154 na hostiteli virtualizace (na hostiteli, na kterém je spuštěná virtualizace, spuštění na virtuálním počítači je v pořádku). Může způsobit, že zrcadlení portů přestane fungovat správně. 
        > - Pokud je na počítači snímače ATP nainstalovaný Nástroj Wireshark, musíte po spuštění nástroje Wireshark restartovat senzor ATP, protože používá stejné ovladače.

    - Služba pro senzory Azure ATP a služba aktualizace pro senzory Azure ATP
    - Microsoft Visual C++ 2013 Redistributable


## <a name="next-steps"></a>Další kroky

Senzor ATP Azure je navržený tak, aby měl minimální dopad na prostředky vašeho řadiče domény a síťové aktivity. Informace o tom, jak vytvořit vyhodnocení výkonu, najdete v tématu [plánování kapacity řešení Azure ATP](install-atp-step5.md).


## <a name="join-the-community"></a>Připojte se ke komunitě

Máte k dispozici další otázky nebo zájem o projednávání Azure ATP a souvisejícího zabezpečení s ostatními? Připojte se ke [komunitě ATP Azure](https://aka.ms/azureatpcommunity) ještě dnes!
