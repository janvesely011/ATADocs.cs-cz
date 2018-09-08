---
title: Nejčastější dotazy k Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Obsahuje seznam nejčastější dotazy týkající se ochrany ATP v programu Azure a související odpovědi
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/13/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ce3c41f1cca7e3f621ea2afbf89565e7d6009f28
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166812"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*

# <a name="azure-atp-frequently-asked-questions"></a>Nejčastější dotazy k Azure ATP
Tento článek obsahuje seznam nejčastější dotazy týkající se ochrany ATP v programu Azure a poskytuje podrobné informace a odpovědi.


## <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Kde získám licenci pro Azure Advanced Threat Protection (ATP)?

Licence můžete získat pro Enterprise Mobility + Security (EMS E5) 5 přímo prostřednictvím [portál služeb Office 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) nebo prostřednictvím licenčního modelu partnera CSP (Cloud Solution).                  

## <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>Co mám dělat, když ochrana ATP v programu Azure nebo samostatný senzor nespustí?
Podívejte se na poslední chyba aktuální chybě [protokolu](troubleshooting-atp-using-logs.md) (kde služby Azure ATP je nainstalována ve složce "Protokoly").

## <a name="how-can-i-test-azure-atp"></a>Jak můžu otestovat ochrany ATP v programu Azure?
Začátku do konce testu můžete simulovat podezřelé aktivity. V následujícím scénáři se simuluje rekognoskace DNS:

1.  Ověření ochrany ATP v programu Azure senzorů jsou nainstalovaná a nakonfigurovaná na řadičích domény (nebo samostatné senzory a související zrcadlení portů jsou nainstalované a nakonfigurované)
2.  Otevřít CMD
3.  Spusťte následující příkaz: nslookup –<DC iP address>
    1.  Stisknutím klávesy enter
    2.  Typu: Je -d <FQDN>
    3.  V závislosti na konfiguraci vašeho prostředí se odpovědi liší z "Bylo odmítnuto dotazu" na seznam záznamů DNS. 
4. Zobrazte výstrahy související s Simulovaná rekognoskace DNS v konzole služby Azure ATP. 

## <a name="does-azure-atp-work-with-encrypted-traffic"></a>Služba Ochrana ATP v programu Azure funguje při šifrovaném provozu?
Ochrana ATP v programu Azure spoléhá na analýzu více síťových protokolů, událostí shromážděných ze systému SIEM nebo prostřednictvím předávání událostí Windows.  Síťové protokoly s šifrovaný provoz (například LDAPS nebo IPSEC) nejsou dešifrovat, ale jsou analyzovány.


## <a name="does-azure-atp-work-with-kerberos-armoring"></a>Služba Ochrana ATP v programu Azure funguje s obranou protokolu Kerberos?
Povolení obrany protokolu Kerberos, označované také jako FAST Flexible Authentication Secure Tunneling (), je podporována ochrana ATP v programu, s výjimkou pass typu over-pass-the hash detekce, což nefunguje s obranou protokolu Kerberos.

## <a name="how-many-azure-atp-sensors-do-i-need"></a>Počet senzorů ochrany ATP v programu Azure budu potřebovat?

