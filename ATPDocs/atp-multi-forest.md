---
title: Podpora vícenásobného doménovými strukturami Azure rozšířené ochrany před internetovými útoky | Dokumentace Microsoftu
description: Jak nastavit podporu několika doménových struktur služby Active Directory do služby Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/17/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c76e459709c786082bea7566a61e5384a235eda4
ms.sourcegitcommit: 8feb9b65dc0e1de0ace00aca11784e54f9852a15
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39098198"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*

# <a name="install-azure-atp---step-9"></a>Instalace služby Azure ATP - kroku 9

>[!div class="step-by-step"]
[«Krok 8](install-atp-step8-samr.md)

## <a name="step-9--set-up-azure-advanced-threat-protection-multi-forest-support"></a>Krok 9:  Nastavte podporu více doménovými strukturami rozšířené ochrany před internetovými útoky pro Azure

Ochrana ATP v programu Azure může podporovat organizace s víc doménovými strukturami, které poskytuje možnost monitorování aktivity a profily uživatelů napříč doménovými strukturami. 

Podnikové organizace může mít několik doménových struktur služby Active Directory – často používají pro různé účely, třeba zastaralou infrastrukturu z podnikové fúze a akvizice, zeměpisné distribuce a hranice zabezpečení (červená doménové struktury). Může chránit několik doménových struktur pomocí služby Azure ATP, všechna data pro generování sestav do jednoho, primární pracovní prostor poskytuje možnost monitorovat a prozkoumávat prostřednictvím podokně ze skla.

Schopnost podporují více doménových struktur služby Active Directory umožňuje následující:
-   Můžete zobrazit a prozkoumat aktivity prováděné uživateli napříč více doménovými strukturami z podokně ze skla. 
-   Podpora více doménovými strukturami zvyšuje zjišťování a snižuje počet falešně pozitivních výsledků tím, že poskytuje pokročilé integrace služby Active Directory a účet řešení. 
-   Vzhledem k tomu, že podpora více foresst eliminuje potřebu víc pracovních prostorů, budete mít větší kontrolu a snazší nasazení řadiče domény jsou všechny centrálně monitorovat z jedné služby Azure ATP konzola, která poskytuje lepší monitorování výstrahy a vytváření sestav pro pokrytí napříč organizací.


## <a name="how-azure-atp-detects-activities-across-multiple-forests"></a>Jak služby Azure ATP detekuje aktivity napříč více doménovými strukturami 

Ke zjištění aktivity mezi doménovými strukturami, senzory ochrany ATP v programu Azure dotazovat řadiče domény ve vzdálených doménových strukturách vytvořit profily pro všechny entity používané, včetně uživatelů a počítačů ze vzdálených doménových strukturách. 

> [!NOTE]
> - V pořadí, aby to fungovalo musí důvěřovat doménové struktuře, ve kterém jsou nainstalované senzory ochrany ATP v programu Azure všechny ostatní doménové struktury.
> - Uživatel, který konfigurujete v konzole služby Azure ATP v **adresářové služby** musí důvěřovat ve všech dalších doménových struktur.


Pokud máte doménových struktur, na které žádné služby Azure ATP jsou nainstalované senzory, můžete zobrazit a sledovat aktivity pocházející z těchto doménových strukturách stále ochrany ATP v programu Azure. Senzorů ochrany ATP v programu nainstalovat se můžete dotazovat řadiče domény všechny připojené vzdálené doménové struktuře řešení uživatelů a počítačů a vytvořit profily pro každý z nich. 

## <a name="installation-requirements"></a>Požadavky na instalaci 

-   Pokud samostatný senzorů ochrany ATP v programu Azure jsou nainstalovány na samostatné počítače, nikoli přímo na řadiče domény, ujistěte se, že počítače jsou povoleny pro komunikaci se všemi vzdálené doménové struktuře řadičů domény pomocí protokolu LDAP. 
- Uživatel, který konfigurujete v konzole služby Azure ATP v **adresářové služby** musí důvěřovat ve všech dalších doménových struktur a musí mít alespoň oprávnění ke čtení jenom k provádění dotazů LDAP řadiče domény.

- Aby Azure ochrany ATP v programu předat ochrany ATP v programu senzory a ochrana ATP v programu samostatné senzorů otevřete následující porty na každý Machine, na kterém jsou nainstalované senzory ochrany ATP v programu:

 
  |Protokol|Přenos|Port|Směr|Direction|
  |----|----|----|----|----|
  |**Porty Internet**||||
  |SSL (*.atp.azure.com)|TCP|443|Cloudovou službu Azure ATP|Odchozí|
  |**Interní porty**||||           
  |LDAP|TCP a UDP|389|Řadiče domény|Odchozí|
  |Zabezpečený LDAP (LDAPS)|TCP|636|Řadiče domény|Odchozí|
  |LDAP pro globální katalog|TCP|3268|Řadiče domény|Odchozí|
  |LDAPS pro globální katalog|TCP|3269|Řadiče domény|Odchozí|


## <a name="multi-forest-support-network-traffic-impact"></a>S více přenosovými doménové struktury podpory síťové přenosy dopad 

Ochrana ATP v programu Azure maps vaší doménové struktury, využívá proces, který má vliv na následující:

-   Po spuštění senzoru služby Azure ATP dotazuje vzdálených doménových strukturách služby Active Directory a načte seznam uživatelů a počítačů data pro vytvoření profilu.
-   Každých 5 minut, každý senzoru služby Azure ATP dotazuje jeden řadič domény v každé doméně, v každé doménové struktuře, mapovat všechny doménové struktury v síti.
-   Každý senzoru služby Azure ATP mapuje pomocí objektu "trustedDomain" ve službě Active Directory, přihlášení a kontrola typu vztahu důvěryhodnosti doménové struktury.
-   Může také zobrazit ad-hoc provoz při ochrany ATP v programu senzor zachytí aktivity napříč doménovou strukturu. Když k tomu dojde, senzory ochrany ATP v programu pošle dotaz LDAP na příslušných řadičích domény v pořadí načtení entity informace. 

## <a name="known-limitations"></a>Známá omezení
-   Interaktivní prováděného uživateli v jedné doménové struktuře pro přístup k prostředkům v jiné doménové struktuře nejsou zobrazeny v řídicím panelu služby Azure ATP.


>[!div class="step-by-step"]
[«Krok 8](install-atp-step8-samr.md)


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti ATA](http://aka.ms/aatpsizingtool)
- [Architektura ATA](atp-architecture.md)
- [Instalace ATA](install-atp-step1.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)

