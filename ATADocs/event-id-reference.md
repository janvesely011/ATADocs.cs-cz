---
title: "Odkaz na ID událostí ATA | Microsoft Docs"
description: "Obsahuje seznam událostí ATA ID a jejich popisy."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 3ef6322a4c63c15bbdae0669a7d116dfd80756db
ms.sourcegitcommit: e2cb3af9c1dbb0b75946dc70cc439b19d654541c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/06/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*


# <a name="ata-event-id-reference"></a>Odkaz na ID událostí ATA

V prohlížeči událostí ATA Center protokoluje události pro ATA. Tento článek obsahuje seznam ID událostí a jejich popis.

Události naleznete zde:

![umístění ID událostí](./media/event-id-location.png)

## <a name="ata-health-events"></a>Události stavu ATA

1001 – ATA Center databázových dat jednotka výstraha stavu volného místa 

1003 – výstraha stavu přetížené ATA Center 

1004 – výstraha stavu vypršení platnosti certifikátu 

1005 – výstraha odpojeném stavu databáze center 

1006 – ATA Gateway directory services klienta účtu heslo vypršení platnosti stavu výstrahy 

1007 – výstraha stavu není přiřazen synchronizátor domény ATA Gateway 

1008 – ATA Gateway zachycení síťový adaptér chybný stav výstrahy 

1009 – síťový adaptér chybějící výstraha stavu zaznamenání ATA Gateway 

1010 – ATA Gateway directory services klienta připojení stavu výstrahy 

1011 – výstraha odpojeném stavu ATA Gateway 

1012 – výstraha stavu aktivity událostí přetížený ATA Gateway 

1013 – výstraha stavu aktivity síť přetížená ATA Gateway 

1014 – výstraha stavu center e-mailu 

1015 – výstraha stavu center Syslog 

1016 – výstraha komponenty ATA Gateway zastaralé stavu 

1017 – center nepřijaté provoz stavu výstrahy 

1018 – výstraha při selhání stavu spuštění ATA Gateway 

1019 – výstraha stavu nedostatku paměti ATA Gateway 

1020 – výstraha stavu naslouchací proces protokolu RADIUS ATA Gateway událostí 

1021 – výstraha stavu naslouchací proces ATA Gateway Syslog událostí 

1022 – ATA Center externí IP adresu řešení stavu výstraha při selhání 
 
## <a name="ata-suspicious-activity-events"></a>Události podezřelé aktivity ATA

2001 – podezřelé aktivity neobvyklé chování 

2002 – neobvyklé protokol podezřelé aktivity 

2003 – podezřelé aktivity účtu výčet 

2004 – LDAP hrubou vynutit podezřelé aktivity 

2005 – předběžné ověření počítače se nezdařilo podezřelé aktivity 

2006 – directory services replikace podezřelé aktivity 

2007 – DNS rekognoskace podezřelé aktivity 

2008 – podezřelé aktivity přechod na starší verzi šifrování 

2012 – výčet relací podezřelé aktivity 

2013 – forged PAC podezřelé aktivity 

2014 – Honeytokenu aktivity podezřelé aktivity 

2015 – LDAP vymažte text heslo podezřelé aktivity 

2016 – masivní objekt odstranění podezřelé aktivity 

2017 – předat hodnotu hash podezřelé aktivity 

2018 – předat lístku podezřelé aktivity 

2019 – vzdálené spuštění podezřelé aktivity 

2020 – načtení dat ochrany zálohování klíče podezřelé aktivity 

2021 – SAMR rekognoskace podezřelé aktivity 

2022 – zlatý lístek podezřelé aktivity 

2023 – hrubou silou podezřelé aktivity 

2024 - neobvyklé citlivou skupinu členství změnu podezřelé aktivity  

## <a name="ata-auditing-events"></a>Auditování událostí ATA

3001 – změňte konfiguraci ATA 

3002 – ATA Gateway přidán

3003 – ATA Gateway odstranit

3004 - aktivovat licence ATA

3005 – přihlášení do konzoly ATA

3006 – ruční změna stavu aktivity 

3007 – ruční změna stavu podezřelé aktivity 


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
