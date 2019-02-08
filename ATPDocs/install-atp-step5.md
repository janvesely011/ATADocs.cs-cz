---
title: Konfigurace ochrany ATP v programu Azure quickstart nastavení senzor | Dokumentace Microsoftu
description: Krok 5 instalace ochrany ATP v programu Azure vám pomůže nakonfigurovat nastavení pro samostatný senzor vaší ochrany ATP v programu Azure.
author: mlottner
ms.author: mlottner
ms.date: 02/06/2018
ms.topic: quickstart
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 661e9ec9a40f45c0dc323b5a9d612b03a3128cb7
ms.sourcegitcommit: 96752da28f43896e7b8e5945947b32c4810bdff6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/07/2019
ms.locfileid: "55831442"
---
# <a name="quickstart-configure-azure-atp-sensor-settings"></a>Rychlý start: Konfigurace nastavení senzoru služby Azure ATP

V tomto rychlém startu budete konfigurovat nastavení senzoru služby Azure ATP se data začnou zobrazovat. Bude potřeba provést další konfiguraci a integraci a využijte výhod možností služby Azure ATP.  

## <a name="prerequisites"></a>Požadavky

- [Instance služby Azure ATP](install-atp-step1.md) to [připojeným ke službě Active Directory](install-atp-step2.md).
- Stažený kopie vašeho [ochrany ATP v programu senzor instalační balíček](install-atp-step3.md) a přístupový klíč.

## <a name="configure-sensor-settings"></a>Konfigurace nastavení senzor

Po dokončení instalace senzoru služby Azure ATP, proveďte následující kroky ke konfiguraci nastavení senzoru služby Azure ATP.

1.  Na portálu ochrany ATP v programu Azure, přejděte na **konfigurace** a v části **systému** vyberte **senzorů**.
   
    ![Nakonfigurovat senzor nastavení image](media/atp-sensor-config.png)


2. Po kliknutí na senzor, který chcete nakonfigurovat a zadejte následující informace:

   ![Nakonfigurovat senzor nastavení image](media/atp-sensor-config-2.png)

   - **Popis**: Zadejte popis (nepovinné) senzoru služby Azure ATP.
   - **Řadiče domény (FQDN)** (vyžadováno pro služby Azure ATP samostatný senzor, toto chování nelze změnit pro senzoru služby Azure ATP): Zadejte úplný plně kvalifikovaný název domény řadiči domény a kliknutím na symbol plus ho přidejte do seznamu. Například **dc01.contoso.com**.

     Následující informace platí pro servery, které zadáte do seznamu **Řadiče domény**:
     - Všechny řadiče domény, jejichž provoz se monitoruje přes zrcadlení portů samostatný senzor ochrany ATP v programu Azure, musí být uvedené v **řadiče domény** seznamu. Pokud řadič domény není uvedený v **řadiče domény** seznamu, detekce podezřelých aktivit nemusí fungovat podle očekávání.
     - Nejméně jeden řadič domény v seznamu by měl být globální katalog. To umožňuje ochrany ATP v programu Azure k vyřešení objekty počítačů a uživatelů v jiných doménách v doménové struktuře.

   - **Síťové adaptéry pro zachytávání** (povinné):
   
    - Pro služby Azure ATP senzory všechny síťové adaptéry, které se používají ke komunikaci s dalšími počítači ve vaší organizaci.
    - Samostatný senzor ochrany ATP v programu Azure na vyhrazený server vyberte síťové adaptéry, které jsou nakonfigurované jako cílový port zrcadlení. Tyto síťové adaptéry příjem provozu řadiče domény zrcadlené.

  - **Kandidát na synchronizátora domény**: 
    
    - Synchronizátor domény je zodpovědná za synchronizaci mezi ochrany ATP v programu Azure a vaší domény služby Active Directory. V závislosti na velikosti domény počáteční synchronizace může nějakou dobu trvat a je náročná. Ochrana ATP v programu Azure doporučuje nastavení alespoň jeden řadič domény jako kandidát na synchronizátora domény na doménu. Nepodařilo se vybrat aspoň jeden řadič domény jako kandidát na synchronizátora domény znamená, že ochrana ATP v programu Azure bude jenom pasivně kontroly sítě a nemusí být schopen shromažďovat všechny změny Active Directory a podrobnosti o entitách. Alespoň jeden určené **kandidát na synchronizátora domény** doménu zajistí ochrana ATP v programu Azure aktivně hledá v síti po celou dobu a může shromažďovat všechny změny Active Directory a hodnoty entit.
  
    - Ve výchozím nastavení senzory ochrany ATP v programu Azure nejsou kandidáti na synchronizátora domény, jsou samostatné senzorů ochrany ATP v programu Azure. Chcete-li ručně nastavit senzoru služby Azure ATP jako kandidát na synchronizátora domény, přepněte **kandidát na synchronizátora domény** přepněte možnost **ON** na obrazovce konfigurace.
        
    - Doporučuje se, že zakážete všechny vzdálené lokality (čidly služby Azure ATP) nebudou kandidáti na synchronizátora domény.
   
    - Řadiče domény jen pro čtení nemají nastavený jako kandidáti na synchronizátora domény. Další informace o synchronizaci služby Azure ATP domény najdete v tématu [architektura služby Azure ATP](atp-architecture.md#azure-atp-sensor-features).
  
3. Klikněte na **Uložit**.


## <a name="validate-installations"></a>Ověření instalací
Pokud chcete ověřit, že se úspěšně nasadil senzoru služby Azure ATP, zkontrolujte následující kroky:

1. Zkontrolujte, zda je služba **rozšířené ochrany před internetovými útoky pro Azure senzor** běží. Po uložení nastavení senzoru služby Azure ATP, může trvat několik sekund pro službu spustit.

2. Pokud se služba nespustí, zkontrolujte soubor "Microsoft.Tri.sensor-Errors.log" umístěný v následující výchozí složce "%programfiles%\Azure rozšířené ochrany před internetovými útoky sensor\Version X\Logs".
 
   >[!NOTE]
   > Verze služby Azure ATP aktualizace často, zkontrolujte nejnovější verzi portálu ochrany ATP v programu Azure, přejděte na **konfigurace** a potom **o**. 

3. Přejděte na adresu URL instance služby Azure ATP. Na portálu ochrany ATP v programu Azure něco vyhledejte v panelu vyhledávání, třeba na uživatele nebo skupinu ve vaší doméně.

## <a name="next-steps"></a>Další postup

- [Konfigurace proxy serveru](configure-proxy.md)
- [Pokročilé zásady auditu](atp-advanced-audit-policy.md)
- [Konfigurace služby Azure ATP pro vzdálená volání do SAM](install-atp-step8-samr.md)


## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://aka.ms/azureatpcommunity) ještě dnes!
