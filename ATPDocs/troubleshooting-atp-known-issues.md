---
title: Řešení potíží s Azure ATP známé problémy | Microsoft Docs
description: Popisuje, jak můžete potíže v Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 15c857085fb7d003f783981a89fe02e920a8e49a
ms.sourcegitcommit: 3539dd3f9ab7729e5326b904fc64985c808bc8ce
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/21/2018
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="troubleshooting-azure-atp-known-issues"></a>Řešení potíží s Azure ATP – známé problémy 


## <a name="deployment-log-location"></a>Umístění protokolu nasazení
 
Protokoly nasazení Azure ATP jsou umístěné v adresáři temp uživatele, který příslušný produkt nainstaloval. Ve výchozím umístění instalace, se nachází v: C:\Users\Administrator\AppData\Local\Temp (nebo v adresáři % temp %).

## <a name="proxy-authentication-problem-presents-as-licensing-error"></a>Problém s ověřováním proxy uvede jako licencování chyba.

Během instalace senzor se zobrazí následující chyba: **senzoru se nepodařilo zaregistrovat v důsledku problémů při správě licencí.**

Položky protokolu nasazení: [1C 60: 1AA8] [2018-03-24T23:59:13] i000: vrátí informace o InteractiveDeploymentManager ValidateCreateSensorAsync 2018-03-25 02:59:13.1237 [\[] validateCreateSensorResult = LicenseInvalid [\]] [60 1 c : 1AA8] [2018-03-24T23:59:56] i000: vrátí informace o InteractiveDeploymentManager ValidateCreateSensorAsync 02:59:56.4856 2018-03-25 [\[] validateCreateSensorResult = LicenseInvalid [\]] [1 C 60: 1AA8] [2018-03-25T00:27:56] i000: 2018-03-25 03:27:56.7399 ladění SensorBootstrapperApplication Engine.Quit [\[] deploymentResultStatus = 1602 isRestartRequired = False [\]] [1 C 60: 15B8] [2018-03-25T00:27:56] i500: vypínání, ukončovací kód: 0x642


**Příčina:**

V některých případech při komunikaci prostřednictvím proxy serveru během ověřování může odpovídat na senzoru Azure ATP s chybou 401 nebo 403 místo chyby 407. Senzor Azure ATP bude interpretovat chyba 401 nebo 403 jako licencování problém a ne jako chybu ověřování proxy serveru. 

**Řešení:**

Ujistěte se, že můžete vyhledat senzoru *. atp.azure.com prostřednictvím konfigurovaný server proxy bez ověřování. Další informace najdete v tématu [konfigurace proxy tak, aby komunikace](configure-proxy.md).




## Azure ATP senzor seskupování problém síťový adaptér <a name="nic-teaming"></a>

Pokud se pokusíte nainstalovat senzoru ATP na počítači nakonfigurované s adaptérem seskupování síťových adaptérů, obdržíte chybu instalace. Pokud chcete nainstalovat senzoru ATP na počítači nakonfigurované seskupování síťových adaptérů, postupujte podle těchto pokynů:

Pokud jste senzoru neinstalovali ještě:

1.  Stáhněte si Npcap z [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
2.  Odinstalujte WinPcap, pokud byl nainstalovaný.
3.  Instalace Npcap pomocí následujících možností: loopback_support = ne & winpcap_mode = Ano
4.  Nainstalujte balíček senzoru.

Pokud jste již nainstalovali senzoru:

1.  Stáhněte si Npcap z [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
2.  Odinstalujte senzoru.
3.  Odinstalujte WinPcap.
4.  Instalace Npcap pomocí následujících možností: loopback_support = ne & winpcap_mode = Ano
5.  Přeinstalujte senzor balíčku.

## <a name="windows-defender-atp-integration-issue"></a>Problém integrace Windows Defender ATP

Azure Advanced Threat Protection umožňuje integraci se službou Windows Defender ATP Azure ATP. Integrace je aktuálně aktivní, pouze pokud jste zákazník s Windows Defender ATP privátní Preview verzi. 

## <a name="vmware-virtual-machine-sensor-issue"></a>Problém senzor virtuálního počítače VMware

Pokud máte Azure ATP senzor na virtuální počítače VMware, může se zobrazit upozornění monitorování **provoz v síti není analyzované**. K tomu dochází z důvodu neshody konfigurace v prostředí VMware.

K vyřešení problému:

Nastavte následující nastavení **0** nebo **zakázané** v konfiguraci virtuálního počítače síťový adaptér: TsoEnable, LargeSendOffload, TSO snižování zátěže, Obří TSO přesměrování.
> [!NOTE]
> Pro Azure ATP senzorů, potřebujete jenom zakázat **snižování zátěže TSO IPv4** v části Konfigurace síťových karet.

 ![Problém senzor VMware](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)