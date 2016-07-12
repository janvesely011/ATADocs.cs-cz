---
title: "Instalace ATA – Krok 5 | Microsoft Advanced Threat Analytics"
description: "Krok 5 instalace ATA vám pomůže nakonfigurovat nastavení pro komponentu ATA Gateway."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: d6e7d7bef97bfc4ffde07959dd9256f0319d685f
ms.openlocfilehash: 6400a0eabefac91b418e00eb670b1329fa1b5fb5


---

# Instalace ATA – Krok 5

>[!div class="step-by-step"]
[« Krok 4](install-ata-step4.md)
[Krok 6 »](install-ata-step6.md)


## Krok 5. Konfigurace nastavení ATA Gateway
Po instalaci komponenty ATA Gateway proveďte následující kroky a nakonfigurujte nastavení ATA Gateway.

1.  V konzole ATA klikněte na **Konfigurace** a vyberte stránku **ATA Gateway**.

2.  Zadejte následující informace.

  - **Popis**: <br>Zadejte popis ATA Gateway (nepovinné).
  - **Řadiče domény se zrcadlením portů (FQDN)** (povinné pro ATA Gateway, pro ATA Lightweight Gateway nejde nastavit): <br>Zadejte úplný plně kvalifikovaný název domény řadiči domény a kliknutím na symbol plus ho přidejte do seznamu. Například **dc01.contoso.com**.<br /><br />![Obrázek příkladu plně kvalifikovaného názvu domény](media/ATAGWDomainController.png)

Následující informace platí pro servery, které zadáte do seznamu **Řadiče domény**: – Všechny řadiče domény, jejichž provoz ATA Gateway monitoruje přes zrcadlení portů, musí být uvedené v seznamu **Řadiče domény**. Pokud řadič domény není uvedený v seznamu **Řadiče domény**, detekce podezřelých aktivit nemusí fungovat podle očekávání.
– Nejméně jeden řadič domény v seznamu musí být server globálního katalogu. Tak může ATA překládat objekty počítačů a uživatelů v jiných doménách v doménové struktuře.

 - **Síťové adaptéry pro zachytávání** (povinné):<br>
     - Pro ATA Gateway na vyhrazeném serveru vyberte síťové adaptéry, které jsou nakonfigurované jako cílový port zrcadlení. Tyto budou přijímat zrcadlený provoz řadičů domén.
     - V případě ATA Lightweight Gateway by to měly být všechny síťové adaptéry, které se používají ke komunikaci s ostatními počítači ve vaší organizaci.

![Obrázek konfigurace nastavení brány](media/ATA-Config-GW-Settings.jpg)

 - **Kandidát na synchronizátora domény**<br>
Za synchronizaci mezi ATA a doménou Active Directory může být zodpovědná libovolná komponenta ATA Gateway, která je nastavená jako kandidát na synchronizátora domény. V závislosti na velikosti domény může počáteční synchronizace nějakou dobu trvat a je náročná na prostředky. Ve výchozím nastavení jako kandidáti na synchronizátora domény nastavené jenom komponenty ATA Gateway. <br>Doporučuje se zakázat komponentám ATA Gateway vzdálené lokality, aby byly kandidátem na synchronizátora domény.<br>Pokud je řadič domény jen pro čtení, nenastavujte ho jako kandidáta na synchronizátora domény. Další informace najdete v části [Architektura ATA](/advanced-threat-analytics/plan-design/ata-architecture#ata-lightweight-gateway-features).

> [!NOTE] 
> První spuštění služby ATA Gateway bude trvat několik minut, protože sestavuje mezipaměť analyzátorů zachytávání dat ze sítě.<br>
> Změny konfigurace se použijí v ATA Gateway při příští plánované synchronizaci mezi komponentami ATA Gateway a ATA Center.



    

3. Volitelně můžete nastavit [Syslog listener and Windows Event Forwarding Collection](configure-event-collection.md) (Naslouchací proces syslog a kolekce předávání událostí systému Windows). 
4. Zaškrtněte políčko pro **automatickou aktualizaci ATA Gateway**, aby se ve vydání příštích verzí při aktualizaci komponenty ATA Center automaticky aktualizovala tato komponenta ATA Gateway.
3.  Klikněte na **Uložit**.


## Ověření instalací
Chcete-li ověřit, že ATA Gateway je úspěšně nasazená, zkontrolujte následující:

1.  Zkontrolujte, že je služba **Microsoft Advanced Threat Analytics Gateway** spuštěná. Po uložení nastavení ATA Gateway může trvat několik minut, než se služba spustí.

2.  Pokud se služba nespustí, zkontrolujte soubor Microsoft.Tri.Gateway-Errors.log umístěný v následující výchozí složce, %programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs.

3.  Pomoc najdete v tématu [Řešení potíží s ATA](/advanced-threat-analytics/troubleshoot/troubleshooting-ata-known-errors).

4.  Pokud se jedná o první nainstalovanou komponentu ATA Gateway, přihlaste se ke konzole ATA za několik minut a otevřete podokno oznámení potáhnutím pravé strany obrazovky. Měli byste vidět seznam **Entities Recently Learned** (Nedávno zjištěné entity) na panelu oznámení na pravé straně konzoly.

5.  Na ploše klikněte na zástupce **Microsoft Advanced Threat Analytics** a připojte se ke konzole ATA. Přihlaste se pomocí stejných přihlašovacích údajů, které jste použili k instalaci ATA Center.
6.  V konzole něco vyhledejte v panelu vyhledávání, například uživatele nebo skupinu ve vaší doméně.
7.  Otevřete nástroj Sledování výkonu. Ve stromovém zobrazení Výkon klikněte na **Sledování výkonu** a potom klikněte na ikonu se znaménkem plus **Přidat čítač**. Rozbalte položku **Microsoft ATA Gateway** a přejděte dolů k položce **Network Listener PEF Captured Messages/Sec** (Zprávy zachycené komponentou PEF NetworkListener/s) a přidejte ji. Zkontrolujte, že v grafu vidíte aktivitu.

    ![Obrázek přidání čítačů výkonu](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Krok 4](install-ata-step4.md)
[Krok 6 »](install-ata-step6.md)

## Viz také

- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jun16_HO4-->


