---
title: "Konfigurace předávání událostí systému Windows v Azure Advanced Threat Protection | Microsoft Docs"
description: "Popisuje možnosti konfigurace předávání událostí systému Windows s Azure ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 3547519f-8d9c-40a9-8f0e-c7ba21081203
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: df06235de3a29051f9ffcd889bb95936ed9fc27d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection verze 1.9*



# <a name="configuring-windows-event-forwarding"></a>Konfigurace předávání událostí systému Windows

> [!NOTE]
> Senzor Azure ATP automaticky načte události místně, aniž by bylo nutné konfigurovat předávání událostí.


K vylepšení možností detekce, Azure ATP vyžaduje následující události systému Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 a 7045. Tyto může buď přečíst automaticky senzoru Azure ATP nebo v případě, že Azure ATP senzoru není nasazený, můžete přesměrovávají na samostatné senzoru Azure ATP v jednom ze dvou způsobů, tím nakonfigurujete senzoru samostatné Azure ATP tak, aby naslouchala událostem SIEM nebo configuri NG předávání událostí systému Windows.

> [!NOTE]
> Zkontrolujte, že řadič domény je správně nakonfigurován, aby požadované události.

### <a name="wef-configuration-for-azure-atp-standalone-sensors-with-port-mirroring"></a>Konfigurace WEF pro Azure ATP samostatné senzoru při zrcadlení portů

Po dokončení konfigurace zrcadlení portů z řadičů domény na samostatné senzoru Azure ATP konfigurace předávání událostí systému Windows pomocí iniciované zdroj konfigurace následujících pokynů. Je to jedna z možných konfigurací pro předávání událostí systému Windows. 

**Krok 1: Přidejte účet síťových služeb do skupiny Event Log Readers domény.** 

V tomto scénáři předpokládat, že samostatné senzoru Azure ATP je členem domény.

1.  Otevřete Active Directory Users and Computers, přejděte **BuiltIn** složku a dvojím kliknutím **Event Log Readers**. 
2.  Vyberte možnost **Členové**.
4.  Pokud **Síťová služba** není uvedená, klikněte na **Přidat** a do pole **Zadejte názvy objektů k výběru** zadejte **Síťová služba**. Potom klikněte na **Zkontrolovat jména** a dvakrát klikněte na **OK**. 

Po přidání **síťové služby** k **Event Log Readers** skupině, restartování řadiče domény pro změna se projeví.

**Krok 2: Vytvořte zásadu pro řadiče domény, abyste nastavili možnost Nakonfigurovat cílového správce odběrů.** 
> [!Note] 
> Můžete vytvořit pro tato nastavení zásady skupiny a použití zásad skupiny pro každý řadič domény, který je monitorován pomocí samostatné senzoru Azure ATP. Následující kroky upravit místní zásady řadiče domény.     

1.  Na každém řadiči domény spusťte následující příkaz: *winrm quickconfig*.
2.  Do příkazového řádku zadejte *gpedit.msc*.
3.  Rozbalte položku **Konfigurace počítače > Šablony pro správu > Součásti systému Windows > Předávání událostí**.

 ![Obrázek editoru skupiny místních zásad](media/wef 1 local group policy editor.png)

4.  Klikněte dvakrát na **cíl konfigurovat odběr Manager**.
   
    1.  Vyberte **Povoleno**.
    2.  V části **možnosti**, klikněte na tlačítko **zobrazit**.
    3.  V části **SubscriptionManagers**, zadejte následující hodnotu a klikněte na **OK**: *Server = http: / /<fqdnATPSensor>: 5985 nebo wsman/SubscriptionManager/WEC, aktualizace = 10* () For example: Server = http://atpsensor9.contoso.com:5985 nebo wsman/SubscriptionManager/WEC, aktualizace = 10)
 
   ![Obrázek konfigurace cílového odběru](media/wef 2 config target sub manager.png)
   
    5.  Klikněte na **OK**.
    6.  Do příkazového řádku se zvýšenými oprávněními zadejte *gpupdate /force*. 

**Krok 3: Proveďte následující kroky na samostatné senzoru Azure ATP** 

1.  Otevřete příkazový řádek se zvýšenými oprávněními a zadejte příkaz *wecutil qc*.
2.  Otevřete **Prohlížeč událostí**. 
3.  Klikněte pravým tlačítkem na **odběry** a vyberte **vytvořit odběr**. 

   1.   Zadejte název a popis odběru. 
   2.   Pro **cílové protokolu**, ujistěte se, že **předávaných událostí ty** je vybrána. Pro Azure ATP číst události, musí být v cílovém protokolu **předávaných událostí**. 
   3.   Vyberte **Spuštěno zdrojovým počítačem** a klikněte na **Vybrat skupiny počítačů**.
        1.  Klikněte na **Přidat počítač domény**.
        2.  Do pole **Zadejte název objektu k výběru** zadejte název řadiče domény. Potom klikněte na **Zkontrolovat jména** a nakonec na **OK**. 
       
        ![Obrázek Prohlížeče událostí](media/wef3 event viewer.png)
   
        
        3.  Klikněte na **OK**.
   4.   Klikněte na **Vybrat události**.

        1. Klikněte na **Podle protokolu** a vyberte **Zabezpečení**.
        2. Do pole **Zahrne nebo vyloučí ID události** zadejte číslo události a klikněte na **OK**. Zadejte 4776, jako je například následující ukázka:

 ![Obrázek filtru dotazu](media/wef-4-query-filter.png)

   5.   Klikněte pravým tlačítkem na vytvořený odběr a vyberte **běhový stav** zda jsou všechny problémy se stavem. 
   6.   Po několika minutách zkontrolujte události nastavit na předají se zobrazuje, protože v událostech předávaných na samostatné senzoru Azure ATP.


Další informace najdete v tématu: [konfigurace počítačů pro předání a shromáždění událostí](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Viz také

- [Nainstalovat Azure ATP](install-atp-step1.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)