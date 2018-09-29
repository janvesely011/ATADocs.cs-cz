---
title: Instalace Azure Advanced Threat Protection – krok 6 | Dokumentace Microsoftu
description: V tomto kroku instalace ochrany ATP v programu můžete integrovat vaši síť VPN.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9ce1bbbda96cc8a10b026f2f422ac79b1b2bae55
ms.sourcegitcommit: b283bf66e63d76e6dba4564a229e804792794c6d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/29/2018
ms.locfileid: "47454101"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="install-azure-atp---step-6"></a>Instalace služby Azure ATP – krok 6

> [!div class="step-by-step"]
> [« Krok 5](install-atp-step5.md)
> [Krok 7 »](install-atp-step7.md)

## <a name="step-6-integrate-vpn"></a>Krok 6: Integrace sítě VPN

Azure Advanced Threat Protection (ATP) z řešení sítě VPN můžete shromažďovat informace o monitorování účtů. Při konfiguraci, uživatelského profilu obsahovat informace z připojení VPN, jako je například IP adresy a umístění, původu připojení. To doplňuje procesu šetření tím, že poskytuje další informace na aktivity uživatelů, jakož i nové zjišťování pro nestandardní připojení k síti VPN. Volání překládat externí IP adresu na umístění je anonymní. Žádné osobní identifikátor se posílá ve toto volání.

Ochrana ATP v programu Azure integruje řešení sítě VPN prostřednictvím naslouchání událostech monitorování účtů protokolu RADIUS předávaných do senzorů ochrany ATP v programu Azure. Tento mechanismus je založen na standardní monitorování účtů protokolu RADIUS ([RFC 2866](https://tools.ietf.org/html/rfc2866)), a podporují těchto dodavatelů VPN:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Požadavky

Povolení integrace sítě VPN, ujistěte se, že můžete nastavit následující parametry:

-   Otevřete port UDP 1813 ochrany ATP v programu Azure samostatné senzory a senzoru služby Azure ATP.


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

1.  Na portálu ochrany ATP v programu Azure pracovní prostor, klikněte na ikonu konfigurace a pak **VPN**.
 

2.  Zapnout **monitorování účtů protokolu Radius**a zadejte **sdílený tajný klíč** jste dříve nakonfigurovali na serveru RRAS VPN. Potom klikněte na **Uložit**.
 

  ![Konfigurovat síť VPN Azure ATP](./media/atp-vpn-radius.png)


Poté, co je tato možnost povolena, všechny služby Azure ATP samostatné senzory a senzory naslouchání na portu 1813 pro události monitorování účtů protokolu RADIUS. 

Vaše instalace byla dokončena. 

Poté, co senzoru služby Azure ATP přijímá události VPN a odesílá je ke cloudové službě ochrana ATP v programu Azure pro zpracování, profil entity označí odlišné navštívená umístění VPN a aktivity v profilu označí umístění.





> [!div class="step-by-step"]
> [«Krok 6](install-atp-step5.md)
> [krok 7»](install-atp-step7.md)


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
