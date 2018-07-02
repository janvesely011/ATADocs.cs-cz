---
title: Konfigurace proxy serveru nebo brány firewall k umožnění komunikace služby Azure ATP s daným senzorem | Dokumentace Microsoftu
description: Popisuje, jak nastavit brány firewall nebo proxy a povolit komunikaci mezi ochrany ATP v programu Azure cloudové služby a služby Azure ATP senzorů
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/29/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2f39c0d3628c3a3cc9e034fa1da8bb5a66bc704b
ms.sourcegitcommit: 3eade64779002d2c8ae005565bc69e1b3f89fb7d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/05/2018
ms.locfileid: "34560237"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Konfigurace koncového bodu proxy serveru a nastavení připojení k Internetu pro vaše senzor ochrany ATP v programu Azure

Každý ze senzorů Azure Advanced Threat Protection (ATP) vyžaduje připojení k Internetu ke cloudové službě ochrana ATP v programu Azure správně fungovala. V některých organizacích řadiče domény nejsou připojené přímo k Internetu, ale jsou připojené prostřednictvím připojení k proxy serveru webových. Každý senzoru služby Azure ATP vyžaduje používat konfiguraci proxy serveru Microsoft Windows Internet (WinINET) na data ze senzorů sestavy a komunikovat se službou ochrana ATP v programu Azure. Pokud používáte konfiguraci proxy serveru WinHTTP, stále potřebujete ke konfiguraci proxy nastavení prohlížeče Internet Windows (WinINet) pro komunikaci mezi senzorem a cloudové službě ochrana ATP v programu Azure.


Při konfiguraci proxy serveru, budete muset vědět, že vložené službu sensor ochrany ATP v programu Azure běží v kontextu systému pomocí **LocalService** účet a službu Updater senzor ochrany ATP v programu Azure běží v kontextu systému pomocí **LocalSystem** účtu. 

> [!NOTE]
> Pokud používáte transparentní proxy server nebo WPAD v topologii vaší sítě, není potřeba konfigurovat WinINET pro váš proxy server.

## <a name="configure-the-proxy"></a>Konfigurace proxy serveru 

Konfigurace proxy serveru ručně pomocí založenou na registru statické proxy pro povolení ochrany ATP v programu Azure ze senzorů do sestavy diagnostická data a komunikovat s cloudovou službou ochrany ATP v programu Azure, když počítač není povolené pro připojení k Internetu.

> [!NOTE]
> Následující změny v registru, bude použito pouze do LocalService a LocalSystem.

Statické proxy je možné konfigurovat pomocí registru. Konfigurace proxy serveru, který používáte v kontextu uživatele musíte zkopírovat do localservice a localsystem. Zkopírování uživatelského kontextu nastavení serveru proxy:

1.   Ujistěte se, že k zálohování klíčů registru, před jejich úpravou.

2. V registru, vyhledejte hodnotu `DefaultConnectionSetting` jako REG_BINARY v klíči registru `HKCU\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting` a zkopírujte ho.
 
2.  Pokud LocalSystem nemá žádné nastavení proxy serveru správná (buď nejsou nakonfigurovány nebo jsou odlišné od Current_User), zkopírujte nastavení z Current_User k systému LocalSystem proxy serveru. V klíči registru `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

3.  Vložte hodnotu z Current_user `DefaultConnectionSetting` jako REG_BINARY.

4.  Pokud LocalService nemá žádné nastavení proxy serveru správná, zkopírujte nastavení z Current_User do LocalService proxy serveru. V klíči registru `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

5.  Vložte hodnotu z Current_User `DefaultConnectionSetting` jako REG_BINARY.

> [!NOTE]
> To ovlivní všechny aplikace, včetně služby Windows, které používají rozhraní WinINET s LocalService, LocalSytem kontextu.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Povolit přístup k adresám URL služby ochrany ATP v programu Azure v proxy serveru

Pokud proxy server nebo brána firewall blokuje veškerý provoz ve výchozím nastavení a umožňuje pouze konkrétní domény prostřednictvím nebo je povolenou komunikací HTTPS vyhledávání (kontroly protokolu SSL), ujistěte se, že následující adresy URL jsou uvedené prázdné, aby umožňovala komunikaci se službou Azure ATP v port 443:

|Umístění služby|. Záznam Atp.Azure.com DNS|
|----|----|
|USA |triprd1wcusw1sensorapi.ATP.Azure.com<br>triprd1wcuswb1sensorapi.ATP.Azure.com<br>triprd1wcuse1sensorapi.ATP.Azure.com|
|Evropa|triprd1wceun1sensorapi.ATP.Azure.com<br>triprd1wceuw1sensorapi.ATP.Azure.com|
|Asie|triprd1wcasse1sensorapi.ATP.Azure.com|


Můžete také posílit ochranu firewall nebo proxy pravidla pro konkrétní pracovní prostor, že kterou jste vytvořili, tak, že vytvoříte pravidlo pro následující záznamy DNS:
- < název pracovního prostoru >. atp.azure.com – pro připojení konzoly. Například contosoATP.atp.azure.com
- < název pracovního prostoru > sensorapi.atp.azure.com – senzorů připojení. Například contosoATPsensorapi.atp.azure.com

 
> [!NOTE]
> Provádí kontrolu SSL na síťový provoz služby Azure ATP (mezi senzorem a službu ochrany ATP v programu Azure), musí podporovat kontrolu SSL vzájemné kontroly.


## <a name="see-also"></a>Viz také
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)