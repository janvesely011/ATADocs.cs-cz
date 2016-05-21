---
# required metadata

title: Instalace ATA – Krok 5 | Microsoft Advanced Threat Analytics
description: Krok 5 instalace ATA vám pomůže nakonfigurovat nastavení pro komponentu ATA Gateway.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 2a5b6652-2aef-464c-ac17-c7e5f12f920f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Instalace ATA – Krok 5

>[!div class="step-by-step"]
[« Krok 4](install-ata-step4.md)
[Krok 6 »](install-ata-step6.md)


## Krok 5. Konfigurace nastavení ATA Gateway
Po instalaci komponenty ATA Gateway proveďte následující kroky a nakonfigurujte nastavení ATA Gateway.

1.  Z konzole ATA na počítači ATA Gateway klikněte na **Konfigurace** a vyberte stránku **ATA Gateways**.

2.  Zadejte následující informace.



  - **Popis**: <br>Zadejte popis ATA Gateway (nepovinné).
  - **Řadiče domény** (povinné): <br>Níže naleznete další informace o seznamu řadičů.<br>Zadejte úplný plně kvalifikovaný název domény řadiči domény a kliknutím na symbol plus ho přidejte do seznamu. Například **dc01.contoso.com**.<br /><br />![Obrázek příkladu plně kvalifikovaného názvu domény](media/ATAGWDomainController.png)<br>Objekty v prvním řadiči domény v seznamu se budou synchronizovat prostřednictvím dotazů protokolu LDAP. V závislosti na velikosti domény to může chvíli trvat.<br>
  **Poznámka:** <br>Ujistěte se, že první řadič domény **není** jen pro čtení. Řadiče domény jen pro čtení se můžou přidávat až po dokončení počáteční synchronizace.<br>


 - **Síťové adaptéry pro zachytávání** (povinné):<br>Vyberte síťové adaptéry, které jsou připojené k přepínači a které jsou nakonfigurované jako cílový port zrcadlení pro příjem provozu řadiče domény.|Vyberte síťový adaptér pro zachytávání.
    ![Obrázek konfigurace nastavení brány](media/ATA-Config-GW-Settings.jpg)

3.  Klikněte na **Uložit**..

    > [!NOTE]
    > První spuštění služby ATA Gateway bude trvat několik minut, protože sestavuje mezipaměť analyzátorů zachytávání dat ze sítě, které používá ATA Gateway.

Následující informace platí pro servery, které zadáte do seznamu **Řadiče domény**.

-   První řadič domény v seznamu použije ATA Gateway k synchronizaci objektů v doméně pomocí dotazů protokolu LDAP. V závislosti na velikosti domény to může chvíli trvat.

-   Všechny řadiče domény, jejichž provoz ATA Gateway monitoruje přes zrcadlení portů, musí být uvedené v seznamu **Řadiče domény**. Pokud řadič domény není uvedený v seznamu **Řadiče domény**, detekce podezřelých aktivit nemusí fungovat podle očekávání.

-   Ujistěte se, že první řadič domény **není** řadičem domény jen pro čtení (RODC).

    Řadiče domény jen pro čtení se můžou přidávat až po dokončení počáteční synchronizace.

-   Nejméně jeden řadič domény v seznamu musí být server globálního katalogu. Tak může ATA překládat objekty počítačů a uživatelů v jiných doménách v doménové struktuře.

Změny konfigurace se použijí v ATA Gateway při příští plánované synchronizaci mezi komponentami ATA Gateway a ATA Center.

### Ověření instalace:
Chcete-li ověřit, že ATA Gateway je úspěšně nasazená, zkontrolujte následující:

1.  Zkontrolujte, že je služba Microsoft Advanced Threat Analytics Gateway spuštěná. Po uložení nastavení ATA Gateway může trvat několik minut, než se služba spustí.

2.  Pokud se služba nespustí, zkontrolujte soubor Microsoft.Tri.Gateway-Errors.log umístěný v následující výchozí složce, %programfiles%\Microsoft Advanced Threat Analytics\Gateway\Logs, a vyhledejte položky s textem „transfer“ nebo „service start“.

3.  Zkontrolujte následující čítače výkonu Microsoft ATA Gateway:

    -   **NetworkListener Captured Messages / sec** (Zprávy zachycené komponentou NetworkListener/s): Tento čítač sleduje, kolik zpráv zachytí ATA za sekundu. Hodnota by měla být od několika set k tisícům v závislosti na počtu monitorovaných řadičů domény a na jejich vytížení. Jednociferné nebo dvouciferné hodnoty můžou značit problém s konfigurací zrcadlení portů.

    -   **EntityTransfer Activity Transfers/Sec** (Přenosy aktivit komponenty EntityTransfer/s): Tato hodnota by měla být v rozsahu několik stovek každých několik sekund.

4.  Pokud se jedná o první nainstalovanou komponentu ATA Gateway, přihlaste se ke konzole ATA za několik minut a otevřete podokno oznámení potáhnutím pravé strany obrazovky. Měli byste vidět seznam **Entities Recently Learned** (Nedávno zjištěné entity) na panelu oznámení na pravé straně konzoly.

5.  Ověření, že je instalace úspěšně dokončená:

    V konzole něco vyhledejte v panelu vyhledávání, například uživatele nebo skupinu ve vaší doméně.

    Otevřete nástroj Sledování výkonu. Ve stromovém zobrazení Výkon klikněte na **Sledování výkonu** a potom klikněte na ikonu se znaménkem plus **Přidat čítač**. Rozbalte položku **Microsoft ATA Gateway** a přejděte dolů k položce **Network Listener Captured Messages per Second** (Zprávy zachycené komponentou NetworkListener/s) a přidejte ji. Zkontrolujte, že v grafu vidíte aktivitu.

    ![Obrázek přidání čítačů výkonu](media/ATA-performance-monitoring-add-counters.png)


>[!div class="step-by-step"]
[« Krok 4](install-ata-step4.md)
[Krok 6 »](install-ata-step6.md)

## Viz také

- [Podporu získáte na našem fóru!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurace shromažďování událostí](/advanced-threat-analytics/plan-design/configure-event-collection)
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=Apr16_HO4-->


