---
title: "Instalace Advanced Threat Analytics – krok 7 | Dokumentace Microsoftu"
description: "V tomto kroku instalace ATA můžete integrovat vaši síť VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/9/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c02649a6acb6a083145ba81b3b9c1647e7f8ea2a
ms.sourcegitcommit: e9f2bfd610b7354ea3fef749275f16819d60c186
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/09/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="install-ata---step-7"></a>Instalace ATA – krok 7

>[!div class="step-by-step"]
[«Krok 5](install-ata-step5.md)
[krok 8»](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Krok 7: Integrovat sítě VPN

### <a name="configuring-vpn"></a>Konfigurace sítě VPN

ATA shromažďuje data sítě VPN, která pomáhá profil umístění, ze které počítače připojit k síti a jako dokáže detekovat nestandardní připojení k síti VPN.

Konfigurace sítě VPN data v ATA:

1. Přejděte na **konfigurace** a klikněte **VPN** kartě.

2. Zadejte **účet sdílený tajný klíč** serveru RADIUS. Chcete-li získat sdílený tajný klíč, naleznete v dokumentaci k síti VPN.

 ![Konfigurovat síť VPN ATA](media/vpn.png)

3.  Jakmile je tato možnost povolena, všechny komponenty ATA Gateway a Lightweight Gateway naslouchat na portu 1813 pro události monitorování účtů protokolu RADIUS. 

4.  Události monitorování účtů protokolu RADIUS sítě VPN mají předávat všechny komponenty ATA Gateway nebo ATA Lightweight Gateway to konfigurován.

5.  Po ATA Gateway přijímá VPN události a odesílá je ATA Center pro zpracování, ATA Center vyžaduje připojení k Internetu pro protokol HTTPS port 443 pro umět překládat externí IP adresy v událostech VPN na jejich informace o zeměpisné poloze.

Volání přeložit externí IP adresu na umístění jsou anonymní. Žádné osobní identifikátor se odešlou v toto volání.

Podporovaní dodavatelé sítí VPN:
- Microsoft
- F5
- Check Point
- Cisco ASA




>[!div class="step-by-step"]
[« Krok 6](install-ata-step5.md)
[Krok 8 »](install-ata-step7.md)



## <a name="related-videos"></a>Související videa
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Výběr správné typu ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/atasizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

