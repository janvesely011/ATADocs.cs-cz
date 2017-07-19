---
title: "Konfigurace předávání událostí Windows v Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Tento článek popisuje, jaké máte u ATA možnosti pro konfiguraci předávání událostí Windows."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 3f0498f9-061d-40e6-ae07-98b8dcad9b20
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 6469f602d2da833e96bba72003aad3fe2b67eb48
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/03/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="configuring-windows-event-forwarding"></a>Konfigurace předávání událostí systému Windows

Kvůli vylepšení detekčních schopností potřebuje ATA následující události Windows: 4776, 4732, 4733, 4728, 4729, 4756, 4757. Tyto události buď může automaticky číst ATA Lightweight Gateway, nebo mohou být jedním ze dvou způsobů předávány komponentě ATA Gateway (v případě, že komponenta ATA Lightweight Gateway není nasazená), a to konfigurací komponenty ATA Gateway pro naslouchání událostem SIEM, nebo [konfigurací předávání událostí Windows](#configuring-windows-event-forwarding).

> [!NOTE]
> U ATA verze 1.8 a vyšších se u komponent ATA Lightweight Gateway shromažďování událostí už nemusí konfigurovat. ATA Lightweight Gateway teď dokáže číst události místně bez nutnosti konfigurace předávání událostí.

### <a name="wef-configuration-for-ata-gateways-with-port-mirroring"></a>Konfigurace WEF pro ATA Gateway se zrcadlením portů

Po nakonfigurování zrcadlení portů z řadičů domény do ATA Gateway postupujte podle níže uvedených pokynů a nakonfigurujte předávání událostí systému Windows pomocí konfigurace Spuštěno zdrojem. Je to jedna z možných konfigurací pro předávání událostí systému Windows. 

**Krok 1: Přidejte účet síťových služeb do skupiny Event Log Readers domény.** 

V tomto scénáři předpokládáme, že ATA Gateway je členem domény.

1.  Otevřete Uživatelé a počítače služby Active Directory, přejděte do složky **BuiltIn** a poklikejte na skupinu **Event Log Readers**. 
2.  Vyberte možnost **Členové**.
4.  Pokud **Síťová služba** není uvedená, klikněte na **Přidat** a do pole **Zadejte názvy objektů k výběru** zadejte **Síťová služba**. Potom klikněte na **Zkontrolovat jména** a dvakrát klikněte na **OK**. 

Mějte na paměti, že po přidání **Síťové služby** do skupiny **Event Log Readers** musíte restartovat řadiče domény, aby se změna projevila.

**Krok 2: Vytvořte zásadu pro řadiče domény, abyste nastavili možnost Nakonfigurovat cílového správce odběrů.** 
> [!Note] 
> Můžete vytvořit zásady skupiny pro tato nastavení a používat je na každý řadič domény, který je monitorovaný pomocí součásti ATA Gateway. Následující postup upravuje místní zásady řadiče domény.     

1.  Na každém řadiči domény spusťte následující příkaz: *winrm quickconfig*.
2.  Do příkazového řádku zadejte *gpedit.msc*.
3.  Rozbalte položku **Konfigurace počítače > Šablony pro správu > Součásti systému Windows > Předávání událostí**.

 ![Obrázek editoru skupiny místních zásad](media/wef 1 local group policy editor.png)

4.  Dvakrát klikněte na **Nakonfigurovat cílového správce odběrů**.
   
    1.  Vyberte **Povoleno**.
    2.  V části **Možnosti** klikněte na **Zobrazit**.
    3.  V části **SubscriptionManagers** zadejte následující hodnotu a klikněte na tlačítko **OK**:  *Server=http://<fqdnATAGateway>:5985/wsman/SubscriptionManager/WEC,Refresh=10* (například: Server=http://atagateway9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10).
 
   ![Obrázek konfigurace cílového odběru](media/wef 2 config target sub manager.png)
   
    5.  Klikněte na **OK**.
    6.  Do příkazového řádku se zvýšenými oprávněními zadejte *gpupdate /force*. 

**Krok 3: V ATA Gateway proveďte následující postup.** 

1.  Otevřete příkazový řádek se zvýšenými oprávněními a zadejte příkaz *wecutil qc*.
2.  Otevřete **Prohlížeč událostí**. 
3.  Klikněte pravým tlačítkem na **Odběry** a vyberte **Vytvořit odběr**. 

   1.   Zadejte název a popis odběru. 
   2.   V případě možnosti **Cílový protokol** potvrďte výběr možnosti **Předané události**. Aby řešení ATA mohlo události číst, musí být cílovým protokolem **Předané události**. 
   3.   Vyberte **Spuštěno zdrojovým počítačem** a klikněte na **Vybrat skupiny počítačů**.
        1.  Klikněte na **Přidat počítač domény**.
        2.  Do pole **Zadejte název objektu k výběru** zadejte název řadiče domény. Potom klikněte na **Zkontrolovat jména** a nakonec na **OK**. 
       
        ![Obrázek Prohlížeče událostí](media/wef3 event viewer.png)
   
        
        3.  Klikněte na **OK**.
   4.   Klikněte na **Vybrat události**.

        1. Klikněte na **Podle protokolu** a vyberte **Zabezpečení**.
        2. Do pole **Zahrne nebo vyloučí ID události** zadejte číslo události a klikněte na **OK**. 

 ![Obrázek filtru dotazu](media/wef 4 query filter.png)

   5.   Klikněte pravým tlačítkem na vytvořený odběr a vyberte **Stav runtime**, abyste viděli, jestli jsou se stavem nějaké potíže. 
   6.   Po několika minutách ověřte, že se události, jejichž předávání jste nastavili, zobrazují mezi předanými událostmi v komponentě ATA Gateway.


Další informace najdete v tématu [Konfigurace počítačů pro předání a shromáždění událostí](https://technet.microsoft.com/library/cc748890).

## <a name="see-also"></a>Viz také
- [Instalace ATA](install-ata-step1.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
