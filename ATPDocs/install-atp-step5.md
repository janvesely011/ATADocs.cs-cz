---
title: Konfigurace rychlého startu nastavení senzorů Azure ATP | Microsoft Docs
description: Krok pět pro instalaci Azure ATP vám pomůže nakonfigurovat nastavení pro samostatný senzor Azure ATP.
author: mlottner
ms.author: mlottner
ms.date: 07/17/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1c9f8d0928e7439afe9eb0745c07fad2c515169a
ms.sourcegitcommit: b7b3d4a401faaa3edb4bd669a1a003a6d21a4322
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2019
ms.locfileid: "68298913"
---
# <a name="quickstart-configure-azure-atp-sensor-settings"></a>Rychlý Start Konfigurace nastavení snímače ATP Azure

V tomto rychlém startu nakonfigurujete nastavení senzoru ATP Azure a začnete zobrazovat data. Abyste mohli využívat možnosti služby Azure ATP, budete muset provést další konfiguraci a integraci.  

## <a name="prerequisites"></a>Požadavky

- [Instance ATP Azure](install-atp-step1.md) , která je [připojená ke službě Active Directory](install-atp-step2.md).
- Stažená kopie balíčku pro [instalaci senzoru ATP](install-atp-step3.md) a přístupový klíč.

## <a name="configure-sensor-settings"></a>Konfigurovat nastavení senzoru

Po instalaci senzoru služby Azure ATP proveďte následující postup konfigurace nastavení senzoru ATP Azure.

1. Kliknutím na **Spustit** otevřete prohlížeč a přihlaste se k portálu Azure atp.

1.  Na portálu Azure ATP klikněte na **Konfigurace** a v části **systém** vyberte **senzory**.
   
    ![Obrázek konfigurace nastavení senzoru](media/atp-sensor-config.png)


1. Klikněte na senzor, který chcete nakonfigurovat, a zadejte následující informace:

   ![Obrázek konfigurace nastavení senzoru](media/atp-sensor-config-2.png)

   - **Popis**: Zadejte popis snímače ATP Azure (volitelné).
   - **Řadiče domény (FQDN)** (vyžaduje se pro samostatný senzor Azure ATP, ale nedá se změnit pro senzor Azure ATP.): Zadejte úplný plně kvalifikovaný název domény řadiči domény a kliknutím na symbol plus ho přidejte do seznamu. Například **dc01.contoso.com**.

     Následující informace platí pro servery, které zadáte do seznamu **Řadiče domény**:
     - Všechny řadiče domény, jejichž provoz se monitoruje pomocí zrcadlení portů, musí být v seznamu **řadiče domény** uvedeni. Pokud řadič domény není uvedený v seznamu **řadiče domény** , detekce podezřelých aktivit nemusí fungovat podle očekávání.
     - Nejméně jeden řadič domény v seznamu by měl být globální katalog. Díky tomu může Azure ATP vyřešit objekty počítačů a uživatelů v jiných doménách v doménové struktuře.

   - **Síťové adaptéry pro zachytávání** (povinné):
   
    - Pro senzory Azure ATP všechny síťové adaptéry, které se používají ke komunikaci s ostatními počítači ve vaší organizaci.
    - U samostatného senzoru služby Azure ATP na vyhrazeném serveru vyberte síťové adaptéry, které jsou nakonfigurované jako cílový port zrcadlení. Tyto síťové adaptéry dostanou zrcadlený provoz řadiče domény.

 
1. Klikněte na **Uložit**.


## <a name="validate-installations"></a>Ověření instalací
Pokud chcete ověřit, jestli se senzor Azure ATP úspěšně nasadil, zkontrolujte následující:

1. Ověřte, že je spuštěná služba s názvem **Azure Advanced Threat Protection snímač** . Po uložení nastavení senzoru Azure ATP může trvat několik sekund, než se služba spustí.

1. Pokud se služba nespustí, zkontrolujte soubor Microsoft. Tri. sensor-Errors. log umístěný v následující výchozí složce, "%programfiles%\Azure Advanced Threat Protection sensor\Version X\Logs".
 
   >[!NOTE]
   > Pravidelně se aktualizují verze Azure ATP, aby bylo možné zjistit nejnovější verzi, na portálu Azure ATP, přejít na **Konfigurace** a potom **o produktu**. 

1. Přejít na adresu URL vaší instance ATP Azure ATP. Na portálu Azure ATP vyhledejte něco na panelu hledání, například uživatele nebo skupinu ve vaší doméně.

1. Pomocí následujících kroků ověřte připojení ATP na libovolném zařízení s doménami:
    1. Otevření příkazového řádku
    1. Typ ```nslookup```
    1. Jako typ **Server** zadejte plně kvalifikovaný název domény nebo IP adresu řadiče domény, na kterém je senzor ATP nainstalovaný. Například ```server contosodc.contoso.azure```.
        - Nezapomeňte nahradit ContosoDC. contoso. Azure a contoso. Azure pomocí plně kvalifikovaného názvu domény vašeho senzoru ATP a názvu domény v uvedeném pořadí.
    1. Typ ```ls -d contoso.azure```
    1. Zopakujte kroky 3 a 4 pro každý senzor, který chcete testovat.  
    1. Z konzoly Azure ATP otevřete profil entity pro počítač, ze kterého jste spustili test připojení. 
    1. Zkontrolujte související logickou aktivitu a potvrďte připojení. 

    > [!NOTE] 
    >Pokud je řadič domény, který chcete otestovat, vaším prvním nasazeným senzorem, počkejte aspoň 15 minut, než se dokončí pokus o ověření související logické aktivity pro tuto doménu, aby back-end dokončil počáteční nasazení nezbytných mikroslužeb. kontrolér.

## <a name="next-steps"></a>Další postup

- [Konfigurace proxy serveru](configure-proxy.md)
- [Rozšířené zásady auditu](atp-advanced-audit-policy.md)
- [Konfigurace služby Azure ATP pro vzdálená volání do SAM](install-atp-step8-samr.md)


## <a name="join-the-community"></a>Připojte se ke komunitě

Máte k dispozici další otázky nebo zájem o projednávání Azure ATP a souvisejícího zabezpečení s ostatními? Připojte se ke [komunitě ATP Azure](https://aka.ms/azureatpcommunity) ještě dnes!
