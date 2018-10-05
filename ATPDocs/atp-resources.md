---
title: Seznam užitečné zdroje informací pro rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Tento článek obsahuje seznam užitečné zdroje informací pro služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 029077455f9b2800984065a10c3e221e62d7c606
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783147"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="azure-atp-readiness-guide"></a>Příručka ke službě Azure ATP připravenosti

Tento článek vám poskytne plány připravenosti, který vám poskytne seznam prostředků, které vám Začínáme se službou Azure Advanced Threat Protection. 

## <a name="understanding-azure-atp"></a>Principy Azure ATP

Azure Protection pokročilé před internetovými útoky (ATP) je Cloudová služba, která pomáhá identifikovat a chránit váš podnik před různými typy pokročilých cílených kybernetických útoků a ohrožením zevnitř. Další informace o ochrany ATP v programu Azure: 
- [Přehled služby Azure ATP](what-is-atp.md)
- [Ochrana ATP v programu úvodní video Azure (25 minut) – úplná](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [Podrobné informace o videu Azure ochrany ATP v programu (75 minut) – úplná](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>Rozhodnutí o nasazení

Ochrana ATP v programu Azure se skládá z cloudové služby, které se nacházejí v Azure a integrované senzory, které lze nainstalovat na řadič domény nebo samostatné senzorů na vyhrazené servery. Předtím, než je zprovoznění služby Azure ATP, je důležité, abyste zvolili typ snímače, nejlépe vyhovovalo vašim nasazení a potřebám. Azure ochrany ATP v programu integrované senzorů (senzorů služby Azure ATP) poskytují zvýšené zabezpečení, snížení provozních nákladů a nasazení než samostatné senzorů ochrany ATP v programu Azure. Azure senzorů samostatné ochrany ATP v programu vyžaduje fyzický hardware, additionl konfigurační kroky a zpracují náročnější provozní náklady. <br>Pokud používáte fyzické servery, plánování kapacity je velmi důležité. Nápovědu získáte z nástroje pro změnu velikosti k přidělení místa pro vaše senzory: 
- [Azure nástroje pro změnu velikosti ochrany ATP v programu](http://aka.ms/aatpsizingtool) – nástroj pro změnu velikosti automatizuje kolekce objem přenosů služby Azure ATP monitoruje. Automaticky poskytuje možnosti podpory a zdroje doporučení pro senzory. 
- [Ochrana ATP v programu pokyny k plánování kapacity](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Nasazení služby Azure ATP

Tyto prostředky vám pomůže nastavit ochrana ATP v programu Azure, připojit k Active Directory, stažení balíčku senzoru, nastavit shromažďování událostí a volitelně integrovat vaši síť VPN a nastavit vyloučení a účty honeytokenu. 
- [Vyzkoušejte Azure ATP (součástí EMS E5)](http://aka.ms/aatptrial) zkušební verze platí po dobu 90 dnů.
- [Nastavení Azure ATP](install-atp-step1.md) nasazení služby Azure ATP ve vašem prostředí, následujícím postupem.
- [Integrace ochrany ATP v programu Azure s programem Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Nastavení služby Azure ATP

Základní nastavení potřebné v ochrany ATP v programu Azure se konfiguruje při vytváření pracovního prostoru. Existuje ale několik dalších nastavení, které můžete nakonfigurovat v ochraně ATP v Azure, zkontrolujte detekce přesnější pro vaše prostředí, jako je například integrace sítě VPN, SAM požadovaná oprávnění a pokročilé nastavení zásad auditu. 

- [Integrace sady VPN](install-atp-step6-vpn.md)
- [SAM-R, vyžaduje oprávnění](install-atp-step8-samr.md)
- [Nastavení zásad auditu](atp-advanced-audit-policy.md) – auditovat vaše stav řadiče domény před a po nasazení ochrany ATP v programu. 

## <a name="work-with-azure-atp"></a>Práce s Azure ATP

Po ochrany ATP v programu Azure je zapnutý a spuštěný, zobrazení výstrah zabezpečení v časové osy aktivity portálu ochrany ATP v programu Azure. Časové osy aktivity je výchozí cílová stránka po přihlášení na portál ochrany ATP v programu Azure. Ve výchozím nastavení jsou zobrazeny všechny výstrahy zabezpečení otevřít na časové ose útoku. Můžete také zobrazit závažnosti přiřazené jednotlivých výstrah. Zkontrolovat každé upozornění, že procházení k podrobnostem entitách (počítače, zařízení a uživatele) otevřete jejich profilové stránky s dalšími informacemi. Tyto materiály vám pomohou při práci s výstrahami zabezpečení služby Azure ATP: 

- [Azure Průvodce výstrah zabezpečení ochrany ATP v programu](suspicious-activity-guide.md) se naučíte, jak třídit a udělejte další kroky s detekcí vaší ochrany ATP v programu Azure.
- [Označit jako citlivé skupiny](sensitive-accounts.md) vizualizuje odhalení přihlašovacích údajů na zabezpečení citlivých skupin.

## <a name="security-best-practices"></a>Osvědčené postupy zabezpečení

- [Azure ATP – nejčastější dotazy](atp-technical-faq.md) – Tento článek obsahuje seznam nejčastější dotazy týkající se ochrany ATP v programu Azure a poskytuje podrobné informace a odpovědi. 

## <a name="community-resources"></a>Zdroje informací a materiály z komunity

Blog: [blogu Azure ATP](https://aka.ms/aatpblog)

Veřejné komunita: [Azure ATP technické komunity](https://aka.ms/AatpCom)

Soukromé komunity: [skupiny Yammeru ochrany ATP v programu Azure](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Kanál 9: [stránky Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>Viz také

- [Práce s citlivými účty](sensitive-accounts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)