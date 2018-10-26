---
title: Instalace Advanced Threat Analytics – krok 5 | Dokumentace Microsoftu
description: Krok 5 instalace ATA vám pomůže nakonfigurovat nastavení pro komponentu ATA Gateway.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0fbd15aa61983a62313f0f1ef89f688046474b9d
ms.sourcegitcommit: 2916d6f8d6e6f754d7fb8a5d31b255a46aa35ecd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/26/2018
ms.locfileid: "50132652"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="install-ata---step-5"></a>Instalace ATA – krok 5

> [!div class="step-by-step"]
> [« Krok 4](install-ata-step4.md)
> [Krok 6 »](install-ata-step6.md)


## <a name="step-5-configure-the-ata-gateway-settings"></a>Krok 5. Konfigurace nastavení ATA Gateway
Po instalaci komponenty ATA Gateway proveďte následující kroky a nakonfigurujte nastavení ATA Gateway.

1.  V konzole ATA přejděte do sekce **Konfigurace** a v části **Systém** vyberte možnost **Gateway**.
   
     ![Obrázek konfigurace nastavení brány](media/ata-gw-config-1.png)


2.  Klikněte na bránu, kterou chcete nakonfigurovat, a zadejte následující informace:

    ![Obrázek konfigurace nastavení brány](media/ATA-Gateways-config-2.png)

  - **Popis**: Zadejte popis pro ATA Gateway (volitelné).
  - **Řadiče domény zrcadlené portem (FQDN)** (požadováno pro ATA Gateway, nastavení nelze změnit pro ATA Lightweight Gateway): Zadejte úplný název FQDN řadiče domény a kliknutím na symbol plus ho přidejte do seznamu. Například **dc01.contoso.com**.

Následující informace platí pro servery, které zadáte do seznamu **Řadiče domény**:
    - Všechny řadiče domény, jejichž provoz ATA Gateway monitoruje přes zrcadlení portů, musí být uvedené v seznamu **Řadiče domény**. Pokud řadič domény není uvedený v seznamu **Řadiče domény**, detekce podezřelých aktivit nemusí fungovat podle očekávání.
    - Nejméně jeden řadič domény v seznamu by měl být globální katalog. To umožňuje ATA překládat objekty počítačů a uživatelů v jiných doménách v doménové struktuře.

  - **Síťové adaptéry pro zachytávání** (povinné):
  - Pro ATA Gateway na vyhrazeném serveru vyberte síťové adaptéry, které jsou nakonfigurované jako cílový port zrcadlení. Tyto příjem provozu řadiče domény zrcadlené.
  - V případě ATA Lightweight Gateway by to měly být všechny síťové adaptéry, které se používají ke komunikaci s ostatními počítači ve vaší organizaci.
  
  - **Kandidát na synchronizátora domény**: Za synchronizaci mezi ATA a doménou Active Directory může být zodpovědná libovolná ATA Gateway, která je nastavená jako kandidát na synchronizátora domény. Počáteční synchronizace v závislosti na velikosti domény může nějakou dobu trvat a je náročná. Ve výchozím nastavení jsou jako kandidáti na synchronizátora domény nastavené jenom ATA Gateway.
   Doporučuje se, že zakážete všechny vzdálené lokality komponenty ATA Gateway nebudou kandidáti na synchronizátora domény.
   Pokud je řadič domény jen pro čtení, nenastavujte ho jako kandidáta na synchronizátora domény. Další informace najdete v části [Architektura ATA](ata-architecture.md#ata-lightweight-gateway-features).

  > [!NOTE] 
  > První spuštění služby ATA Gateway po instalaci bude trvat několik minut, protože sestavuje mezipaměť analyzátorů zachytávání dat ze sítě.
  > Změny konfigurace jsou použity v ATA Gateway při příští plánované synchronizaci mezi ATA Gateway a ATA Center.

3. Volitelně můžete nastavit [Syslog listener and Windows Event Forwarding Collection](configure-event-collection.md) (Naslouchací proces syslog a kolekce předávání událostí systému Windows). 
4. Povolit **aktualizaci ATA Gateway automaticky** tak, že ve vydání příštích verzí při aktualizaci komponenty ATA Center, tato komponenta ATA Gateway se automaticky aktualizuje.

5. Klikněte na **Uložit**.


## <a name="validate-installations"></a>Ověření instalací
Chcete-li ověřit, že ATA Gateway byla úspěšně nasazena, zkontrolujte následující kroky:

1.  Zkontrolujte, že je služba **Microsoft Advanced Threat Analytics Gateway** spuštěná. Po uložení nastavení ATA Gateway může trvat několik minut, než se služba spustí.

2.  Pokud se služba nespustí, zkontrolujte soubor Microsoft.Tri.Gateway-Errors.log umístěný v následující výchozí složce, %programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs, a pomoc najdete v tématu [Řešení potíží s ATA](troubleshooting-ata-known-errors.md).

3.  Pokud se jedná o první nainstalovanou komponentu ATA Gateway, přihlaste se ke konzole ATA za několik minut a otevřete podokno oznámení potáhnutím pravé strany obrazovky. Měli byste vidět seznam **Entities Recently Learned** (Nedávno zjištěné entity) na panelu oznámení na pravé straně konzoly.

4.  Na ploše klikněte na zástupce **Microsoft Advanced Threat Analytics** a připojte se ke konzole ATA. Přihlaste se pomocí stejných přihlašovacích údajů, které jste použili k instalaci ATA Center.
5.  V konzole něco vyhledejte v panelu vyhledávání, například uživatele nebo skupinu ve vaší doméně.
6.  Otevřete nástroj Sledování výkonu. Ve stromovém zobrazení Výkon klikněte na **Sledování výkonu** a potom klikněte na ikonu se znaménkem plus **Přidat čítač**. Rozbalte položku **Microsoft ATA Gateway** a přejděte dolů k položce **Network Listener PEF Captured Messages/Sec** (Zprávy zachycené komponentou PEF NetworkListener/s) a přidejte ji. Zkontrolujte, že v grafu vidíte aktivitu.

    ![Obrázek přidání čítačů výkonu](media/ATA-performance-monitoring-add-counters.png)


> [!div class="step-by-step"]
> [« Krok 4](install-ata-step4.md)
> [Krok 6 »](install-ata-step6.md)



## <a name="related-videos"></a>Související videa
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Volba správného typu komponenty ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

