---
title: Podpora více doménovými strukturami Azure rozšířené ochrany před internetovými útoky | Dokumentace Microsoftu
description: Podpora několika doménových struktur služby Active Directory do služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 00718998299590f658f8cdd6c7e2fc21c553210c
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65195586"
---
# <a name="azure-advanced-threat-protection-multi-forest-support"></a>Podpora více doménovými strukturami Azure Advanced Threat Protection


## <a name="multi-forest-support-set-up"></a>Podpora více doménovými strukturami nastavení 

Ochrana ATP v programu Azure podporuje organizace s víc doménovými strukturami, což vám umožní snadno monitorovat aktivity a profily uživatelů napříč doménovými strukturami. 

Organizace obvykle mívají několik doménových struktur služby Active Directory – často používají pro různé účely, třeba zastaralou infrastrukturu z podnikové fúze a akvizice, zeměpisné distribuce a hranice zabezpečení (červená doménové struktury). Může chránit několik doménových struktur pomocí služby Azure ATP, poskytne vám umožňuje monitorovat a prozkoumávat celou svou síť prostřednictvím podokně ze skla.

Schopnost podporují více doménových struktur služby Active Directory umožňuje následující:
-   Zobrazení a prošetřování aktivity prováděné uživateli napříč více doménovými strukturami, v podokně ze skla. 
-   Vylepšený detekční a nižší počet falešných poplachů tím, že poskytuje pokročilé řešení integrace a účet služby Active Directory. 
-   Jednodušší nasazení a větší kontrolu. Vylepšené výstrahy monitorování a vytváření sestav pro pokrytí napříč organizací, když všechny řadiče domény jsou monitorované z jediné konzoly ochrany ATP v programu Azure.


## <a name="azure-atp-detection-activity-across-multiple-forests"></a>Detekce aktivit v Azure ATP napříč více doménovými strukturami 

Ke zjištění aktivity mezi doménovými strukturami, senzory ochrany ATP v programu Azure dotazovat řadiče domény ve vzdálených doménových strukturách vytvořit profily pro všechny entity (včetně uživatelů a počítačů ze vzdálených doménových strukturách). 

- Azure senzorů ochrany ATP v programu lze nainstalovat na všechny doménové struktury, dokonce i doménové struktury bez vztahu důvěryhodnosti.
- Přidáte přihlašovací údaje na stránce adresáře služby pro všechny doménové struktury ve vašem prostředí. 
    - Přihlašovacích údajů se vyžaduje pro každou doménovou strukturu s obousměrným vztahem důvěryhodnosti. 
    - Další přihlašovací údaje jsou požadovány pro každou doménovou strukturu s důvěryhodností protokolu Kerberos nebo žádný vztah důvěryhodnosti. 
    - Limit 10 doménové struktury na instanci služby Azure ATP. Pokud má vaše organizace více než 10 doménových struktur, obraťte se na podporu. 

![Azure ATP úvodní fáze 1](media/directory-services-add-no-trust-forests.png)

### <a name="requirements"></a>Požadavky 

- Uživatel, který konfigurujete v konzole služby Azure ATP v **adresářové služby** musí důvěřovat ve všech dalších doménových struktur a musí mít alespoň oprávnění jen pro čtení k provádění dotazů LDAP na řadiče domény.
- Pokud samostatný senzorů ochrany ATP v programu Azure jsou nainstalovány na samostatné počítače, nikoli přímo na řadiče domény, ujistěte se, že počítače jsou povoleny pro komunikaci se všemi vzdálené doménové struktuře řadičů domény pomocí protokolu LDAP. 

- Aby ochrany ATP v programu Azure ke komunikaci s senzorů ochrany ATP v programu Azure a služby Azure ATP samostatné senzory otevřete následující porty na každém počítači, na kterém jsou nainstalované senzory ochrany ATP v programu Azure:
 
  |Protocol (Protokol)|Přenos|Port|Směr|Direction|
  |----|----|----|----|----|
  |**Porty Internet**||||
  |SSL (*.atp.azure.com)|TCP|443|Cloudovou službu Azure ATP|Odchozí|
  |**Interní porty**||||           
  |LDAP|TCP a UDP|389|Řadiče domény|Odchozí|
  |Zabezpečený LDAP (LDAPS)|TCP|636|Řadiče domény|Odchozí|
  |LDAP pro globální katalog|TCP|3268|Řadiče domény|Odchozí|
  |LDAPS pro globální katalog|TCP|3269|Řadiče domény|Odchozí|


## <a name="multi-forest-support-network-traffic-impact"></a>Podpora více doménovými strukturami síťové přenosy dopad 

Ochrana ATP v programu Azure maps vaší doménové struktury, využívá proces, který má vliv na následující:

-   Po spuštění senzoru služby Azure ATP dotazuje vzdálených doménových strukturách služby Active Directory a načte seznam uživatelů a počítačů data pro vytvoření profilu.
-   Každých 5 minut, každý senzoru služby Azure ATP dotazuje jeden řadič domény v každé doméně, v každé doménové struktuře, mapovat všechny doménové struktury v síti.
-   Každý senzoru služby Azure ATP mapuje pomocí objektu "trustedDomain" ve službě Active Directory, přihlášení a kontrola typu vztahu důvěryhodnosti doménové struktury.
-   Může také zobrazit ad-hoc provoz, když zjistí aktivitu napříč doménovou strukturu senzoru služby Azure ATP. Když k tomu dojde, senzorů ochrany ATP v programu Azure pošle dotaz LDAP na příslušných řadičích domény získat informace o entitě. 

## <a name="known-limitations"></a>Známá omezení
-   Interaktivní prováděného uživateli v jedné doménové struktuře pro přístup k prostředkům v jiné doménové struktuře nejsou zobrazeny v řídicím panelu služby Azure ATP.



## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Architektura služby Azure ATP](atp-architecture.md)
- [Instalace služby Azure ATP](install-atp-step1.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

