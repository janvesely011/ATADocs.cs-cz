---
title: Stav posouzení zabezpečení identity pro starší verze Azure Advanced Threat Protection | Microsoft Docs
description: Tento článek poskytuje přehled sestavy vyhodnocení starší verze protokolu zabezpečení pro identifikaci protokolu služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 6597b8c7-f83e-43c6-8149-fb4a914a845b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a4beca7b0c8e990bcb64c44716888eda6a76640e
ms.sourcegitcommit: 09275d3400534200fa6ea572e89e440b3cc58360
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/10/2019
ms.locfileid: "67788851"
---
# <a name="security-assessment-prevent-legacy-protocol-implementation"></a>Posouzení zabezpečení: Zabránit implementaci staršího protokolu
 
## <a name="what-are-legacy-protocols"></a>Co jsou starší protokoly?

Díky všem standardním pracovním společnostem, které provádějí ochranu své infrastruktury pomocí opravy a posílení zabezpečení serveru, je jedna oblast, která často přechází, je vyřazení staršího protokolu. Bez omezení vystavení staršího protokolu je krádež přihlašovacích údajů poměrně snadné dosáhnout. 

Většina starších protokolů se vytvořila v konceptu a vytvořila ještě předtím, než byly dnešní požadavky na zabezpečení a vytvořené před tím, než byly jasné požadavky na moderní podnikové zabezpečení. Starší protokoly ale zůstanou nezměněné a dají se snadno transformovat na zranitelné přístupové body v každé moderní organizaci. 

## <a name="what-risks-do-retained-legacy-protocols-introduce"></a>Jaká rizika zachovají starší protokoly? 

Moderní počítačové útoky často využívají starší verze protokolů při jejich útoku a často je využívají k zacílení na organizace, které ještě mají k implementaci řádného zmírnění. 

Omezení možností útoku můžete dosáhnout vypnutím podpory pro nezabezpečené starší verze protokolů, jako jsou: 

- TLS 1,0 & 1,1 (stejně jako všechny verze SSL)
- Server Message Block V1 (SMBv1)
- LanMan (LM) / NTLMv1
- Ověřování hodnotou hash

Aby bylo možné vyřadit starší protokoly, musí vaše organizace nejdřív zjistit, které interní entity a aplikace je využívají. Tabulka sestavy posouzení **použití starších protokolů** vystaví nejvyšší zjištěné entity pomocí starších protokolů (pro teď ověřovací NTLMv1). Pomocí této sestavy můžete okamžitě zkontrolovat všechny nejdůležitější entity, které by mohly být ovlivněny, a provádět na nich akce, zastavovat používání těchto protokolů a nakonec je zcela zakázat. Další informace o rizicích při používání starších protokolů najdete v tématu [ukončení používání LAN Manageru a ověřovací NTLMv1!](https://blogs.technet.microsoft.com/miriamxyra/2017/11/07/stop-using-lan-manager-and-ntlmv1/).


## <a name="how-do-i-use-this-security-assessment"></a>Návody použít toto posouzení zabezpečení? 
1. Pomocí tabulky sestav zjistíte, které ze shora zjištěných entit používá starší protokoly.  
    <br>![Zabránit použití starších protokolů](media/atp-mcas-ispm-legacy-protocols-2.png)
1. Proveďte příslušné akce s těmito entitami, abyste zjistili závislosti, zastavili použití staršího protokolu a nakonec zakázali [protokoly zcela](https://blogs.technet.microsoft.com/miriamxyra/2017/11/07/stop-using-lan-manager-and-ntlmv1/). 

## <a name="next-steps"></a>Další postup
- [Filtrování aktivit v Azure ATP v Cloud App Security](atp-activities-filtering-mcas.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
