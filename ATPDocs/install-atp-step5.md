---
title: Instalace Azure Advanced Threat Protection – krok 5 | Microsoft Docs
description: Krok 5 instalace Azure ATP vám pomůže nakonfigurovat nastavení pro vaše senzor samostatné Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a2e61758e06aedfe607afc0d3365227af872fe20
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
ms.locfileid: "29446033"
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-5"></a>Nainstalovat Azure ATP – krok 5

>[!div class="step-by-step"]
[« Krok 4](install-atp-step4.md)
[Krok 6 »](install-atp-step6-vpn.md)


## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>Krok 5: Nakonfigurujte nastavení senzor Azure ATP
Po instalaci Azure ATP senzoru, proveďte následující kroky ke konfiguraci nastavení pro Azure ATP senzoru.

1.  Na portálu Azure ATP pracovního prostoru, přejděte na **konfigurace** a v části **systému**, vyberte **senzor**.
   
     ![Obrázek nastavení senzor konfigurace](media/atp-sensor-config.png)


2.  Klikněte na senzor, který chcete konfigurovat a zadejte následující informace:

    ![Obrázek nastavení senzor konfigurace](media/atp-sensor-config-2.png)

  - **Popis**: Zadejte popis (nepovinné) Azure ATP senzoru.
  - **Řadiče domény (FQDN)** (vyžaduje samostatné senzoru Azure ATP, toto chování nelze změnit senzoru Azure ATP): zadejte plně kvalifikovaný název domény řadiči domény a klikněte na symbol plus ho přidejte do seznamu. Například **dc01.contoso.com**.

      Následující informace platí pro servery, které zadáte do seznamu **Řadiče domény**:
      - Všechny řadiče domény, jejichž provoz je monitoruje přes zrcadlení portů senzoru samostatné Azure ATP musí být uvedené v **řadiče domény** seznamu. Pokud řadič domény není uvedený v seznamu **Řadiče domény**, detekce podezřelých aktivit nemusí fungovat podle očekávání.
      - Nejméně jeden řadič domény v seznamu by měl být globální katalog. To umožňuje Azure ATP překládat objekty počítačů a uživatelů v jiných doménách v doménové struktuře.

  - **Síťové adaptéry pro zachytávání** (povinné):
     - Pro samostatné služby Azure ATP senzor na vyhrazeném serveru vyberte síťové adaptéry, které jsou nakonfigurované jako cílový port zrcadlení. Tyto přijímat zrcadlený provoz řadičů domén.
     - Pro služby Azure ATP senzor to musí být všechny síťové adaptéry, které se používají ke komunikaci s dalšími počítači ve vaší organizaci.


  - **Kandidát na synchronizátora domény**: senzor samostatné Any Azure ATP nastavená jako kandidát na synchronizátora domény může být zodpovědná za synchronizaci mezi Azure ATP a doméně služby Active Directory. V závislosti na velikosti domény počáteční synchronizace může chvíli trvat a je náročná. Pouze samostatné senzorů Azure ATP jsou ve výchozím nastavení jako kandidáti na synchronizátora domény.
   Doporučuje se, že zakážete všechny vzdálené lokality Azure ATP senzor nebudou kandidáti na synchronizátora domény.
   Pokud je řadič domény jen pro čtení, nenastavujte ho jako kandidáta na synchronizátora domény. Další informace najdete v tématu [Azure ATP architektura](atp-architecture.md#azure-atp-sensor-features).
  
4. Klikněte na **Uložit**.


## <a name="validate-installations"></a>Ověření instalací
Chcete-li ověřit, že senzoru Azure ATP byla úspěšně nasazena, zkontrolujte následující kroky:

1.  Zkontrolujte, zda je služba **Azure Advanced Threat Protection senzor** běží. Po uložení nastavení senzor Azure ATP může trvat několik sekund pro službu spustit.

2.  Pokud se služba nespustí, zkontrolujte soubor "Microsoft.Tri.sensor-Errors.log" umístěný v následující výchozí složce "%programfiles%\Azure pokročilé ochrana před internetovými útoky sensor\Version X\Logs".
 
 >[!NOTE]
 > Verze aktualizace Azure ATP často, zkontrolujte na nejnovější verzi, na portálu Azure ATP síti na pracovišti, přejděte na **konfigurace** a potom **o**. 

3.  Přejděte na adresu URL pracovního prostoru. Na portálu prostoru vyhledávání v panelu vyhledávání, například uživatele nebo skupinu ve vaší doméně.



>[!div class="step-by-step"]
[« Krok 4](install-atp-step4.md)
[Krok 6 »](install-atp-step6-vpn.md)


## <a name="see-also"></a>Viz také

- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
