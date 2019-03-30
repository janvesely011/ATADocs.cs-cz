---
title: Řešení potíží – známé problémy ochrany ATP v Azure | Dokumentace Microsoftu
description: Popisuje, jak můžete řešit problémy v ochrany ATP v programu Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 10/04/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: dd654182fff5ed60fe02da56572e79dac13ff761
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674890"
---
# <a name="troubleshooting-azure-atp-known-issues"></a>Řešení potíží s Azure – ochrana ATP v programu známé problémy 


## <a name="deployment-log-location"></a>Umístění protokolu nasazení
 
Protokoly nasazení služby Azure ATP jsou umístěné v adresáři temp uživatele, který příslušný produkt nainstaloval. Ve výchozím umístění instalace můžete najít na: C:\Users\Administrator\AppData\Local\Temp (nebo v jednom adresáři % temp %). Další informace najdete v tématu [analytických řešení potíží pomocí protokolů](troubleshooting-atp-using-logs.md)

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Problém s ověřováním proxy prezentuje jako chybu licencování

Pokud během instalace senzoru se zobrazí následující chyba:  **Zaregistrovat kvůli problémům s licencováním se senzor nepovedlo.**

Položky protokolu nasazení: [1C 60: 1AA8] [2018-03-24T23:59:13] i000: 2018-03-25 02:59:13.1237 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Debug SensorBootstrapperApplication Engine.Quit [\[]deploymentResultStatus=1602 isRestartRequired=False[\]] [1C60:15B8][2018-03-25T00:27:56]i500: Vypíná, ukončovací kód: 0x642


**Příčina:**

V některých případech se při komunikaci přes proxy server během ověřování může odpovídat na senzoru služby Azure ATP s chybou 401 nebo 403 místo chyby 407. Senzoru služby Azure ATP interpretovaly chyba 401 nebo 403 jako licencování problém a ne jako problém ověřování proxy serveru. 

**Řešení:**

Ujistěte se, že senzor můžete přejít na *. atp.azure.com pomocí nakonfigurovaného proxy serveru bez ověřování. Další informace najdete v tématu [konfigurace proxy serveru k umožnění komunikace](configure-proxy.md).




## Azure ochrany ATP v programu senzor seskupování problém síťové karty <a name="nic-teaming"></a>

Pokud se pokusíte nainstalovat senzor ochrany ATP v programu na počítači nakonfigurované s adaptérem seskupování síťových adaptérů, obdržíte chybu instalace. Pokud chcete nainstalovat na počítač nakonfigurovaný pomocí seskupování síťových adaptérů senzor ochrany ATP v programu, postupujte podle těchto pokynů:

Pokud jste ještě nenainstalovali senzor:

1.  Stáhněte si Npcap z [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
2.  WinPcap, odinstalujte, pokud byla nainstalována.
3.  Instalace Npcap pomocí následujících možností: loopback_support = č & winpcap_mode = Ano
4.  Instalace balíčku senzoru.

Pokud jste již nainstalovali senzor:

1.  Stáhněte si Npcap z [ https://nmap.org/npcap/ ](https://nmap.org/npcap/).
2.  Odinstalujte senzoru.
3.  WinPcap, odinstalujte.
4.  Instalace Npcap pomocí následujících možností: loopback_support = č & winpcap_mode = Ano
5.  Přeinstalujte balíčku senzoru.

## <a name="windows-defender-atp-integration-issue"></a>Problémy s integrací ochrany ATP v programu Windows Defender

Azure Advanced Threat Protection umožňuje integrovat Azure ATP s ochrany ATP v programu Windows Defender. Zobrazit [integrace služby Azure ATP s ochrany ATP v programu Windows Defender](integrate-wd-atp.md) Další informace. 

## <a name="vmware-virtual-machine-sensor-issue"></a>Problém senzor virtuálního počítače VMware

Pokud máte senzoru služby Azure ATP na virtuálních počítačích VMware, můžou se zobrazit monitorovací upozornění **některý síťový provoz se neanalyzuje**. K tomu dochází kvůli neshodě v konfiguraci ve VMware.

Řešení tohoto problému:

Nastavte následující nastavení na **0** nebo **zakázané** v konfiguraci síťové karty virtuálního počítače: TsoEnable, LargeSendOffload, TSO Offload, Giant TSO Offload.
> [!NOTE]
> Pro služby Azure ATP senzory, potřebujete jenom zakázat **IPv4, TSO Offload** v části konfigurace síťové karty.

 ![Problém senzor VMware](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
