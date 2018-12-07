---
title: Referenční informace o události ID ATA | Dokumentace Microsoftu
description: Poskytuje seznam události ID ATA a jejich popisy.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 353395f782d29bb18e95c02ad56407a592d8c20b
ms.sourcegitcommit: 2b15356612eb720f83235ff8cb08e4a6435206ea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/07/2018
ms.locfileid: "53022420"
---
*Platí pro: Advanced Threat Analytics verze 1.9*


# <a name="ata-event-id-reference"></a>ATA referenční informace o ID události

V prohlížeči událostí komponenty ATA Center protokoluje události pro ATA. Tento článek obsahuje seznam ID událostí a popis jednotlivých.

Události najdete tady:

![umístění ID události](./media/event-id-location.png)

## <a name="ata-health-events"></a>Události stavu ATA

1001 – jednotky databázových dat ATA Center upozornění na stav volného místa 

1003 – upozornění na přetížení stav ATA Center 

1004 – upozornění na stav vypršení platnosti certifikátu 

1005 – upozornění na stav odpojení databáze System center 

1006 – ATA Gateway adresář služby klienta účtu heslo vypršení platnosti upozornění na stav 

1007 – upozornění na stav nepřiřazený synchronizátor domény ATA Gateway 

1008 – ATA Gateway Zachytávání síťových adaptéru chybovém stavu výstrahy 

1009 – ATA Gateway zaznamenat upozornění na chybějící stav sítě adaptéru 

1010 – ATA Gateway adresář služby klienta připojení stavu výstrahy 

1011 – upozornění na stav odpojení ATA Gateway 

1012 – upozornění na stav aktivity události přetížené ATA Gateway 

1013 – ATA Gateway přetížené síti upozornění na stav aktivity 

1014 – upozornění na stav e-mailu System center 

1015 – upozornění na stav Syslog System center 

1016 – upozornění na zastaralý stav komponenty ATA Gateway 

1017 – System center není příjem upozornění na stav provozu 

1018 – upozornění na stav selhání spuštění ATA Gateway 

1019 – upozornění na stav nedostatku paměti ATA Gateway 

1020 – upozornění na stav naslouchací proces události ATA Gateway RADIUS 

1021 – upozornění na stav naslouchací proces události ATA Gateway Syslog 

1022 – ATA Center externích IP adres řešení selhání upozornění na stav 
 
## <a name="ata-suspicious-activity-events"></a>Události podezřelých aktivit ATA

2001 – podezřelá aktivita neobvyklé chování 

2002 – podezřelá aktivita neobvyklý protokol 

2003 – podezřelá aktivita výčtu účtů 

2004 – LDAP hrubou vynutit podezřelé aktivity 

2006 – adresářových služeb replikace podezřelé aktivity 

2007 – podezřelé aktivity rekognoskace DNS 

2008 – podezřelá aktivita snížení úrovně šifrování (žádné podtyp)

2009 – aktivita snížení úrovně šifrování podezřelé (podezřelý GoldenTicket)
       
2010 – aktivita snížení úrovně šifrování podezřelé (podezřelý Overpass-The-Hash)

2011 – aktivita snížení úrovně šifrování podezřelé (podezřelý Skeleton Key)

2012 – výčet relací podezřelé aktivity 

2013 – falešný certifikát PAC podezřelé aktivity 

2014 – podezřelá aktivita Honeytokenu aktivita 

2016 – podezřelá aktivita odstranění objekt 

2017 – předání hodnoty hash podezřelé aktivity 

2018 – předání lístku podezřelé aktivity 

2019 – vzdálené spuštění podezřelých aktivit 

2020 – načíst data protection zálohování klíče podezřelé aktivity 

2021 – podezřelé aktivity rekognoskace SAMR 

2022 – podezřelá aktivita zlatý lístek 

2023 – útok hrubou silou podezřelé aktivity 

2024 – neobvyklé členství změnit na podezřelé aktivity senstitive skupiny 

2025 – neobvyklé podezřelou aktivitu sítě VPN

2026 – škodlivé služby vytvoření podezřelé aktivity

## <a name="ata-auditing-events"></a>Události auditu ATA

3001 – změna konfigurace ATA 

3002 – přidání ATA Gateway

3003 – odstranit ATA Gateway

3004 - aktivovat licenci ATA

3005 – Přihlaste se ke konzole ATA

3006 – ručně prováděné změny stavu aktivity 

3007 – ruční změna stavu podezřelé aktivity 


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
