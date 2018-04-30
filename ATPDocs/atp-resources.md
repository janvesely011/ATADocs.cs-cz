---
title: Seznam užitečné zdroje pro Azure Advanced Threat Protection | Microsoft Docs
description: Tento článek obsahuje seznam užitečné zdroje pro Azure ATP
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/29/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 34dc152c-6b7f-4128-93fe-aad56c282730
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b8d91468664a76436078772ad1fc8510ea56d67a
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/30/2018
---
*Platí pro: Azure Advanced Threat Protection*



# <a name="azure-atp-readiness-guide"></a>Průvodce připravenosti Azure ATP

Tento článek obsahuje plán připravenosti, který vám poskytne seznam prostředky, které pomáhají vám umožní začít s Azure Advanced Threat Analytics. 

## <a name="understanding-azure-atp"></a>Seznámení s Azure ATP

Azure ochrany rozšířené hrozba (ATP) je Cloudová služba, která pomáhá chránit vaše organizace z více typů pokročilými cílenými útoky internetový i vnitřními hrozbami. Další informace o Azure ATP použijte v následujících zdrojích informací: 
- [Přehled služby Azure ATP](what-is-atp.md)
- [Azure, ATP úvodní video – úplná](https://www.youtube.com/watch?v=KX-xpFc0sBw) 

## <a name="deployment-decisions"></a>Rozhodnutí o nasazení

Azure ATP se skládá z cloudové služby, které se nacházejí v Azure a senzory, které je možné nainstalovat na řadič domény nebo na vyhrazené servery. Než získáte Azure ATP spuštěná, je důležité, abyste zvolili co typ lépe vyhovovala vašim senzorů vaše nasazení.<br>Pokud používáte fyzické servery, měli byste naplánovat kapacitu. Získat pomoc od nástroj pro změnu velikosti k přidělení místa pro vaše snímače: 
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool) – nástroj pro změnu velikosti automatizuje kolekce objem provozu monitoruje Azure ATP. Automaticky poskytuje možnosti podpory a doporučení prostředků pro senzorů. 
- [Pokyny plánování kapacity ATA](atp-capacity-planning.md)

## <a name="deploy-azure-atp"></a>Nasazení Azure ATP

Tyto prostředky vám pomůže nastavit Azure ATP, připojit ke službě Active Directory, stáhněte si balíček senzor, nastavit shromažďování událostí a volitelně můžete integrovat vaši síť VPN a nastavení účtů honeytokenu a vyloučení. 
- [Zkuste ATP Azure (součást EMS E5)](http://aka.ms/aatptrial) tuto zkušební verzi platí 90 dní.
- [Průvodce nasazením](install-atp-step1.md) nasazení ATP Azure ve vašem prostředí následujícím postupem.
- [Integrovat Azure ATP programu Windows Defender ATP](integrate-wd-atp.md)
- 
## <a name="azure-atp-settings"></a>Nastavení Azure ATP

Základní potřebná nastavení v Azure ATP se konfiguruje při vytváření pracovního prostoru. Existují však několik dalších nastavení, která můžete nakonfigurovat a doladit tak Azure ATP které provedou detekce přesnější pro vaše prostředí, jako je například SIEM integrace a nastavení auditu. 

- [ATP obecné dokumentace k Azure](what-is-atp.md)
- [Nastavení auditování](https://blogs.technet.microsoft.com/positivesecurity/2017/08/18/ata-auditing-auditpol-advanced-audit-settings-enforcement-lightweight-gateway-service-discovery/) – auditovat vaše stav řadiče domény, před a po nasazení ATA. 

## <a name="work-with-azure-atp"></a>Práce s Azure ATP

Po Azure ATP je spuštěná, bude moci zobrazit podezřelé aktivity, které jsou zjištěna v časové ose aktivity. Toto je výchozí cílová stránka, ke které se otevře při přihlášení k portálu Azure ATP. Ve výchozím nastavení jsou všechny otevřené podezřelé aktivity zobrazené na časové ose útoků. Můžete také zjistit závažnost, která se jednotlivým aktivitám přiřadila. Každá podezřelá aktivita šetření tak, že procházení k podrobnostem entit (počítače, zařízení, uživatelé) pro otevření jejich profil stránek, které poskytují další informace ohledně. Tyto prostředky vám usnadní práci s podezřelými aktivitami Azure ATP: 

- [Průvodce podezřelou aktivitu Azure ATP](suspicious-activity-guide.md) postup rychlou kontrolu a provést další kroky s vaší detekce Azure ATP.
- [Značka skupiny jako velká a malá písmena](sensitive-accounts.md) získat přehled o odhalení přihlašovacích údajů ke skupině citlivé zabezpečení.

## <a name="security-best-practices"></a>Osvědčené postupy zabezpečení

- [Azure ATP – nejčastější dotazy](atp-technical-faq.md) – Tento článek obsahuje seznam nejčastějších dotazů týkajících Azure ATP a poskytuje podrobné informace a odpovědi. 
## <a name="community-resources"></a>Zdroje informací a materiály z komunity

Blog: [blog Azure ATP](https://aka.ms/aatpblog)

Veřejné komunity: [Azure ATP technické komunity](https://aka.ms/AatpCom)

Komunita privátní: [skupiny Yammer ATP Azure](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893&view=all)

Kanál 9: [stránku Microsoft Security Channel 9](https://channel9.msdn.com/Shows/Microsoft-Security/)



## <a name="see-also"></a>Viz také

- [Práce s citlivými účty](sensitive-accounts.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)