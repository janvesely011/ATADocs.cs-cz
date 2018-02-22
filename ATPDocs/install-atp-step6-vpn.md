---
title: "Instalace Azure Advanced Threat Protection – krok 6 | Microsoft Docs"
description: "V tomto kroku instalace ATP integrovat vaši síť VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/14/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d29210983f3f9f879b462ef760d0b3fe6e53cd5d
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-6"></a>Nainstalovat Azure ATP – krok 6

>[!div class="step-by-step"]
[« Krok 5](install-atp-step5.md)
[Krok 7 »](install-atp-step7.md)

## <a name="step-6-integrate-vpn"></a>Krok 6: Integrovat sítě VPN

Azure Advanced Threat Protection (ATP) může shromažďovat informace o monitorování účtů z řešení sítě VPN. Při konfiguraci, stránka profil uživatele obsahuje informace z připojení k síti VPN, jako je například IP adresy a umístění, kde připojení vytvořena. To doplňuje procesu šetření tím, že poskytuje další informace na aktivity uživatelů, jakož i nové detekce neobvyklé připojení k síti VPN. Volání přeložit externí IP adresu na umístění jsou anonymní. Žádné osobní identifikátor se odešlou v toto volání.

Azure ATP se integruje s řešení sítě VPN prostřednictvím naslouchání události monitorování účtů protokolu RADIUS předávány snímače Azure ATP. Tento mechanismus je založen na standardní monitorování účtů protokolu RADIUS ([RFC 2866](https://tools.ietf.org/html/rfc2866)), a jsou podporovány následující dodavatelů VPN:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Požadavky

Chcete-li povolit integraci VPN, nezapomeňte nastavit následující parametry:

-   Otevřete port UDP 1813 na Azure ATP samostatné senzory a senzor Azure ATP.


Následující příklad používá Microsoft Routing a vzdálený přístup (RRAS) do popisují proces konfigurace sítě VPN.

Pokud používáte řešení VPN jiných výrobců, si projděte jejich dokumentaci pokyny o tom, jak povolit monitorování účtů protokolu RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Nakonfigurujte monitorování účtů protokolu RADIUS na serveru sítě VPN

Proveďte následující kroky na serveru RRAS.
 
1.  Otevřete konzolu pro směrování a vzdálený přístup.
2.  Klikněte pravým tlačítkem na název serveru a klikněte na tlačítko **vlastnosti**.
3.  V **zabezpečení** v části **zprostředkovatele monitorování účtů**, vyberte **monitorování účtů protokolu RADIUS** a klikněte na tlačítko **konfigurace**.

    ![Instalační program protokolu RADIUS](./media/radius-setup.png)

4.  V **přidat Server RADIUS** okno, zadejte **název serveru** nejbližší senzor samostatné Azure ATP nebo Azure ATP senzoru. V části **Port**, zkontrolujte, že je nakonfigurované výchozí 1813. Klikněte na tlačítko **změnu** a zadejte nový sdílený tajný řetězec alfanumerické znaky, které si pamatujete. Je třeba vyplnit později ve vaší konfiguraci ATP Azure. Zkontrolujte **zprávy odesílat účet protokolu RADIUS na a monitorování účtů Off** pole a pak klikněte na **OK** na všechna otevřená dialogová okna.
 
     ![Nastavení virtuální privátní sítě](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-atp"></a>Konfigurace sítě VPN v ATP

Azure ATP shromažďuje data sítě VPN, která pomáhá profil umístění, ze které počítače připojit k síti a jako dokáže detekovat nestandardní připojení k síti VPN.

Konfigurace sítě VPN data v ATP:

1.  Na portálu Azure ATP pracovního prostoru klikněte na ikonu konfigurace a potom **VPN**.
 

2.  Zapnout **monitorování účtů protokolu Radius**a zadejte **sdílený tajný klíč** jste nakonfigurovali dříve na serveru RRAS VPN. Potom klikněte na **Uložit**.
 

  ![Konfigurovat síť VPN Azure ATP](./media/atp-vpn-radius.png)


Po je tato možnost povolena, všechny Azure ATP samostatné senzory a snímače naslouchání na portu 1813 pro události monitorování účtů protokolu RADIUS. 

Vaše instalace je dokončena. 

Po senzoru Azure ATP přijímá VPN události a odesílá je ke cloudové službě Azure ATP pro zpracování, profil entity označí odlišné používaná umístění sítě VPN a aktivity v profilu označí umístění.





>[!div class="step-by-step"]
[«Krok 6](install-atp-step5.md)
[krok 7»](install-atp-step7.md)


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
