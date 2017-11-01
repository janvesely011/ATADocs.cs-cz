---
title: "Instalace Advanced Threat Analytics – krok 7 | Dokumentace Microsoftu"
description: "V tomto kroku instalace ATA můžete integrovat vaši síť VPN."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/31/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 748121a709ac05756edf34e04e13b996190e9711
ms.sourcegitcommit: b951c64228d4f165ee1fcc5acc0ad6bb8482d6a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/31/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*



# <a name="install-ata---step-7"></a>Instalace ATA – krok 7

>[!div class="step-by-step"]
[«Krok 5](install-ata-step5.md)
[krok 8»](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Krok 7: Integrovat sítě VPN

Microsoft Advanced Threat Analytics (ATA) verze 1.8 může shromažďovat informace o monitorování účtů z řešení sítě VPN. Při konfiguraci, stránky profil uživatele bude obsahovat informace z připojení k síti VPN, jako je například IP adresy a umístění, kde připojení vytvořena. Doplní procesu šetření to budou poskytování dalších informací o činnosti uživatelů. Volání přeložit externí IP adresu na umístění jsou anonymní. Žádné osobní identifikátor se odešlou v toto volání.

ATA se integruje s řešení sítě VPN prostřednictvím naslouchání událostech monitorování účtů protokolu RADIUS předávaných do ATA Gateway. Tento mechanismus je založen na standardní monitorování účtů protokolu RADIUS ([RFC 2866](https://tools.ietf.org/html/rfc2866)), a jsou podporovány následující dodavatelů VPN:

-   Microsoft
-   F5
-   Check Point
-   Cisco ASA

## <a name="prerequisites"></a>Požadavky

Povolit síť VPN, integrace Přesvědčte se, že nastavíte následující:

-   Otevřete port UDP 1813 na ATA Gateway a ATA Lightweight Gateway.

-   ATA Center připojení k Internetu, tak, aby se můžete dotazovat umístění příchozí IP adresy.

V následujícím příkladu používáme Microsoft Routing a vzdálený přístup (RRAS) popisují proces konfigurace sítě VPN.

Pokud používáte 3. stran řešení sítě VPN, si projděte jejich dokumentaci pokyny o tom, jak povolit monitorování účtů protokolu RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Nakonfigurujte monitorování účtů protokolu RADIUS na serveru sítě VPN

Na serveru RRAS, proveďte následující kroky.
 
1.  Otevřete konzolu pro směrování a vzdálený přístup.
2.  Klikněte pravým tlačítkem na název serveru a klikněte na tlačítko **vlastnosti**.
3.  V **zabezpečení** v části **zprostředkovatele monitorování účtů**, vyberte **monitorování účtů protokolu RADIUS** a klikněte na tlačítko **konfigurace**.

    ![Instalační program protokolu RADIUS](./media/radius-setup.png)

4.  V **přidat Server RADIUS** okno, zadejte **název serveru** nejbližší ATA Gateway nebo ATA Lightweight Gateway. V části **Port**, zkontrolujte, že je nakonfigurované výchozí 1813. Klikněte na tlačítko **změnu** a zadejte nový sdílený tajný řetězec alfanumerické znaky, které si pamatujete. Musíte se k vyplnění později v konfiguraci ATA. Zkontrolujte **zprávy odesílat účet protokolu RADIUS na a monitorování účtů Off** pole a pak klikněte na **OK** na všechna otevřená dialogová okna.
 
     ![Nastavení virtuální privátní sítě](./media/vpn-set-accounting.png)
     
### <a name="configure-vpn-in-ata"></a>Konfigurace sítě VPN v ATA

ATA shromažďuje data sítě VPN, která pomáhá profil umístění, ze které počítače připojit k síti a jako dokáže detekovat nestandardní připojení k síti VPN.

Konfigurace sítě VPN data v ATA:

1.  V konzole ATA, otevřete stránku konfigurace ATA a přejděte na **VPN**.
 
  ![Nabídky konfigurace ATA](./media/config-menu.png)

2.  Zapnout **monitorování účtů protokolu Radius** a zadejte **sdílený tajný klíč** jste nakonfigurovali dříve na serveru RRAS VPN. Potom klikněte na **Uložit**.
 

  ![Konfigurovat síť VPN ATA](./media/vpn.png)


Jakmile je tato možnost povolena, všechny komponenty ATA Gateway a Lightweight Gateway naslouchat na portu 1813 pro události monitorování účtů protokolu RADIUS. 

Vaše instalace je dokončena a zobrazí aktivitu sítě VPN v stránky profil uživatele:
 
   ![Nastavení virtuální privátní sítě](./media/vpn-user.png)

Po ATA Gateway přijímá VPN události a odesílá je ATA Center pro zpracování, ATA Center vyžaduje připojení k Internetu pro protokol HTTPS port 443 pro umět překládat externí IP adresy v událostech VPN na jejich informace o zeměpisné poloze.





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

