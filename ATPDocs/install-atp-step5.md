---
title: Instalace Azure Advanced Threat Protection – krok 5 | Dokumentace Microsoftu
description: Krok 5 instalace ochrany ATP v programu Azure vám pomůže nakonfigurovat nastavení pro samostatný senzor vaší ochrany ATP v programu Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d7c95f8c-04f8-4946-9bae-c27ed362fcb0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 15e3639aa08e48a40ae65bf229964ae589ce1ba8
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454067"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="install-azure-atp---step-5"></a>Instalace služby Azure ATP – krok 5

> [!div class="step-by-step"]
> [« Krok 4](install-atp-step4.md)
> [Krok 6 »](install-atp-step6-vpn.md)


## <a name="step-5-configure-the-azure-atp-sensor-settings"></a>Krok 5: Konfigurace nastavení senzoru služby Azure ATP
Po dokončení instalace senzoru služby Azure ATP proveďte následující postup pro konfiguraci nastavení senzoru služby Azure ATP.

1.  Na portálu ochrany ATP v programu Azure pracovní prostor, přejděte na **konfigurace** a v části **systému**vyberte **senzor**.
   
     ![Nakonfigurovat senzor nastavení image](media/atp-sensor-config.png)


2.  Po kliknutí na senzor, který chcete nakonfigurovat a zadejte následující informace:

    ![Nakonfigurovat senzor nastavení image](media/atp-sensor-config-2.png)

  - **Popis**: Zadejte popis (nepovinné) senzoru služby Azure ATP.
  - **Řadiče domény (FQDN)** (vyžadováno pro služby Azure ATP samostatný senzor, toto chování nelze změnit pro senzoru služby Azure ATP): zadejte plně kvalifikovaný název domény řadiči domény a klikněte na symbol plus ho přidat do seznamu. Například **dc01.contoso.com**.

      Následující informace platí pro servery, které zadáte do seznamu **Řadiče domény**:
      - Všechny řadiče domény, jejichž provoz se monitoruje přes zrcadlení portů samostatný senzor ochrany ATP v programu Azure, musí být uvedené v **řadiče domény** seznamu. Pokud řadič domény není uvedený v seznamu **Řadiče domény**, detekce podezřelých aktivit nemusí fungovat podle očekávání.
      - Nejméně jeden řadič domény v seznamu by měl být globální katalog. To umožňuje ochrany ATP v programu Azure k vyřešení objekty počítačů a uživatelů v jiných doménách v doménové struktuře.

  - **Síťové adaptéry pro zachytávání** (povinné):
   
     - Pro senzoru služby Azure ATP to mělo být všechny síťové adaptéry, které se používají ke komunikaci s dalšími počítači ve vaší organizaci.
    - Pro Azure ATP samostatný senzor na vyhrazeném serveru vyberte síťové adaptéry, které jsou nakonfigurované jako cílový port zrcadlení. Tyto příjem provozu řadiče domény zrcadlené.

    - **Kandidát na synchronizátora domény**: ve výchozím nastavení, senzory ochrany ATP v programu Azure nejsou kandidáti na synchronizátora domény, jsou samostatné senzorů ochrany ATP v programu Azure. Chcete-li vybrat ručně senzoru služby Azure ATP jako kandidát syncronizer domény, přepněte **kandidát na synchronizátora domény** přepněte možnost **ON** na obrazovce konfigurace. 
    
        Synchronizátor domény je zodpovědná za synchronizaci mezi ochrany ATP v programu Azure a vaší domény služby Active Directory. Počáteční synchronizace v závislosti na velikosti domény může nějakou dobu trvat a je náročná. 
   Doporučuje se, že zakážete všechny vzdálené lokality (čidly služby Azure ATP) nebudou kandidáti na synchronizátora domény.
   Pokud je řadič domény jen pro čtení, nenastavujte ho jako kandidáta na synchronizátora domény. Další informace o synchronizaci služby Azure ATP domény najdete v tématu [architektura služby Azure ATP](atp-architecture.md#azure-atp-sensor-features)
  
4. Klikněte na **Uložit**.


## <a name="validate-installations"></a>Ověření instalací
Pokud chcete ověřit, že se úspěšně nasadil senzoru služby Azure ATP, zkontrolujte následující kroky:

1.  Zkontrolujte, zda je služba **rozšířené ochrany před internetovými útoky pro Azure senzor** běží. Po uložení nastavení senzoru služby Azure ATP, může trvat několik sekund pro službu spustit.

2.  Pokud služba nespustí, zkontrolujte soubor "Microsoft.Tri.sensor-Errors.log" umístěný v následující výchozí složce "%programfiles%\Azure rozšířené ochrany před internetovými útoky sensor\Version X\Logs".
 
 >[!NOTE]
 > Verze služby Azure ATP aktualizace často, zkontrolujte nejnovější verzi, na portálu ochrany ATP v programu Azure síti na pracovišti, přejděte na **konfigurace** a potom **o**. 

3.  Přejděte na adresu URL vašeho pracovního prostoru. Na portálu pro pracovní prostor něco vyhledejte v panelu vyhledávání, například uživatele nebo skupinu ve vaší doméně.



> [!div class="step-by-step"]
> [« Krok 4](install-atp-step4.md)
> [Krok 6 »](install-atp-step6-vpn.md)


## <a name="see-also"></a>Viz také

- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
