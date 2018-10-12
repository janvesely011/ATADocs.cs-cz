---
title: Instalace integrace služby Azure Advanced Threat Protection VPN | Dokumentace Microsoftu
description: Shromážděte informace o monitorování účtů pro služby Azure ATP integrace sítě VPN.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/11/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9f5caf3ef7c0c986404cfe90a6f8cc40aa9462b4
ms.sourcegitcommit: 30d874808cfeafd46ee8fbbf34e0bbcb337f6544
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/11/2018
ms.locfileid: "49089368"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="integrate-vpn"></a>Integrace sítě VPN

Azure Advanced Threat Protection (ATP) z řešení sítě VPN můžete shromažďovat informace o monitorování účtů. Při konfiguraci, uživatelského profilu obsahovat informace z připojení VPN, jako je například IP adresy a umístění, původu připojení. To doplňuje procesu šetření tím, že poskytuje další informace na aktivity uživatelů, jakož i nové zjišťování pro nestandardní připojení k síti VPN. Volání překládat externí IP adresu na umístění je anonymní. Žádné osobní identifikátor se posílá ve toto volání.

Ochrana ATP v programu Azure integruje řešení sítě VPN prostřednictvím naslouchání událostech monitorování účtů protokolu RADIUS předávaných do senzorů ochrany ATP v programu Azure. Tento mechanismus je založen na standardní monitorování účtů protokolu RADIUS ([RFC 2866](https://tools.ietf.org/html/rfc2866)), a podporují těchto dodavatelů VPN:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Požadavky

Povolení integrace sítě VPN, ujistěte se, že můžete nastavit následující parametry:

-   Otevřete port UDP 1813 na vaší ochrany ATP v programu Azure senzorů a/nebo senzorů samostatné ochrany ATP v programu Azure.


Následující příklad používá Microsoft Routing a Server pro vzdálený přístup (RRAS) k popisu proces konfigurace sítě VPN.

Pokud používáte řešení VPN jiných výrobců, si projděte jejich dokumentaci pokyny o tom, jak povolit monitorování účtů protokolu RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Nakonfigurujte monitorování účtů protokolu RADIUS sítě VPN systému

Proveďte následující kroky na serveru RRAS.
 
1.  Otevřete konzolu pro směrování a vzdálený přístup.
2.  Klikněte pravým tlačítkem na název serveru a klikněte na tlačítko **vlastnosti**.
3.  V **zabezpečení** ve skupině **zprostředkovatel účtování**vyberte **monitorování účtů protokolu RADIUS** a klikněte na tlačítko **konfigurovat**.

    ![Nastavení protokolu RADIUS](./media/radius-setup.png)

4.  V **přidat Server protokolu RADIUS** okno, zadejte **název serveru** nejbližší samostatný senzor ochrany ATP v programu Azure nebo senzoru služby Azure ATP. V části **Port**, ujistěte se, že je nakonfigurovaný výchozí 1813. Klikněte na tlačítko **změnu** a zadejte nový sdílený tajný řetězec alfanumerických znaků, které si zapamatujete. Je potřeba vyplnit později v konfiguraci ochrany ATP v programu Azure. Zkontrolujte **zprávy odesílat účtu RADIUS On a vypnutém** pole a potom klikněte na tlačítko **OK** na všechna otevřená dialogová okna.
 
     ![Nastavení sítě VPN](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-atp"></a>Konfigurace sítě VPN v ochrany ATP v programu

Ochrana ATP v programu Azure shromažďuje data sítě VPN, která pomáhá profilu umístění, ze které počítače připojit k síti a aby byla schopna odhalit podezřelé připojení k síti VPN.

Data sítě VPN nakonfigurujete v ochrany ATP v programu:

1.  Na portálu ochrany ATP v programu Azure, klikněte na ikonu konfigurace a pak **VPN**.
 

2.  Zapnout **monitorování účtů protokolu Radius**a zadejte **sdílený tajný klíč** jste dříve nakonfigurovali na serveru RRAS VPN. Potom klikněte na **Uložit**.
 

  ![Konfigurovat síť VPN Azure ATP](./media/atp-vpn-radius.png)


Jakmile je tato možnost povolena, všechny služby Azure ATP senzory a samostatné senzorů naslouchání na portu 1813 události monitorování účtů protokolu RADIUS a vaší instalace byla dokončena. 

 Poté, co senzoru služby Azure ATP přijímá události VPN a odesílá je ke cloudové službě ochrana ATP v programu Azure pro zpracování, profil entity označí odlišné navštívená umístění VPN a aktivity v profilu označí umístění.



## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
