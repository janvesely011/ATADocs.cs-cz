---
title: Instalace Advanced Threat Analytics – krok 7 | Dokumentace Microsoftu
description: V tomto kroku instalace ATA můžete integrovat vaši síť VPN.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f98dfb3f5688f143a490a8ab7abb7eea7d8da5d9
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65197030"
---
# <a name="install-ata---step-7"></a>Instalace ATA – krok 7

*Platí pro: Advanced Threat Analytics verze 1.9*

> [!div class="step-by-step"]
> [«Krok 5](install-ata-step5.md)
> [krok 8»](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Krok 7: Integrace sítě VPN

Microsoft Advanced Threat Analytics (ATA) verze 1.8 může shromažďovat informace o monitorování účtů z řešení sítě VPN. Při konfiguraci, uživatelského profilu obsahovat informace z připojení VPN, jako je například IP adresy a umístění, původu připojení. To tím, že poskytuje další informace o aktivitě uživatelů doplňuje procesu šetření. Volání překládat externí IP adresu na umístění je anonymní. Žádné osobní identifikátor se posílá ve toto volání.

ATA se integruje s řešení sítě VPN prostřednictvím naslouchání události monitorování účtů protokolu RADIUS předávány do komponenty ATA Gateway. Tento mechanismus je založen na standardní monitorování účtů protokolu RADIUS ([RFC 2866](https://tools.ietf.org/html/rfc2866)), a podporují těchto dodavatelů VPN:

-   Microsoft
-   F5
-   Cisco ASA

## <a name="prerequisites"></a>Požadavky

Povolení integrace sítě VPN, ujistěte se, že můžete nastavit následující parametry:

-   Otevřete port UDP 1813 na komponenty ATA Gateway a ATA Lightweight Gateway.

-   Komponenty ATA Center musí mít přístup k *ti.ata.azure.com* pomocí protokolu HTTPS (port 443), aby ji mohl zadávat dotazy umístění příchozí IP adresy.

Následující příklad používá Microsoft Routing a Server pro vzdálený přístup (RRAS) k popisu proces konfigurace sítě VPN.

Pokud používáte řešení VPN třetích stran, si projděte jejich dokumentaci pokyny o tom, jak povolit monitorování účtů protokolu RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Nakonfigurujte monitorování účtů protokolu RADIUS sítě VPN systému

Proveďte následující kroky na serveru RRAS.
 
1.  Otevřete konzolu pro směrování a vzdálený přístup.
2.  Klikněte pravým tlačítkem na název serveru a klikněte na tlačítko **vlastnosti**.
3.  V **zabezpečení** ve skupině **zprostředkovatel účtování**vyberte **monitorování účtů protokolu RADIUS** a klikněte na tlačítko **konfigurovat**.

    ![Nastavení protokolu RADIUS](./media/radius-setup.png)

4.  V **přidat Server protokolu RADIUS** okno, zadejte **název serveru** nejbližší ATA Gateway nebo ATA Lightweight Gateway. V části **Port**, ujistěte se, že je nakonfigurovaný výchozí 1813. Klikněte na tlačítko **změnu** a zadejte nový sdílený tajný řetězec alfanumerických znaků, které si zapamatujete. Je potřeba vyplnit později v konfiguraci ATA. Zkontrolujte **zprávy odesílat účtu RADIUS On a vypnutém** pole a potom klikněte na tlačítko **OK** na všechna otevřená dialogová okna.
 
     ![Nastavení sítě VPN](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>Konfigurace sítě VPN v ATA

ATA shromažďuje data sítě VPN a identifikuje, kdy a kde se právě používají přihlašovací údaje přes síť VPN a integruje data do šetření. To poskytuje další informace, které vám pomůžou zjistit, výstrahy, které oznamují řešením ATA.

Data sítě VPN nakonfigurujete v ATA:

1. V konzole ATA, otevřete stránku konfigurace ATA a přejděte na **VPN**.
 
   ![Konfigurační nabídka ATA](./media/config-menu.png)

2. Zapnout **monitorování účtů protokolu Radius**a zadejte **sdílený tajný klíč** jste dříve nakonfigurovali na serveru RRAS VPN. Potom klikněte na **Uložit**.
 

  ![Konfigurovat síť VPN pro ATA](./media/vpn.png)


Jakmile je tato možnost povolena, všechny komponenty ATA Gateway a Lightweight Gateway naslouchání na portu 1813 události monitorování účtů protokolu RADIUS. 

Vaše instalace byla dokončena a nyní je vidět aktivitu sítě VPN v profilu uživatele:
 
   ![Nastavení sítě VPN](./media/vpn-user.png)

Poté, co ATA Gateway přijímá události VPN a odesílá do ATA Center pro zpracování, ATA Center potřebuje přístup k *ti.ata.azure.com* umět přeložit externí IP adresy v události VPN, které chcete pomocí protokolu HTTPS (port 443) jejich zeměpisné umístění.




> [!div class="step-by-step"]
> [« Krok 6](install-ata-step5.md)
> [Krok 8 »](install-ata-step7.md)



## <a name="related-videos"></a>Související videa
- [Přehled nasazení ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Volba správného typu komponenty ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Viz také
- [Průvodce nasazením ATA POC](http://aka.ms/atapoc)
- [Nástroje pro změnu velikosti ATA](http://aka.ms/aatpsizingtool)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky ATA](ata-prerequisites.md)

