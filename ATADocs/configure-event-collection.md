---
title: Konfigurace předávání událostí Windows v Advanced Threat Analytics | Dokumentace Microsoftu
description: Tento článek popisuje, jaké máte u ATA možnosti pro konfiguraci předávání událostí Windows.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7f96971f3d7d11f49c025ddf88c1ced5e4fc8cb6
ms.sourcegitcommit: f86dc8ad3d1e75ba64b372d4d0ab5386e28f2e29
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/13/2018
ms.locfileid: "51609669"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="configuring-windows-event-forwarding"></a>Konfigurace předávání událostí systému Windows

> [!NOTE]
> U ATA verze 1.8 a vyšších se u komponent ATA Lightweight Gateway shromažďování událostí už nemusí konfigurovat. ATA Lightweight Gateway teď číst události místně bez nutnosti konfigurace předávání událostí.

Kvůli vylepšení detekčních schopností potřebuje ATA následující události Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757, 7045. Ty můžete buď automaticky číst ATA Lightweight Gateway nebo v případě ATA Lightweight Gateway není nasazená, může být přeposílán komponentě ATA Gateway jedním ze dvou způsobů, konfigurací komponenty ATA Gateway tak, aby naslouchala událostem SIEM, nebo tím, že nakonfigurujete události Windows Předávání.

> [!NOTE]
> Pokud používáte Server Core [wecutil](https://docs.microsoft.com/windows-server/administration/windows-commands/wecutil) umožňuje vytvářet a spravovat odběry událostí, které jsou předávané ze vzdálených počítačů.

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>Konfigurace WEF pro ATA Gateway se zrcadlením portů

Po dokončení konfigurace zrcadlení portů z řadičů domény do komponenty ATA Gateway, použijte následující pokyny ke konfiguraci předávání událostí Windows pomocí konfigurace spuštěno zdrojem. Je to jedna z možných konfigurací pro předávání událostí systému Windows. 

**Krok 1: Přidejte účet síťových služeb do skupiny Event Log Readers domény.** 

V tomto scénáři se předpokládá, že ATA Gateway členem domény.

1.  Otevření Active Directory Users and Computers, přejděte **BuiltIn** složky a dvojím kliknutím **Event Log Readers**. 
2.  Vyberte možnost **Členové**.
3.  Pokud **Síťová služba** není uvedená, klikněte na **Přidat** a do pole **Zadejte názvy objektů k výběru** zadejte **Síťová služba**. Potom klikněte na **Zkontrolovat jména** a dvakrát klikněte na **OK**. 

Po přidání **síťová služba** k **Event Log Readers** skupině, restartování řadiče domény se změna projevila.

**Krok 2: Vytvořte zásadu pro řadiče domény, abyste nastavili možnost Nakonfigurovat cílového správce odběrů.** 
> [!Note] 
> Můžete vytvořit zásady skupiny pro tato nastavení a používat je na každý řadič domény, který je monitorovaný pomocí součásti ATA Gateway. Následující postup upravuje místní zásady řadiče domény.     

1.  Na každém řadiči domény spusťte následující příkaz: *winrm quickconfig*.
2.  Do příkazového řádku zadejte *gpedit.msc*.
3.  Rozbalte položku **Konfigurace počítače > Šablony pro správu > Součásti systému Windows > Předávání událostí**.

![Obrázek editoru skupiny místních zásad](media/wef%201%20local%20group%20policy%20editor.png)

4.  Dvakrát klikněte na panel **nakonfigurovat cílového správce odběrů**.
   
    1.  Vyberte **Povoleno**.
    2.  V části **možnosti**, klikněte na tlačítko **zobrazit**.
    3.  V části **SubscriptionManagers**, zadejte následující hodnoty a klikněte na tlačítko **OK**: *Server = http: / /<fqdnATAGateway>: 5985 nebo wsman/SubscriptionManager/WEC, obnovení = 10* 
      
         *(Příklad: Server = http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC, aktualizujte = 10)*
      
         ![Obrázek konfigurace cílového odběru](media/wef%202%20config%20target%20sub%20manager.png)
      
    4.  Klikněte na **OK**.
    5.  Do příkazového řádku se zvýšenými oprávněními zadejte *gpupdate /force*. 

**Krok 3: V ATA Gateway proveďte následující postup.** 

1.  Otevřete příkazový řádek se zvýšenými oprávněními a zadejte příkaz *wecutil qc*.
2.  Otevřete **Prohlížeč událostí**. 
3.  Klikněte pravým tlačítkem na **předplatná** a vyberte **vytvořit odběr**. 

    1.  Zadejte název a popis odběru. 
    2.  Pro **cílový protokol**, ujistěte se, že **předané události** zaškrtnuto. Aby řešení ATA mohlo události číst, musí být cílovým protokolem **Předané události**. 
    3.  Vyberte **Spuštěno zdrojovým počítačem** a klikněte na **Vybrat skupiny počítačů**.
        1.  Klikněte na **Přidat počítač domény**.
        2.  Do pole **Zadejte název objektu k výběru** zadejte název řadiče domény. Potom klikněte na **Zkontrolovat jména** a nakonec na **OK**.  
          ![Obrázek prohlížeče událostí](media/wef3%20event%20viewer.png)  
        3.  Klikněte na **OK**.
    4.  Klikněte na **Vybrat události**.
        1. Klikněte na **Podle protokolu** a vyberte **Zabezpečení**.
        2. Do pole **Zahrne nebo vyloučí ID události** zadejte číslo události a klikněte na **OK**. Zadejte 4776, jako je například v následujícím příkladu.

        ![Obrázek filtru dotazu](media/wef%204%20query%20filter.png)

    5.  Klikněte pravým tlačítkem na vytvořený odběr a vyberte **stav Runtime** jestli jsou všechny problémy se stavem. 
    6.  Po několika minutách ověřte, že se události, jejichž předávání jste nastavili, zobrazují mezi předanými událostmi v komponentě ATA Gateway.


Další informace najdete v tématu: [konfigurace počítačů pro předání a shromáždění událostí](https://technet.microsoft.com/library/cc748890)

## <a name="see-also"></a>Viz také
- [Instalace ATA](install-ata-step1.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
