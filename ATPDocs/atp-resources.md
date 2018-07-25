---
title: Seznam užitečné zdroje informací pro rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Tento článek obsahuje seznam užitečné zdroje informací pro služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/23/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 498d1b4d14db079583da1999bfb68a5648111362
ms.sourcegitcommit: 63a36cd96aec30e90dd77bee1d0bddb13d2c4c64
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/24/2018
ms.locfileid: "39227134"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*



# <a name="azure-atp-readiness-guide"></a>Příručka ke službě Azure ATP připravenosti

Tento článek vám poskytne plány připravenosti, které poskytuje seznam prostředků, které pomáhají vám umožní začít s Azure Advanced Threat Analytics. 

## <a name="understanding-azure-atp"></a>Principy Azure ATP

Azure Protection pokročilé před internetovými útoky (ATP) je Cloudová služba, která pomáhá chránit váš podnik před různými typy pokročilých cílených kybernetických útoků a ohrožením zevnitř. Další informace o ochrany ATP v programu Azure použijte následující prostředky: 
- [Přehled služby Azure ATP](what-is-atp.md)
- [Ochrana ATP v programu úvodní video Azure – úplná](https://www.youtube.com/watch?v=KX-xpFc0sBw) 

## <a name="deployment-decisions"></a>Rozhodnutí o nasazení

Ochrana ATP v programu Azure se skládá z cloudové služby, které se nacházejí v Azure a snímače, které lze nainstalovat na řadič domény nebo vyhrazené servery. Předtím, než je zprovoznění služby Azure ATP, je důležité, abyste zvolili, jaký typ lépe vyhovovalo vašim senzorů vašeho nasazení.<br>Pokud používáte fyzické servery, měli byste naplánovat kapacitu. Nápovědu získáte z nástroje pro změnu velikosti k přidělení místa pro vaše senzory: 
- [Azure nástroje pro změnu velikosti ochrany ATP v programu](http://aka.ms/aatpsizingtool) – nástroj pro změnu velikosti automatizuje kolekce objem přenosů služby Azure ATP monitoruje. Automaticky poskytuje možnosti podpory a zdroje doporučení pro senzory. 
- [Pokyny plánování kapacity ATA](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Nasazení služby Azure ATP

Tyto prostředky vám pomůže nastavit ochrana ATP v programu Azure, připojit k Active Directory, stažení balíčku senzoru, nastavit shromažďování událostí a volitelně integrovat vaši síť VPN a nastavit vyloučení a účty honeytokenu. 
- [Vyzkoušejte Azure ATP (součástí EMS E5)](http://aka.ms/aatptrial) zkušební verze platí po dobu 90 dnů.
- [Průvodce nasazením](install-atp-step1.md) nasazení služby Azure ATP ve vašem prostředí, následujícím postupem.
- [Integrace ochrany ATP v programu Azure s programem Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Nastavení služby Azure ATP

Základní nastavení potřebné v ochrany ATP v programu Azure se konfiguruje při vytváření pracovního prostoru. Existuje ale několik dalších nastavení, které můžete nakonfigurovat a doladit ochrany ATP v programu Azure, která přesnějšího detekce pro vaše prostředí, jako je například integrace řešení SIEM a auditovat jejich nastavení. 

- [Obecná dokumentace Azure ATP](what-is-atp.md)
- [Nastavení auditu](https://blogs.technet.microsoft.com/positivesecurity/2017/08/18/ata-auditing-auditpol-advanced-audit-settings-enforcement-lightweight-gateway-service-discovery/) – auditovat vaše stav řadiče domény před a po nasazení ATA. 

## <a name="work-with-azure-atp"></a>Práce s Azure ATP

Po vytvoření a spuštění je ochrana ATP v programu Azure, budete moci zobrazíte podezřelých aktivit, které se zjistí aktivita časové ose. Toto je výchozí cílová stránka, kterou budete přesměrováni na přihlášení k portálu ochrany ATP v programu Azure. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila. Zkontrolovat každou podezřelou aktivitu, že procházení k podrobnostem entitách (počítače, zařízení a uživatele) otevřete jejich profilové stránky, které poskytují další informace. Tyto prostředky vám usnadní práci s Azure ATP podezřelými aktivitami: 

- [Průvodce prošetřováním podezřelých aktivit Azure ATP](suspicious-activity-guide.md) se naučíte, jak třídit a udělejte další kroky s detekcí vaší ochrany ATP v programu Azure.
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
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)