---
title: Zpráva o hodnocení zabezpečení Azure Advanced Threat Protection stav | Microsoft Docs
description: Tento článek poskytuje přehled sestavy hodnocení zabezpečení stav (slabé šifrování identity) pro Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: cc82212b-7d25-4ec7-828d-2475ff40d685
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a7f62d8244205d191c10a01f62d3830714d02bbd
ms.sourcegitcommit: cf7580163701ded9e821969ed5c103d547fe0118
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/11/2019
ms.locfileid: "67810664"
---
# <a name="security-assessment-weak-cipher-usage"></a>Posouzení zabezpečení: Slabé použití šifry 


## <a name="what-are-weak-ciphers"></a>Co jsou slabé šifry? 

Kryptografie spoléhá na šifry k šifrování našich dat. Například RC4 (Rivest cipher 4 také označované jako ARC4 nebo ARCFOUR, což znamená údajné RC4) je jeden.   I když je RC4 jedinečnou nezapomenutelnou pro jednoduchost a rychlost, zjistilo se od původní verze ŠIFRy několik chyb zabezpečení, takže je vygenerování nezabezpečené. Šifra RC4 je obzvláště zranitelná, když se neodstraní začátek datového proudu výstupního klíče, nebo když se použijí nenáhodné nebo související klíče. 

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Návody pomocí tohoto posouzení zabezpečení zlepšit stav podnikového zabezpečení? 

1. Přečtěte si hodnocení zabezpečení pro slabé použití šifry. 
    ![Kontrola slabého použití šifry při vyhodnocování](media/atp-cas-isp-weak-cipher-2.png)
1. Prozkoumat, proč budou identifikování klienti a servery používat slabé šifry.   
1. Opravte problémy a zakažte použití RC4 nebo dalších slabých šifr (například DES/3DES). 
1. Další informace o deaktivaci ŠIFRy najdete v článku [informační zpravodaj zabezpečení společnosti Microsoft](https://support.microsoft.com/help/2868725/microsoft-security-advisory-update-for-disabling-rc4). 

## <a name="remediation"></a>Náprava

Nastavením následujících klíčů registru Zakažte klientům a serverům, které chcete zastavit, používání šifrovacích sad RC4. Po zakázání může kterýkoli server nebo klient, který komunikuje s jiným klientem nebo serverem, který vyžaduje použití RC4, zabránit tomu, aby se připojení objevilo. Klienti, na kterých je toto nastavení nasazené, se nebudou moci připojit k lokalitám, které vyžadují RC4, a servery, které toto nastavení nasadí, nebudou moci obsluhovat klienty, kteří vyžadují použití šifry RC4.

> [!NOTE]
>Před tím, než je povolíte v produkčním prostředí, se ujistěte, že v kontrolovaném prostředí otestujete následující nastavení. 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128]   "Enabled"=dword:00000000 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128]   "Enabled" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128]   "Enabled" = DWORD: 00000000

Další informace o stahování a aktualizaci úprav registru najdete v [informačním zpravodaji zabezpečení společnosti Microsoft](https://docs.microsoft.com/security-updates/SecurityAdvisories/2013/2868725).


## <a name="next-steps"></a>Další postup
- [Filtrování aktivit v Azure ATP v Cloud App Security](atp-activities-filtering-mcas.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
