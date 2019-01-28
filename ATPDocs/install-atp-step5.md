---
title: Nainstalovat Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Krok 5 instalace ochrany ATP v programu Azure vám pomůže nakonfigurovat nastavení pro samostatný senzor vaší ochrany ATP v programu Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cb9987645ffd1546b50117c984a138e8d3169657
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085261"
---
# <a name="install-azure-atp---step-5"></a>Instalace služby Azure ATP – krok 5

> [!div class="step-by-step"]
> [« Krok 4](install-atp-step4.md)
> [Krok 6 »](install-atp-step6-vpn.md)



## <a name="configure-azure-atp-sensor-settings"></a>Konfigurace nastavení senzoru služby Azure ATP
Po dokončení instalace senzoru služby Azure ATP proveďte následující postup pro konfiguraci nastavení senzoru služby Azure ATP.

1.  Na portálu ochrany ATP v programu Azure, přejděte na **konfigurace** a v části **systému** vyberte **senzorů**.
   
    ![Nakonfigurovat senzor nastavení image](media/atp-sensor-config.png)


2. Po kliknutí na senzor, který chcete nakonfigurovat a zadejte následující informace:

   ![Nakonfigurovat senzor nastavení image](media/atp-sensor-config-2.png)

   - **Popis**: Zadejte popis (nepovinné) senzoru služby Azure ATP.
   - **Řadiče domény (FQDN)** (vyžadováno pro služby Azure ATP samostatný senzor, toto chování nelze změnit pro senzoru služby Azure ATP): Zadejte úplný plně kvalifikovaný název domény řadiči domény a kliknutím na symbol plus ho přidejte do seznamu. Například **dc01.contoso.com**.

     Následující informace platí pro servery, které zadáte do seznamu **Řadiče domény**:
     - Všechny řadiče domény, jejichž provoz se monitoruje přes zrcadlení portů samostatný senzor ochrany ATP v programu Azure, musí být uvedené v **řadiče domény** seznamu. Pokud řadič domény není uvedený v seznamu **Řadiče domény**, detekce podezřelých aktivit nemusí fungovat podle očekávání.
     - Nejméně jeden řadič domény v seznamu by měl být globální katalog. To umožňuje ochrany ATP v programu Azure k vyřešení objekty počítačů a uživatelů v jiných doménách v doménové struktuře.

   - **Síťové adaptéry pro zachytávání** (povinné):
   
    - Pro služby Azure ATP senzory všechny síťové adaptéry, které se používají ke komunikaci s dalšími počítači ve vaší organizaci.
    - Samostatný senzor ochrany ATP v programu Azure na vyhrazený server vyberte síťové adaptéry, které jsou nakonfigurované jako cílový port zrcadlení. Tyto příjem provozu řadiče domény zrcadlené.

  - **Kandidát na synchronizátora domény**: 
    
    - Synchronizátor domény je zodpovědná za synchronizaci mezi ochrany ATP v programu Azure a vaší domény služby Active Directory. V závislosti na velikosti domény počáteční synchronizace může nějakou dobu trvat a je náročná. Ochrana ATP v programu Azure doporučuje nastavení alespoň jeden řadič domény jako kandidát na synchronizátora domény na doménu. Nepodařilo se vybrat aspoň jeden řadič domény jako kandidát na synchronizátora domény znamená, že ochrana ATP v programu Azure bude jenom pasivně kontroly sítě a nemusí být schopen shromažďovat všechny změny Active Directory a podrobnosti o entitách. Alespoň jeden určené **kandidát na synchronizátora domény** doménu zajistí ochrana ATP v programu Azure aktivně hledá v síti po celou dobu a může shromažďovat všechny změny Active Directory a hodnoty entit.
  
    - Ve výchozím nastavení senzory ochrany ATP v programu Azure nejsou uvedena kandidáti na synchronizátora domény, jsou samostatné senzorů ochrany ATP v programu Azure. Chcete-li ručně nastavit senzoru služby Azure ATP jako kandidát na synchronizátora domény, přepněte **kandidát na synchronizátora domény** přepněte možnost **ON** na obrazovce konfigurace.   
        
    - Doporučuje se, že zakážete všechny vzdálené lokality (čidly služby Azure ATP) nebudou kandidáti na synchronizátora domény.
   
    - Nenastavujte řadiče domény jen pro čtení jako kandidáti na synchronizátora domény. Další informace o synchronizaci služby Azure ATP domény najdete v tématu [architektura služby Azure ATP](atp-architecture.md#azure-atp-sensor-features).
  
3. Klikněte na **Uložit**.


## <a name="validate-installations"></a>Ověření instalací
Pokud chcete ověřit, že se úspěšně nasadil senzoru služby Azure ATP, zkontrolujte následující kroky:

1. Zkontrolujte, zda je služba **rozšířené ochrany před internetovými útoky pro Azure senzor** běží. Po uložení nastavení senzoru služby Azure ATP, může trvat několik sekund pro službu spustit.

2. Pokud služba nespustí, zkontrolujte soubor "Microsoft.Tri.sensor-Errors.log" umístěný v následující výchozí složce "%programfiles%\Azure rozšířené ochrany před internetovými útoky sensor\Version X\Logs".
 
   >[!NOTE]
   > Verze služby Azure ATP aktualizace často, zkontrolujte nejnovější verzi portálu ochrany ATP v programu Azure, přejděte na **konfigurace** a potom **o**. 

3. Přejděte na adresu URL instance služby Azure ATP. Na portálu ochrany ATP v programu Azure něco vyhledejte v panelu vyhledávání, například uživatele nebo skupinu ve vaší doméně.



> [!div class="step-by-step"]
> [« Krok 4](install-atp-step4.md)
> [Krok 6 »](install-atp-step6-vpn.md)



## <a name="see-also"></a>Viz také

- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
