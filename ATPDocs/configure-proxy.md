---
title: Konfigurace proxy serveru nebo brány firewall k umožnění komunikace služby Azure ATP s daným senzorem | Dokumentace Microsoftu
description: Popisuje, jak nastavit brány firewall nebo proxy a povolit komunikaci mezi ochrany ATP v programu Azure cloudové služby a služby Azure ATP senzorů
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1ef76226f4f490687ff2437e657e0be240fa5e7f
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/23/2019
ms.locfileid: "54458715"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Konfigurace koncového bodu proxy serveru a nastavení připojení k Internetu pro vaše senzor ochrany ATP v programu Azure

Každý ze senzorů Azure Advanced Threat Protection (ATP) vyžaduje připojení k Internetu ke cloudové službě ochrana ATP v programu Azure správně fungovala. V některých organizacích řadiče domény nejsou připojené přímo k Internetu, ale jsou připojené prostřednictvím připojení k proxy serveru webových. Každý senzoru služby Azure ATP vyžaduje používat konfiguraci proxy serveru Microsoft Windows Internet (WinINET) na data ze senzorů sestavy a komunikovat se službou ochrana ATP v programu Azure. Pokud používáte konfiguraci proxy serveru WinHTTP, stále potřebujete ke konfiguraci proxy nastavení prohlížeče Internet Windows (WinINet) pro komunikaci mezi senzorem a cloudové službě ochrana ATP v programu Azure.


Při konfiguraci proxy serveru, budete muset vědět, že vložené službu sensor ochrany ATP v programu Azure běží v kontextu systému pomocí **LocalService** účet a službu Updater senzor ochrany ATP v programu Azure běží v kontextu systému pomocí  **LocalSystem** účtu. 

> [!NOTE]
> Pokud používáte transparentní proxy server nebo WPAD v topologii vaší sítě, není nutné konfigurovat WinINET pro váš proxy server.

## <a name="configure-the-proxy"></a>Konfigurace proxy serveru 

Konfigurace proxy serveru ručně pomocí založenou na registru statické proxy pro povolení ochrany ATP v programu Azure ze senzorů do sestavy diagnostická data a komunikovat s cloudovou službou ochrany ATP v programu Azure, když počítač není povolené pro připojení k Internetu.

> [!NOTE]
> Následující změny v registru, bude použito pouze do LocalService a LocalSystem.

Statické proxy je možné konfigurovat pomocí registru. Konfigurace proxy serveru, který používáte v kontextu uživatele musíte zkopírovat do localservice a localsystem. Zkopírování uživatelského kontextu nastavení serveru proxy:

1.   Ujistěte se, že k zálohování klíčů registru, před jejich úpravou.

2. V registru, vyhledejte hodnotu `DefaultConnectionSettings` jako REG_BINARY v klíči registru `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` a zkopírujte ho.
 
2.  Pokud LocalSystem nemá žádné nastavení proxy serveru správná (buď nejsou nakonfigurovány nebo jsou odlišné od Current_User), zkopírujte nastavení z Current_User k systému LocalSystem proxy serveru. V klíči registru `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

3.  Vložte hodnotu z Current_user `DefaultConnectionSettings` jako REG_BINARY.

4.  Pokud LocalService nemá žádné nastavení proxy serveru správná, zkopírujte nastavení z Current_User do LocalService proxy serveru. V klíči registru `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`.

5.  Vložte hodnotu z Current_User `DefaultConnectionSettings` jako REG_BINARY.

> [!NOTE]
> To ovlivní všechny aplikace, včetně služby Windows, které používají rozhraní WinINET s LocalService, LocalSytem kontextu.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Povolit přístup k adresám URL služby ochrany ATP v programu Azure v proxy serveru

Pokud proxy server nebo brána firewall blokuje veškerý provoz ve výchozím nastavení a umožňuje pouze konkrétní domény prostřednictvím nebo je povolenou komunikací HTTPS vyhledávání (kontroly protokolu SSL), ujistěte se, že následující adresy URL jsou uvedené prázdné, aby umožňovala komunikaci se službou Azure ATP v port 443:

|Umístění služby|.Atp.Azure.com DNS record|
|----|----|
|USA |triprd1wcusw1sensorapi.atp.azure.com<br>triprd1wcuswb1sensorapi.atp.azure.com<br>triprd1wcuse1sensorapi.atp.azure.com|
|Evropa|triprd1wceun1sensorapi.atp.azure.com<br>triprd1wceuw1sensorapi.atp.azure.com|
|Asie|triprd1wcasse1sensorapi.atp.azure.com|


Můžete také posílit ochranu firewall nebo proxy pravidla pro konkrétní instanci, že kterou jste vytvořili, tak, že vytvoříte pravidlo pro následující záznamy DNS:
- \<your-instance-name >. atp.azure.com – pro připojení konzoly. Například "Contoso-corp.atp.azure.com"
- \<your-instance-name > sensorapi.atp.azure.com – senzorů připojení. Například "contoso-corpsensorapi.atp.azure.com"

 
> [!NOTE]
> Provádí kontrolu SSL na síťový provoz služby Azure ATP (mezi senzorem a službu ochrany ATP v programu Azure), musí podporovat kontrolu SSL vzájemné kontroly.


## <a name="see-also"></a>Viz také
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)