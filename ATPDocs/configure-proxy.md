---
title: Konfigurace proxy serveru nebo brány firewall pro povolení komunikace ATP Azure se senzorem | Microsoft Docs
description: Popisuje, jak nastavit bránu firewall nebo proxy server tak, aby umožňovala komunikaci mezi cloudovou službou Azure ATP a senzory Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 27630e93db4e103454e6d0fec7756824988ec4a2
ms.sourcegitcommit: 15f882cf45776877fdaca8367a7a0fe7f06a7917
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/23/2019
ms.locfileid: "71185507"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>Konfigurace nastavení proxy serveru Endpoint a připojení k Internetu pro senzor ATP Azure

Každý senzor služby Azure Advanced Threat Protection (ATP) vyžaduje k úspěšnému fungování cloudové službě Azure ATP připojení k Internetu. V některých organizacích nejsou řadiče domény přímo připojené k Internetu, ale jsou připojené prostřednictvím připojení k webovému proxy serveru. Každý senzor Azure ATP vyžaduje, abyste pomocí konfigurace Microsoft Windows Internet (WinINET) proxy serveru nahlásili data ze senzorů a komunikovali se službou Azure ATP. Pokud pro konfiguraci proxy serveru použijete WinHTTP, budete muset pro komunikaci mezi senzorem a cloudovou službou Azure ATP nakonfigurovat nastavení proxy prohlížeče pro Windows Internet (WinINet).

Při konfiguraci proxy serveru musíte mít jistotu, že vložená služba senzorů Azure ATP se spouští v kontextu systému pomocí účtu **LocalService** a že služba aktualizace senzorů Azure ATP běží v kontextu systému pomocí účtu **LocalSystem** . 

> [!NOTE]
> Pokud používáte transparentní proxy nebo WPAD v síťové topologii, nemusíte pro svůj proxy server nakonfigurovat rozhraní WinINET.

## <a name="configure-the-proxy"></a>Konfigurace proxy serveru 

Nastavení proxy serveru můžete nakonfigurovat během instalace senzoru pomocí parametrů definovaných v [tiché instalaci, nastavení ověřování proxy serveru](https://docs.microsoft.com/azure-advanced-threat-protection/atp-silent-installation#proxy-authentication).

### <a name="proxy-authentication"></a>Ověřování proxy

K dokončení ověřování proxy použijte následující příkazy:

**Syntaxe**:


> [!div class="mx-tableFixed"]
> 
> |Name|Syntaxe|Povinné pro bezobslužnou instalaci?|Popis|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl = "https\://proxy.contoso.com:8080"|Ne|Určuje ProxyUrl a číslo portu snímače ATP Azure.|
> |ProxyUserName|ProxyUserName = "Contoso\ProxyUser"|Ne|Pokud vaše proxy služba vyžaduje ověření, zadejte uživatelské jméno ve formátu doména \ uživatel.|
> |ProxyUserPassword|ProxyUserPassword = "P@ssw0rd"|Ne|Určuje heslo pro uživatelské jméno proxy serveru. \* Přihlašovací údaje jsou šifrované a ukládají se místně pomocí snímače ATP Azure.|

Proxy server můžete také nakonfigurovat ručně pomocí statického proxy serveru založeného na registru, aby senzor ATP v Azure mohl nahlásit diagnostická data a komunikovat s cloudovou službou Azure ATP, když počítač nemá oprávnění k připojení k Internetu.

> [!NOTE]
> Změny registru by se měly aplikovat jenom na LocalService a LocalSystem.

Statický proxy server lze konfigurovat prostřednictvím registru. Musíte zkopírovat konfiguraci proxy serveru, který používáte v kontextu uživatele, na LocalSystem a LocalService. Kopírování nastavení proxy kontextu uživatele:

1.   Před úpravou klíče registru nezapomeňte zálohovat.

2. V registru vyhledejte v klíči `DefaultConnectionSettings` `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` registru hodnotu REG_BINARY a zkopírujte ji.
 
2.  Pokud účet LocalSystem nemá správné nastavení proxy serveru (buď nejsou nakonfigurované, nebo se liší od Current_User), zkopírujte nastavení proxy serveru z Current_User na LocalSystem. Pod klíčem `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`registru.

3.  Vložte hodnotu z Current_user `DefaultConnectionSettings` jako REG_BINARY.

4.  Pokud LocalService nemá správné nastavení proxy serveru, zkopírujte nastavení proxy serveru z Current_User do LocalService. Pod klíčem `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings`registru.

5.  Vložte hodnotu z Current_User `DefaultConnectionSettings` jako REG_BINARY.

> [!NOTE]
> Tato akce bude mít vliv na všechny aplikace včetně služeb systému Windows, které využívají rozhraní WinINET s LocalSytem kontextem LocalService.


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>Povolení přístupu k adresám URL služby Azure ATP v proxy server

Pokud chcete povolit přístup ke službě Azure ATP, povolte provoz na následujících adresách URL:

- \<název-instance >. atp. Azure. com – pro připojení konzoly. Například "Contoso-corp.atp.azure.com"

- \<název-instance > sensorapi. atp. Azure. com – pro připojení senzorů. Například "contoso-corpsensorapi.atp.azure.com"

Předchozí adresy URL se automaticky mapují na správné umístění služby pro vaši instanci ATP Azure. Pokud potřebujete podrobnější kontrolu, zvažte povolení provozu do relevantních koncových bodů z následující tabulky:

|Umístění služby|*.atp.azure.com DNS record|
|----|----|
|USA |triprd1wcusw1sensorapi.atp.azure.com<br>triprd1wcuswb1sensorapi.atp.azure.com<br>triprd1wcuse1sensorapi.atp.azure.com|
|Evropa|triprd1wceun1sensorapi.atp.azure.com<br>triprd1wceuw1sensorapi.atp.azure.com|
|Asie|triprd1wcasse1sensorapi.atp.azure.com|

 
> [!NOTE]
> Za účelem zajištění maximálního zabezpečení a ochrany osobních údajů využívá Azure ATP vzájemné ověřování na základě certifikátů mezi jednotlivými senzory Azure ATP a cloudovým back-endu Azure ATP. Pokud se ve vašem prostředí používá kontrola SSL, ujistěte se, že je kontrola nakonfigurovaná pro vzájemné ověřování, takže není v procesu ověřování narušena.



## <a name="see-also"></a>Viz také
- [Konfigurace předávání událostí](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
