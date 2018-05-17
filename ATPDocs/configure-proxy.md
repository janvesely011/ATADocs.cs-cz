---
title: Konfigurace proxy serveru nebo brány firewall tak, aby Azure ATP komunikace s senzoru | Microsoft Docs
description: Popisuje, jak nastavit brány firewall nebo proxy server a povolit komunikaci mezi Azure ATP cloud service a Azure ATP senzorů
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/16/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5a1fd5631a568419c600f35d44f09c9c61f17129
ms.sourcegitcommit: 714a01edc9006b38d1163d03852dafc2a5fddb5f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Konfigurace koncového bodu proxy serveru a nastavení připojení k Internetu pro vaše senzor ATP Azure

Každý senzor Azure Advanced Threat Protection (ATP) vyžaduje připojení k Internetu ke cloudové službě Azure ATP správně fungovala. V některých organizacích řadiče domény nejsou připojené přímo k Internetu, ale jsou připojené prostřednictvím připojení k webové proxy. Každý senzor Azure ATP vyžaduje, abyste používat konfiguraci proxy serveru Microsoft Windows Internet (WinINET) pro data snímačů sestavy a komunikovat se službou Azure ATP. Pokud používáte pro konfiguraci proxy serveru WinHTTP, stále potřebujete nakonfigurovat nastavení proxy Internetu systému Windows (WinINet) prohlížeče pro komunikaci mezi senzoru a cloudové služby Azure ATP.


Při konfiguraci proxy serveru, budete muset vědět, že embedded Azure ATP senzor služba bude spuštěna v systému pomocí kontextu **LocalService** účet a Azure ATP senzor aktualizační službu běží v kontextu systému pomocí **LocalSystem** účtu. 

> [!NOTE]
> Pokud používáte transparentní server proxy nebo WPAD v topologii vaší sítě, není potřeba konfigurovat WinINET pro proxy.

## <a name="configure-the-proxy"></a>Konfigurace proxy serveru 

Nakonfigurujte proxy server ručně pomocí založenou na registru statické proxy, aby bylo možné senzor Azure ATP do sestavy diagnostických dat a komunikovat s cloudovou službou Azure ATP, když počítač nemá oprávnění k připojení k Internetu.

> [!NOTE]
> Změny registru bude použito pouze pro účely LocalService a účet LocalSystem.

Statické proxy je lze změnit v nastavení registru. Localsystem a localservice musíte zkopírovat konfiguraci proxy serveru, který můžete použít v kontextu uživatele. Kopírování vaše nastavení proxy serveru kontext uživatele:

1.   Ujistěte se, že před jejich úpravou klíče registru zálohovat.

2. V registru, vyhledejte hodnotu `DefaultConnectionSetting` jako REG_BINARY v klíči registru `HKCU\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting` a zkopírujte ho.
 
2.  Pokud účet LocalSystem nemá nastavení správné proxy (nejsou nakonfigurovány nebo jsou liší od Current_User), pak zkopírujte nastavení z Current_User oprávnění LocalSystem proxy serveru. V klíči registru `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

3.  Vložit hodnotu z Current_user `DefaultConnectionSetting` jako REG_BINARY.

4.  Pokud LocalService nemá nastavení proxy serveru správný, poté zkopírujte nastavení z Current_User k LocalService proxy serveru. V klíči registru `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting`.

5.  Vložit hodnotu z Current_User `DefaultConnectionSetting` jako REG_BINARY.

> [!NOTE]
> Tato akce ovlivní všechny aplikace, včetně služby systému Windows, které používají WinINET s LocalService LocalSytem kontextu.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Povolit přístup k adresám URL služby Azure ATP v proxy serveru

Pokud server proxy nebo brány firewall blokuje veškerý provoz ve výchozím nastavení a povolení jenom konkrétní domény prostřednictvím nebo HTTPS kontrolu (kontrolu SSL) je povoleno, ujistěte se, že následující adresy URL jsou uvedené prázdné, aby umožňovala komunikaci se službou Azure ATP v portu 443:

|Umístění služby|. Záznam Atp.Azure.com DNS|
|----|----|
|NÁM |triprd1wcusw1sensorapi.ATP.Azure.com<br>triprd1wcuswb1sensorapi.ATP.Azure.com<br>triprd1wcuse1sensorapi.ATP.Azure.com|
|Evropa|triprd1wceun1sensorapi.ATP.Azure.com<br>triprd1wceuw1sensorapi.ATP.Azure.com|
|Asie|triprd1wcasse1sensorapi.ATP.Azure.com|


Kvůli posílení zabezpečení brány firewall nebo proxy server pravidla pro určitý pracovní prostor, že jste vytvořili, a vytvoření pravidla pro tyto záznamy DNS:
- < název pracovního prostoru >. atp.azure.com – pro připojení konzoly
- < název pracovního prostoru > sensorapi.atp.azure.com – senzor připojení k
 
> [!NOTE]
> Při provádění kontroly protokolu SSL na síti Azure ATP (mezi senzoru a službou Azure ATP), musí podporovat kontrolu SSL vzájemné kontroly.


## <a name="see-also"></a>Viz také
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)