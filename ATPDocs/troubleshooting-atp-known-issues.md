---
title: Řešení potíží s Azure ATP známé problémy | Microsoft Docs
description: Popisuje, jak můžete potíže v Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/10/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 23386e36-2756-4291-923f-fa8607b5518a
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2112e9fea1f316ff12d87b3a477b78bff4457a5f
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/16/2018
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="troubleshooting-azure-atp-known-issues"></a>Řešení potíží s Azure ATP – známé problémy 


## <a name="deployment-log-location"></a>Umístění protokolu nasazení
 
Protokoly nasazení Azure ATP jsou umístěné v adresáři temp uživatele, který příslušný produkt nainstaloval. Ve výchozím umístění instalace, se nachází v: C:\Users\Administrator\AppData\Local\Temp (nebo v adresáři % temp %).

## <a name="azure-atp-sensor-nic-teaming-issue"></a>Azure ATP senzor seskupování problém síťový adaptér

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