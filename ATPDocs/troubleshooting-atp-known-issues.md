---
title: Řešení známých problémů služby Azure ATP | Microsoft Docs
description: Popisuje, jak můžete řešit problémy v Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 10/04/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 639dc38eeb9f4944cdd011074463953a13a49966
ms.sourcegitcommit: e185d6cf13ef0c40206a5d1980e3953ef8834a48
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/12/2019
ms.locfileid: "65196619"
---
# <a name="troubleshooting-azure-atp-known-issues"></a>Řešení známých problémů Azure ATP 


## <a name="deployment-log-location"></a>Umístění protokolu nasazení
 
Protokoly nasazení ATP Azure jsou umístěné v dočasném adresáři uživatele, který produkt nainstaloval. Ve výchozím umístění instalace je možné ji najít na adrese: C:\Users\Administrator\AppData\Local\Temp (nebo jeden adresář nad% Temp%). Další informace najdete v tématu [řešení potíží s ATP pomocí protokolů](troubleshooting-atp-using-logs.md) .

## <a name="proxy-authentication-problem-presents-as-a-licensing-error"></a>Potíže s ověřováním proxy serveru představují chybu licencování

Při instalaci senzorů se zobrazí následující chyba:  **Nepovedlo se zaregistrovat senzor z důvodu problémů s licencováním.**

Položky protokolu nasazení: [1C60:1AA8] [2018-03-24T23:59:13] i000: 2018-03-25 02:59:13.1237 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-24T23:59:56]i000: 2018-03-25 02:59:56.4856 Info  InteractiveDeploymentManager ValidateCreateSensorAsync returned [\[]validateCreateSensorResult=LicenseInvalid[\]] [1C60:1AA8][2018-03-25T00:27:56]i000: 2018-03-25 03:27:56.7399 Debug SensorBootstrapperApplication Engine.Quit [\[]deploymentResultStatus=1602 isRestartRequired=False[\]] [1C60:15B8][2018-03-25T00:27:56]i500: Vypínání, ukončovací kód: 0x642


**Způsobit**

V některých případech při komunikaci prostřednictvím proxy serveru může během ověřování reagovat na senzor ATP Azure s chybou 401 nebo 403 namísto chyby 407. Senzor ATP Azure bude interpretovat chybu 401 nebo 403 jako problém s licencováním a ne jako problém s ověřováním proxy serveru. 

**Řešení:**

Zajistěte, aby senzor mohl procházet do *. atp.azure.com prostřednictvím nakonfigurovaného proxy serveru bez ověřování. Další informace najdete v tématu [konfigurace proxy serveru pro povolení komunikace](configure-proxy.md).




## Problém seskupování síťových adaptérů senzorů ATP Azure<a name="nic-teaming"></a>

Pokud se pokusíte nainstalovat senzor ATP na počítač nakonfigurovaný pomocí adaptéru pro seskupování síťových adaptérů, dojde k chybě instalace. Pokud chcete senzor ATP nainstalovat na počítač nakonfigurovaný se seskupováním síťových adaptérů, postupujte podle těchto pokynů:

Pokud jste ještě nenainstalovali senzor:

1.  Stáhněte si Npcap [https://nmap.org/npcap/](https://nmap.org/npcap/)z.
2.  Odinstalujte WinPcap, pokud byl nainstalován.
3.  Nainstalujte Npcap s následujícími možnostmi: loopback_support = No & winpcap_mode = Yes.
4.  Nainstalujte balíček senzoru.

Pokud jste už senzor nainstalovali:

1.  Stáhněte si Npcap [https://nmap.org/npcap/](https://nmap.org/npcap/)z.
2.  Odinstalujte senzor.
3.  Odinstalujte WinPcap.
4.  Nainstalujte Npcap s následujícími možnostmi: loopback_support = No & winpcap_mode = Yes.
5.  Přeinstalujte balíček senzorů.

## <a name="windows-defender-atp-integration-issue"></a>Problém s integrací ochrany ATP v programu Windows Defender

Rozšířená ochrana před internetovými útoky v Azure umožňuje integrovat Azure ATP s ochranou ATP v programu Windows Defender. Další informace najdete v tématu [integrace služby Azure ATP s ochranou ATP v programu Windows Defender](integrate-wd-atp.md) . 

## <a name="vmware-virtual-machine-sensor-issue"></a>Problém senzoru virtuálních počítačů VMware

Pokud máte senzor ATP Azure na virtuálních počítačích VMware, může se zobrazit výstraha monitorování. **některé síťové přenosy se**neanalyzují. K tomu dochází z důvodu neshody konfigurace ve VMware.

Problém vyřešíte takto:

Nastavte následující nastavení na **hodnotu 0** nebo **zakázáno** v konfiguraci síťových adaptérů virtuálního počítače: TsoEnable, LargeSendOffload, TSO Offload, Obří TSO snižování zátěže.
> [!NOTE]
> V případě senzorů Azure ATP stačí v konfiguraci síťových adaptérů vypnout **snižování zátěže protokolu IPv4 TSO** .

 ![Problém se senzorem VMware](./media/vm-sensor-issue.png)

## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
