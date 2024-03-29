---
title: Konfigurace předávání událostí Windows ve službě Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Popisuje možnosti pro konfiguraci předávání událostí Windows pomocí služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/29/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 3547519f-8d9c-40a9-8f0e-c7ba21081203
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c5acf930c53e27818d44cde99ad3aace15073090
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65197218"
---
# <a name="configuring-windows-event-forwarding"></a>Konfigurace předávání událostí systému Windows

> [!NOTE]
> Senzoru služby Azure ATP automaticky načte události místně bez nutnosti konfigurace předávání událostí.


Kvůli vylepšení detekčních schopností potřebuje ochrany ATP v programu Azure následující události Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757 a 7045. Ty můžete buď automaticky číst senzoru služby Azure ATP nebo v případě, že není nasazený senzoru služby Azure ATP, může být přeposílán do samostatného senzoru služby Azure ATP v jednom ze dvou způsobů, tím nakonfigurujete samostatný senzor ochrany ATP v programu Azure tak, aby naslouchala událostem SIEM nebo configuri NG předávání událostí Windows.

> [!NOTE]
> Zkontrolujte, že je řadič domény správně nakonfigurovaný na zachycování požadované události.

### <a name="wef-configuration-for-azure-atp-standalone-sensors-with-port-mirroring"></a>Konfigurace WEF pro služby Azure ATP samostatného senzoru se zrcadlením portů

Po dokončení konfigurace zrcadlení portů z řadičů domény do samostatného senzoru služby Azure ATP postupujte podle následujících pokynů a nakonfigurujte předávání událostí Windows pomocí konfigurace spuštěno zdrojem. Je to jedna z možných konfigurací pro předávání událostí systému Windows. 

**Krok 1: Přidejte účet síťových služeb do skupiny Event Log Readers domény.** 

V tomto scénáři předpokládá, že služby Azure ATP samostatný senzor je členem domény.

1.  Otevření Active Directory Users and Computers, přejděte **BuiltIn** složky a dvojím kliknutím **Event Log Readers**. 
2.  Vyberte možnost **Členové**.
3.  Pokud **Síťová služba** není uvedená, klikněte na **Přidat** a do pole **Zadejte názvy objektů k výběru** zadejte **Síťová služba**. Potom klikněte na **Zkontrolovat jména** a dvakrát klikněte na **OK**. 

Po přidání **síťová služba** k **Event Log Readers** skupině, restartování řadiče domény se změna projevila.

**Krok 2: Vytvořte zásadu pro řadiče domény, abyste nastavili možnost nakonfigurovat cílového správce odběrů.** 
> [!Note] 
> Můžete vytvořit zásady skupiny pro tato nastavení a použití zásad skupiny na každý řadič domény služby Azure ATP samostatný senzor monitoruje. Následující postup upravuje místní zásady řadiče domény.     

1. Na každém řadiči domény spusťte následující příkaz: *winrm quickconfig*.
2. Do příkazového řádku zadejte *gpedit.msc*.
3. Rozbalte položku **Konfigurace počítače > Šablony pro správu > Součásti systému Windows > Předávání událostí**.

   ![Obrázek editoru skupiny místních zásad](media/wef%201%20local%20group%20policy%20editor.png)

4. Dvakrát klikněte na panel **nakonfigurovat cílového správce odběrů**.
   
   1.  Vyberte **Povoleno**.
   2.  V části **možnosti**, klikněte na tlačítko **zobrazit**.
   3.  V části **SubscriptionManagers**, zadejte následující hodnoty a klikněte na tlačítko **OK**: Server = http\://\<fqdnATPSensor >: 5985 nebo wsman/SubscriptionManager/WEC, obnovení = 10 (například: Server=http\://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10)
    
   ![Obrázek konfigurace cílového odběru](media/wef%202%20config%20target%20sub%20manager.png)
    
5. Klikněte na **OK**.
6. Do příkazového řádku se zvýšenými oprávněními zadejte *gpupdate /force*. 

**Krok 3: Následující postup proveďte samostatného senzoru služby Azure ATP** 

1. Otevřete příkazový řádek se zvýšenými oprávněními a zadejte příkaz *wecutil qc*.
2. Otevřete **Prohlížeč událostí**. 
3. Klikněte pravým tlačítkem na **předplatná** a vyberte **vytvořit odběr**. 
    
    1. Zadejte název a popis odběru. 
    2. Pro **cílový protokol**, ujistěte se, že **předané události** zaškrtnuto. Pro služby Azure ATP mohlo události číst, musí být cílovým protokolem **předané události**. 
    3. Vyberte **Spuštěno zdrojovým počítačem** a klikněte na **Vybrat skupiny počítačů**.
        1. Klikněte na **Přidat počítač domény**.
        2. Do pole **Zadejte název objektu k výběru** zadejte název řadiče domény. Potom klikněte na **Zkontrolovat jména** a nakonec na **OK**. 
        3. Klikněte na **OK**.
        ![Obrázek prohlížeče událostí](media/wef3%20event%20viewer.png)     
    4. Klikněte na **Vybrat události**.
        1. Klikněte na **Podle protokolu** a vyberte **Zabezpečení**.
        2. Do pole **Zahrne nebo vyloučí ID události** zadejte číslo události a klikněte na **OK**. Zadejte 4776, jako je například v následujícím příkladu:<br/>
        ![Obrázek filtru dotazu](media/wef-4-query-filter.png)
    5. Klikněte pravým tlačítkem na vytvořený odběr a vyberte **stav Runtime** jestli jsou všechny problémy se stavem. 
    6. Po několika minutách zkontrolujte události nastavit na předat dál, zobrazují mezi předanými událostmi v samostatného senzoru služby Azure ATP.


Další informace naleznete v tématu: [Konfigurace počítačů pro předání a shromáždění událostí](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Viz také

- [Instalace služby Azure ATP](install-atp-step1.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
