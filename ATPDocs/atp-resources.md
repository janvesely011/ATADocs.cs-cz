---
title: Seznam užitečné zdroje informací pro rozšířené ochrany před internetovými útoky pro Azure | Dokumentace Microsoftu
description: Tento článek obsahuje seznam užitečné zdroje informací pro služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/24/2019
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cdcba87d16c357205becdeb5683e655f6ca801a0
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085278"
---
# <a name="azure-atp-readiness-guide"></a>Příručka ke službě Azure ATP připravenosti

Tento článek poskytuje asi plán připravenosti seznam prostředků, které vám pomůžou začít pracovat s rozšířené ochrany před internetovými útoky pro Azure. 

## <a name="understanding-azure-atp"></a>Principy Azure ATP

Azure Protection pokročilé před internetovými útoky (ATP) je Cloudová služba, která pomáhá identifikovat a chránit váš podnik před různými typy pokročilých cílených kybernetických útoků a ohrožením zevnitř.
 
Další informace o ochrany ATP v programu Azure: 
- [Přehled služby Azure ATP](what-is-atp.md)
- [Ochrana ATP v programu úvodní video Azure (25 minut) – úplná](https://www.youtube.com/watch?v=EGY2m8yU_KE)
- [Podrobné informace o videu Azure ochrany ATP v programu (75 minut) – úplná](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

## <a name="deployment-decisions"></a>Rozhodnutí o nasazení

Ochrana ATP v programu Azure se skládá z cloudové služby, které se nacházejí v Azure a integrované senzory, které mohou být nainstalovány na řadičích domény nebo samostatné senzorů na vyhrazené servery. Předtím, než je zprovoznění služby Azure ATP, je důležité, abyste zvolili typ snímače, nejlépe vyhovovalo vašim nasazení a potřebám. Azure ochrany ATP v programu integrované senzorů (senzorů služby Azure ATP) poskytují zvýšené zabezpečení, snížení provozních nákladů a nasazení než samostatné senzorů ochrany ATP v programu Azure. Azure senzorů samostatné ochrany ATP v programu vyžaduje fyzický hardware, další konfigurační kroky a zpracují náročnější provozní náklady. <br>Pokud používáte fyzické servery, plánování kapacity je velmi důležité. Získejte pomoc od nástroj pro změnu velikosti k přidělení místa pro vaše senzory: 
- [Azure nástroje pro změnu velikosti ochrany ATP v programu](http://aka.ms/aatpsizingtool) – nástroj pro změnu velikosti automatizuje kolekce objem přenosů služby Azure ATP monitoruje. Automaticky poskytuje možnosti podpory a zdroje doporučení pro senzory. 
- [Ochrana ATP v programu pokyny k plánování kapacity](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Nasazení služby Azure ATP

Pomocí těchto prostředků můžete nastavení ochrany ATP v programu Azure, připojit ke službě Active Directory, stažení balíčku senzoru, nastavit shromažďování událostí a volitelně integrovat vaši síť VPN a nastavit vyloučení a honeytoken účty. 
- [Vyzkoušejte Azure ATP (součástí EMS E5)](http://aka.ms/aatptrial) zkušební verze platí po dobu 90 dnů.
- [Nastavení Azure ATP](install-atp-step1.md) postupujte podle těchto kroků nasadíte ochrany ATP v programu Azure ve vašem prostředí.
- [Integrace ochrany ATP v programu Azure s programem Windows Defender ATP](integrate-wd-atp.md)

## <a name="azure-atp-settings"></a>Nastavení služby Azure ATP

Při vytváření instance vaší služby Azure ATP, základní nastavení potřebné nakonfigurují automaticky. Existuje několik dalších konfigurovatelné nastavení v Azure ATP pro zlepšení detekce a přesnost výstrah pro vaše prostředí, jako je například integrace sítě VPN, SAM požadovaná oprávnění a nastavení zásad auditu. 

- [Integrace sítě VPN](install-atp-step6-vpn.md)
- [SAM-R, vyžaduje oprávnění](install-atp-step8-samr.md)
- [Nastavení zásad auditu](atp-advanced-audit-policy.md) – auditovat vaše stav řadiče domény před a po nasazení ochrany ATP v programu. 

## <a name="work-with-azure-atp"></a>Práce s Azure ATP

Po ochrany ATP v programu Azure je zapnutý a spuštěný, zobrazení výstrah zabezpečení v časové osy aktivity portálu ochrany ATP v programu Azure. Časové osy aktivity je výchozí cílová stránka po přihlášení na portál ochrany ATP v programu Azure. Ve výchozím nastavení jsou zobrazeny všechny výstrahy zabezpečení otevřít na časové osy aktivity. Můžete také zobrazit závažnosti přiřazené jednotlivých výstrah. Zkontrolovat každé upozornění, že procházení k podrobnostem entitách (počítače, zařízení a uživatele) otevřete jejich profilové stránky s dalšími informacemi. Přesune taktiky Lateral Movement, které ukazují potenciální cesty, které lze provést v síti a ohrožení citlivých uživatelé. Prozkoumání a nápravu míru rizika pomocí grafů zjišťování cesty laterální pohyb. Tyto materiály vám pomohou při práci s výstrahami zabezpečení služby Azure ATP: 

- [Azure Průvodce výstrah zabezpečení ochrany ATP v programu](suspicious-activity-guide.md) se naučíte, jak třídit a udělejte další kroky s detekcí vaší ochrany ATP v programu Azure.
- [Cesty taktiky Lateral Movement Azure ATP](use-case-lateral-movement-path.md)
- [Označit jako citlivé skupiny](sensitive-accounts.md) vizualizuje odhalení přihlašovacích údajů na zabezpečení citlivých skupin.

## <a name="security-best-practices"></a>Osvědčené postupy zabezpečení

- [Azure ATP – nejčastější dotazy](atp-technical-faq.md) – Tento článek obsahuje seznam nejčastější dotazy týkající se ochrany ATP v programu Azure a poskytuje podrobné informace a odpovědi. 

## <a name="community-resources"></a>Zdroje informací a materiály z komunity

Blog: [Blog o Azure ATP](https://aka.ms/aatpblog)

Veřejné komunity: [Azure ATP Tech Community](https://aka.ms/AatpCom)

Soukromé komunity: [Azure ATP Yammer Group](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Kanál 9: [Stránka Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>Viz také

- [Práce s citlivými účty](sensitive-accounts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)