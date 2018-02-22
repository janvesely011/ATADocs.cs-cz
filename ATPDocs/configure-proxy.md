---
title: "Konfigurace proxy serveru nebo brány firewall tak, aby Azure ATP komunikace s senzoru | Microsoft Docs"
description: "Popisuje, jak nastavit brány firewall nebo proxy server a povolit komunikaci mezi Azure ATP cloud service a Azure ATP senzorů"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 47fa5ad5d6fb7800c7df4b878d16ec335e2b70e5
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="configure-your-proxy-to-allow-communication-between-azure-atp-sensors-and-the-azure-atp-cloud-service"></a>Konfigurace proxy a povolit komunikaci mezi Azure ATP senzory a cloudové služby Azure ATP

Pro řadiče domény ke komunikaci s cloudovou službou, je nutné otevřít: *. atp.azure.com portu 443 v bráně firewall nebo proxy serveru. Konfigurace musí být na úrovni počítače (= účet počítače) a ne na úrovni účtu uživatele. Jste mohli otestovat vaši konfiguraci pomocí následujících kroků:
 
1.  Potvrďte, že **aktuální uživatel** má přístup ke koncovému bodu procesoru pomocí Internet Exploreru, procházením následující adresu URL z řadiče domény: https://triprd1wcuse1sensorapi.eastus.cloudapp.azure.com (pro USA), měli byste obdržet chyby 503:

 ![Služba není k dispozici](/media/service-unavailable.png)
 
2.  Pokud obdržíte chybu 503, zkontrolujte konfiguraci proxy serveru a zkuste to znovu.

3.  Pokud konfiguraci proxy serveru funguje pro **CURRENT_USER** (to znamená, zobrazí tato chyba 503) potom zkontrolujte, zda jsou nastavení proxy serveru WinInet povolena pro **LOCAL_SYSTEM** účtu (používané aktualizační senzor služby) tak, že v příkazovém řádku se zvýšenými oprávněními spustíte následující příkaz:
 
    REG porovnat "HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" "HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" /v DefaultConnectionSettings

Pokud se zobrazí chyba "Chyba: Nelze najít zadaný klíč registru nebo hodnotu." To znamená, že byl nastaven žádný proxy server **LOCAL_SYSTEM** úroveň
 
 ![Chyba místní systém proxy](/media/proxy-local-system-error.png)

Pokud je výsledek "výsledek porovnání: různé" to znamená, že je pro nastavit proxy server **LOCAL_SYSTEM** ale není to stejné jako **CURRENT_USER**:
 
  ![Porovnávaný výsledek proxy](/media/proxy-result-compared.png)

5.  Pokud **LOCAL_SYSTEM** nemá nastavení správné proxy (nakonfigurován nebo liší od **CURRENT_USER**), pak budete muset zkopírovat nastavení z proxy serveru **CURRENT_ Uživatel** k **LOCAL_SYSTEM**. Ujistěte se, že jste před zahájením úprav zálohovat tento klíč registru:

 Aktuální uživatelský klíč: HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings "místní systém klíč: HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\ DefaultConnectionSettings"

 
6.  Proveďte kroky 4 a 5 pro**Local_Service** účtu (je stejný jako **Local_System** ale měl by být S-1-5-19 místo S-1-5-18.



## <a name="see-also"></a>Viz také
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)