Každý řadič domény v prostředí měly být pokryté komponentami ochrany ATP v programu nebo samostatného senzoru. Další informace najdete v tématu [senzoru služby Azure ATP velikosti](atp-capacity-planning.md#sizing). 


## <a name="why-are-certain-accounts-considered-sensitive"></a>Proč se některé účty považují za citlivé?
To se stane, když je účet členem skupiny, které jsou určené jako citlivé (například: "Domain Admins").

Pokud chcete pochopit, proč je účet citlivý, můžete zkontrolovat jeho členství ve skupinách a zjistit, do kterých citlivých skupin patří (skupina, do které patří, může být citlivá také kvůli jiné skupině, takže je potřeba celý proces opakovat tak dlouho, až zjistíte citlivou skupinu nejvyšší úrovně). Můžete také [značky jako citlivé účty ručně](sensitive-accounts.md).

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Jak můžu monitorovat virtuální řadič domény pomocí ochrany ATP v programu Azure?
Většina virtuálních řadičů domény dají pokrýt komponentami senzoru služby Azure ATP, chcete-li zjistit, zda služby Azure ATP senzor je vhodné pro vaše prostředí [plánování kapacity ochrany ATP v programu Azure](atp-capacity-planning.md).

Pokud se virtuální řadič domény nedá pokrýt komponentou senzoru služby Azure ATP, jak je popsáno v může mít buď virtuální nebo fyzická ochrana ATP v programu Azure samostatný senzor [konfigurace zrcadlení portů](configure-port-mirroring.md).  <br />Nejjednodušší je mít virtuální samostatný senzor ochrany ATP v programu Azure na každém hostiteli, kde existují virtuální řadič domény.<br />Pokud virtuální řadiče domény přesunují mezi hostiteli, je třeba provést jednu z následujících kroků:

-   Pokud se virtuální řadič domény přesune na jiného hostitele, předem nakonfigurujte samostatný senzor ochrany ATP v programu Azure v tomto hostiteli příjem provozu z nedávno přesunutého virtuálního řadiče domény.
-   Ujistěte se, že jste přidružili virtuální samostatný senzor ochrany ATP v programu Azure pomocí virtuálního řadiče domény tak, že pokud se přesune, samostatného senzoru služby Azure ATP se přesune s ním.
-   Některé virtuální přepínače mohou odesílat provoz mezi hostiteli.


## <a name="what-can-azure-atp-detect"></a>Co dokáže ochrana ATP v programu Azure?

Ochrana ATP v programu Azure zjistí známé nebezpečné útoky a techniky, problémy se zabezpečením a rizika.
Úplný seznam detekcí ochrany ATP v programu Azure najdete v tématu [jaké detekce ochrany ATP v programu Azure provádí?](suspicious-activity-guide.md).

## <a name="how-many-nics-does-the-azure-atp-standalone-sensor-require"></a>Kolik síťových adaptérů vyžaduje samostatný senzor ochrany ATP v programu Azure?
Samostatný senzor ochrany ATP v programu Azure vyžaduje minimálně dva síťové adaptéry:<br>1. Síťovou kartu pro připojení k interní síti a cloudové služby Azure ATP<br>2. Síťové rozhraní, který se používá k zachycení síťového provozu na řadiči domény prostřednictvím zrcadlení portů.<br>* To neplatí pro senzoru služby Azure ATP, která nativně využívá všechny síťové adaptéry využívané řadičem domény.

## <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Jaký druh integrace ochrany ATP v programu Azure má se systémy Siem?
Ochrana ATP v programu Azure má obousměrnou integraci se systémy Siem následujícím způsobem:

1. Ochrana ATP v programu Azure lze nakonfigurovat na odesílání výstrahy Syslog na libovolný server SIEM pomocí formátu CEF pro výstrahy týkající se stavu a když zjistí podezřelou aktivitu.
2. Dá se ochrana ATP v programu Azure pro příjem zprávy Syslog pro události Windows z [těchto systémů Siem](configure-event-collection.md).

## <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Jak nakonfigurovat senzorů ochrany ATP v programu Azure komunikovat s cloudovou službou ochrany ATP v programu Azure, pokud proxy server?

Pro řadiče domény ke komunikaci s cloudovou službou, je nutné otevřít: *. atp.azure.com port 443 v brány firewall a proxy. Pokyny, jak to udělat, najdete v části [konfigurace proxy serveru nebo brány firewall k umožnění komunikace s Azure ATP senzorů](configure-proxy.md).
 

## <a name="can-azure-atp-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Ochrana ATP v programu Azure můžete monitorovat řadiče domény virtualizované ve vašem řešení IaaS?
Senzoru služby Azure ATP Ano, můžete použít k monitorování řadičů domény, které jsou v libovolném řešení IaaS.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Bude součástí Azure Active Directory nebo místní služby Active Directory?
Toto řešení je momentálně samostatné nabídky. Není součástí Azure Active Directory nebo místní služby Active Directory.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Je potřeba psát vlastní pravidla a určovat prahové nebo základní hodnoty?
S Azure Advanced Threat Protection není nutné k vytváření pravidel ani prahových nebo standardní hodnoty a jejich následné vyladění. Ochrana ATP v programu Azure analyzuje chování uživatelů, zařízení a prostředků, a také jejich vzájemných vztazích – a dokáže detekovat podezřelé aktivity a známé útoky se rychle. Tři týdny po nasazení služby Azure ATP začne detekovat behaviorálně podezřelé aktivity. Na druhé straně ochrany ATP v programu Azure začne okamžitě po nasazení detekuje známé útoky se zlými úmysly a problémy se zabezpečením.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>Využívají se přitom jenom přenosy služby Active Directory?
Kromě analýzy provozu služby Active Directory s využitím technologie kontrolu paketů na služby Azure ATP taky shromažďuje relevantní události ze informace o zabezpečení a správu událostí (SIEM) a vytváří profily entit na základě informací ze služby Active Directory Domain Services. Pokud používáte senzoru služby Azure ATP, extrahuje tyto události automaticky. Předávání událostí Windows můžete použít k odesílání tyto události do samostatného senzoru služby Azure ATP. Ochrana ATP v programu Azure podporuje také přijímající monitorování účtů protokolu RADIUS sítě VPN protokolů od různých dodavatelů (Microsoft, Cisco, F5 a kontrolního bodu).

## <a name="what-is-port-mirroring"></a>Co je zrcadlení portů?
Zrcadlení portů, které se taky označuje jako SPAN (Switched Port Analyzer), je metoda monitorování síťových aktivit. Pokud je zrcadlení portů povolené, přepínač odešle kopii všech síťových paketů zjištěných na jednom portu (nebo v celé síti VLAN) na jiný port, kde se tyto pakety dají analyzovat.

## <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Ochrany ATP v programu Azure monitorovat pouze zařízení připojená k doméně?
Ne. Ochrana ATP v programu Azure monitoruje všechna zařízení v síti, která zpracovávají požadavky ověřování a autorizace s Active Directory, včetně mimo Windows a mobilní zařízení.

## <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Monitorování ochrany ATP v programu Azure účty počítačů a také uživatelské účty?
Ano. Protože počítače účty (stejně jako ostatní entity) lze použít k provádění škodlivých aktivit, ochrana ATP v programu Azure monitoruje chování všech účtů počítačů a všechny ostatní entity v příslušném prostředí.

## <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Ochrana ATP v programu Azure může podporovat víc domén a doménových struktur?
Azure Advanced Threat Protection podporuje prostředí s více doménami a několik doménových struktur. Tato funkce je aktuálně ve verzi public preview. Další informace a známých omezeních najdete v tématu [podporu více doménovými strukturami](atp-multi-forest.md).

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Dá se zjistit celkový stav nasazení?
Ano, můžete zobrazit celkový stav nasazení a také konkrétní problémy související s konfigurací, připojení atd. kde se zobrazí výstraha při jejich výskytu.

## <a name="what-data-does-azure-atp-collect"></a>Jaká data shromažďuje nástroj ochrany ATP v programu Azure? 
Ochrana ATP v programu Azure shromažďuje a ukládá informace od nakonfigurované servery (řadiče domény, členské servery atd.) v databázi specifické pro službu pro správu, sledování a generování sestav. Mezi shromažďované informace patří síťový provoz do a z řadiče domény (jako je například ověřování protokolem Kerberos, ověřování protokolem NTLM, dotazy DNS), protokoly zabezpečení (například události zabezpečení Windows), údajům služby Active Directory (struktura, podsítí, serverů), a informací o entitách (jako je například jména, e-mailové adresy a telefonní čísla). 

Společnost Microsoft používá tato data: 

-   Aktivně Identifikujte indikátory útoku (IOAs) ve vaší organizaci 
-   Generovat výstrahy, pokud byl zjištěn možný útok 
-   Zadejte operací zabezpečení pohled na entity související signály před internetovými útoky ze sítě, která vám umožní prozkoumat a prozkoumejte přítomnost bezpečnostní hrozby v síti. 

Microsoft není dolovat data pro reklamní účely nebo k jiným účelům než poskytováním služby. 

## <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Je nutné možnost vyberte, kam chcete uložit Moje data? 

Při vytváření pracovního prostoru ochrana ATP v programu Azure, které můžete ukládat data, můžete k ukládání dat v datových center Microsoft Azure v USA nebo Evropa. Po nakonfigurování nejde změnit umístění, kde se vaše data jsou uložená. Microsoft nebude přenášet data ze zadaného umístění. 

## <a name="is-my-data-isolated-from-other-customer-data"></a>Jsou moje data nezávisle ostatní zákaznická data? 

Ano, vaše data jsou izolované na základě ověřování přístupu a logické oddělení podle identifikátoru zákazníka. Každý zákazník přístupná pouze data shromážděná z vlastní organizace a obecná data, která poskytuje Microsoft. 

## <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Jak Microsoft zabránit aktivity zlými úmysly a zneužití vysoká oprávnění rolí? 

Microsoft vývojářům a správcům, podle návrhu, mít dostatečná oprávnění k provedení jejich přiřazené povinnosti, aby provoz a umožněte vývoj služby. Microsoft nasazuje kombinací preventivní detektiv a reaktivní ovládacích prvků, včetně následujících mechanismů a pomáhá chránit před neoprávněným pro vývojáře a/nebo aktivita správy: 

-   Ovládací prvek úzkou přístup k citlivým datům 
-   Kombinací ovládacích prvků, které může to výrazně zvýšit nezávislé odhalování škodlivých aktivit 
-   Více úrovní monitorování, protokolování a vytváření sestav 

Kromě toho Microsoft provádí kontroly podstupovaly ověřování u správců osobní prověrku určité operace a omezuje přístup k aplikacím, systémy a síťovou infrastrukturu výkonový zisk úroveň ověřování probíhá na pozadí. Operace pracovníky postupujte podle formální proces, když jsou potřeba pro přístup k účtu zákazníka nebo související informace v plnění jejich úkolů. 

## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
