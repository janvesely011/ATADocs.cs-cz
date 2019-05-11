---
title: Nejčastější dotazy k Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Obsahuje seznam nejčastější dotazy týkající se ochrany ATP v programu Azure a související odpovědi
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 04/07/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c844aa445378643200997d4389a3bee1aae45099
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65195505"
---
# <a name="azure-atp-frequently-asked-questions"></a>Nejčastější dotazy k Azure ATP
Tento článek obsahuje seznam častých otázek a odpovědí týkajících se ochrany ATP v programu Azure rozdělené do následujících catergories: 
- [Co je ochrana ATP v programu Azure](#what-is-azure-atp)
- [Licencování a ochrany osobních údajů](#licensing-and-privacy)
- [Nasazení](#deployment)
- [Operace](#operation)
- [Odstraňování potíží](#troubleshooting)

## <a name="what-is-azure-atp"></a>Co je ochrana ATP v programu Azure?

### <a name="what-can-azure-atp-detect"></a>Co dokáže ochrana ATP v programu Azure?

Ochrana ATP v programu Azure zjistí známé nebezpečné útoky a techniky, problémy zabezpečení a rizika pro vaši síť.
Úplný seznam detekcí ochrany ATP v programu Azure najdete v tématu [jaké detekce ochrany ATP v programu Azure provádí?](suspicious-activity-guide.md).

### <a name="what-data-does-azure-atp-collect"></a>Jaká data shromažďuje nástroj ochrany ATP v programu Azure? 

Ochrana ATP v programu Azure shromažďuje a ukládá informace od nakonfigurované servery (řadiče domény, členské servery atd.) v databázi specifické pro službu pro správu, sledování a generování sestav. Mezi shromažďované informace patří síťový provoz do a z řadiče domény (jako je například ověřování protokolem Kerberos, ověřování protokolem NTLM, dotazy DNS), protokoly zabezpečení (například události zabezpečení Windows), údajům služby Active Directory (struktura, podsítí, serverů), a informací o entitách (jako je například jména, e-mailové adresy a telefonní čísla). 

Společnost Microsoft používá tato data: 

-   Aktivně Identifikujte indikátory útoku (IOAs) ve vaší organizaci 
-   Generovat výstrahy, pokud byl zjištěn možný útok 
-   Zadejte operací zabezpečení pohled na entity související signály před internetovými útoky ze sítě, která vám umožní prozkoumat a prozkoumejte přítomnost bezpečnostní hrozby v síti. 

Microsoft není dolovat data pro reklamní účely nebo k jiným účelům než poskytováním služby. 

### <a name="does-azure-atp-only-leverage-traffic-from-active-directory"></a>Využívat ochrany ATP v programu Azure jenom přenosy služby Active Directory?

Kromě analýzy provozu služby Active Directory s využitím technologie kontrolu paketů na služby Azure ATP taky shromažďuje relevantní události Windows z řadiče domény a vytváří profily entit na základě informací ze služby Active Directory Domain Services. Ochrana ATP v programu Azure podporuje také přijímající monitorování účtů protokolu RADIUS sítě VPN protokolů od různých dodavatelů (Microsoft, Cisco, F5 a kontrolního bodu).

### <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Ochrany ATP v programu Azure monitorovat pouze zařízení připojená k doméně?
Ne. Ochrana ATP v programu Azure monitoruje všechna zařízení v síti, která zpracovávají požadavky ověřování a autorizace s Active Directory, včetně mimo Windows a mobilní zařízení.

### <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Monitorování ochrany ATP v programu Azure účty počítačů a také uživatelské účty?
Ano. Protože počítače účty (stejně jako ostatní entity) lze použít k provádění škodlivých aktivit, ochrana ATP v programu Azure monitoruje chování všech účtů počítačů a všechny ostatní entity v příslušném prostředí.

## <a name="licensing-and-privacy"></a>Licencování a ochrany osobních údajů 

### <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Kde získám licenci pro Azure Advanced Threat Protection (ATP)?

Ochrana ATP v programu Azure je k dispozici jako součást řešení Enterprise Mobility + Security 5 suite (EMS E5) a jako samostatnou licenci. Můžete získat licence přímo od [portálu služeb Microsoft 365](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing) nebo prostřednictvím licenčního modelu partnera CSP (Cloud Solution).

### <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Bude součástí Azure Active Directory nebo místní služby Active Directory?
Toto řešení ochrany ATP v programu Azure je momentálně samostatné nabídky. Není součástí Azure Active Directory nebo místní služby Active Directory.

### <a name="is-my-data-isolated-from-other-customer-data"></a>Jsou moje data nezávisle ostatní zákaznická data? 

Ano, vaše data jsou izolované na základě ověřování přístupu a logické oddělení podle zákazníka identifikátory. Každý zákazník přístupná pouze data shromážděná z vlastní organizace a obecná data, která poskytuje Microsoft.

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Je nutné možnost vyberte, kam chcete uložit Moje data? 

Ne. Je vytvořena instance vaší služby Azure ATP, je automaticky uložené v datovém centru země nejblíže zeměpisné umístění vašeho tenanta AAD. Azure data ochrany ATP v programu nelze přesunout, po vytvoření instance služby Azure ATP do různých datových center.                

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Jak Microsoft zabránit aktivity zlými úmysly a zneužití vysoká oprávnění rolí? 

Microsoft vývojářům a správcům, podle návrhu, mít dostatečná oprávnění k provedení jejich přiřazené povinnosti, aby provoz a umožněte vývoj služby. Microsoft nasazuje kombinací preventivní detektiv a reaktivní ovládacích prvků, včetně následujících mechanismů a pomáhá chránit před neoprávněným pro vývojáře a/nebo aktivita správy: 

-   Ovládací prvek úzkou přístup k citlivým datům 
-   Kombinací ovládacích prvků, které může to výrazně zvýšit nezávislé odhalování škodlivých aktivit 
-   Více úrovní monitorování, protokolování a vytváření sestav 

Kromě toho Microsoft provádí kontroly podstupovaly ověřování u správců osobní prověrku určité operace a omezuje přístup k aplikacím, systémy a síťovou infrastrukturu výkonový zisk úroveň ověřování probíhá na pozadí. Operace pracovníky postupujte podle formální proces, když jsou potřeba pro přístup k účtu zákazníka nebo související informace v plnění jejich úkolů. 

## <a name="deployment"></a>Nasazení

### <a name="how-many-azure-atp-sensors-do-i-need"></a>Počet senzorů ochrany ATP v programu Azure budu potřebovat?

Každý řadič domény v prostředí měly být pokryté komponentami ochrany ATP v programu nebo samostatného senzoru. Další informace najdete v tématu [velikosti senzoru služby Azure ATP](atp-capacity-planning.md#sizing). 

### <a name="does-azure-atp-work-with-encrypted-traffic"></a>Služba Ochrana ATP v programu Azure funguje při šifrovaném provozu?
Síťové protokoly s šifrovaný provoz (například LDAPS nebo IPSEC) nejsou dešifrovat, ale jsou analyzovány senzory.

### <a name="does-azure-atp-work-with-kerberos-armoring"></a>Služba Ochrana ATP v programu Azure funguje s obranou protokolu Kerberos?
Povolení obrany protokolu Kerberos, označované také jako FAST Flexible Authentication Secure Tunneling (), je podporována ochrana ATP v programu Azure, s výjimkou pass typu over-pass-the hash detekce, což nefunguje s obranou protokolu Kerberos.

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Jak můžu monitorovat virtuální řadič domény pomocí ochrany ATP v programu Azure?
Většina virtuálních řadičů domény dají pokrýt komponentami senzoru služby Azure ATP, chcete-li zjistit, zda služby Azure ATP senzor je vhodné pro vaše prostředí [plánování kapacity ochrany ATP v programu Azure](atp-capacity-planning.md).

Pokud se virtuální řadič domény nedá pokrýt komponentou senzoru služby Azure ATP, jak je popsáno v může mít buď virtuální nebo fyzická ochrana ATP v programu Azure samostatný senzor [konfigurace zrcadlení portů](configure-port-mirroring.md).  <br />Nejjednodušší je mít virtuální samostatný senzor ochrany ATP v programu Azure na každém hostiteli, kde existují virtuální řadič domény.<br />Pokud virtuální řadiče domény přesunují mezi hostiteli, je třeba provést jednu z následujících kroků:

-   Pokud se virtuální řadič domény přesune na jiného hostitele, předem nakonfigurujte samostatný senzor ochrany ATP v programu Azure v tomto hostiteli příjem provozu z nedávno přesunutého virtuálního řadiče domény.
-   Ujistěte se, že jste přidružili virtuální samostatný senzor ochrany ATP v programu Azure pomocí virtuálního řadiče domény tak, že pokud se přesune, samostatného senzoru služby Azure ATP se přesune s ním.
-   Některé virtuální přepínače mohou odesílat provoz mezi hostiteli.

### <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Jak nakonfigurovat senzorů ochrany ATP v programu Azure komunikovat s cloudovou službou ochrany ATP v programu Azure, pokud proxy server?

Pro řadiče domény ke komunikaci s cloudovou službou, je nutné otevřít: *. atp.azure.com port 443 v brány firewall a proxy. Pokyny, jak to udělat, najdete v části [konfigurace proxy serveru nebo brány firewall k umožnění komunikace s Azure ATP senzorů](configure-proxy.md).

### <a name="can-azure-atp-monitored-domain-controllers-be-virtualized-on-your-iaas-solution"></a>Můžete služby Azure ATP monitoruje řadiče domény virtualizované ve vašem řešení IaaS?
Senzoru služby Azure ATP Ano, můžete použít k monitorování řadičů domény, které jsou v libovolném řešení IaaS.

### <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Ochrana ATP v programu Azure může podporovat víc domén a doménových struktur?
Azure Advanced Threat Protection podporuje prostředí s více doménami a několik doménových struktur. Další informace a důvěryhodnost požadavky najdete v tématu [podporu více doménovými strukturami](atp-multi-forest.md).

### <a name="can-you-see-the-overall-health-of-the-deployment"></a>Dá se zjistit celkový stav nasazení?
Ano, můžete zobrazit celkový stav nasazení a také konkrétní problémy související s konfigurací, připojení atd. kde se zobrazí výstraha při jejich výskytu pomocí upozornění na stav ochrany ATP v programu Azure.

## <a name="operation"></a>Operace

### <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Jaký druh integrace ochrany ATP v programu Azure má se systémy Siem?
Ochrana ATP v programu Azure lze nakonfigurovat na odesílání výstrahy Syslog na libovolný server SIEM pomocí formátu CEF pro výstrahy týkající se stavu a když se detekuje výstraha zabezpečení. Zobrazit [referenční informace k protokolům SIEM](cef-format-sa.md) Další informace.

### <a name="why-are-certain-accounts-considered-sensitive"></a>Proč se některé účty považují za citlivé?
To se stane, když je účet členem skupiny, které jsou určené jako citlivé (například: "Skupina domain Admins").

Pokud chcete pochopit, proč je účet citlivý, můžete zkontrolovat jeho členství ve skupinách a zjistit, do kterých citlivých skupin patří (skupina, do které patří, může být citlivá také kvůli jiné skupině, takže je potřeba celý proces opakovat tak dlouho, až zjistíte citlivou skupinu nejvyšší úrovně). Můžete také ručně [jako citlivé účty značka](sensitive-accounts.md).

### <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Je potřeba psát vlastní pravidla a určovat prahové nebo základní hodnoty?
S Azure Advanced Threat Protection není nutné k vytváření pravidel ani prahových nebo standardní hodnoty a jejich následné vyladění. Ochrana ATP v programu Azure analyzuje chování uživatelů, zařízení a prostředky, jakož i jejich vzájemných vztazích a dokáže detekovat podezřelé aktivity a známé útoky se rychle. Tři týdny po nasazení služby Azure ATP začne detekovat behaviorálně podezřelé aktivity. Na druhé straně ochrany ATP v programu Azure začne okamžitě po nasazení detekuje známé útoky se zlými úmysly a problémy se zabezpečením.

### <a name="which-traffic-does-azure-atp-generate-in-the-network-from-domain-controllers-and-why"></a>Jaký provoz služby Azure ATP generuje v síti z řadičů domény a proč? 

Ochrana ATP v programu Azure generuje provoz z řadičů domény do počítačů v organizaci v jednom ze tří scénářů:
1. **Překlad síťových názvů**<br>
   Ochrana ATP v programu Azure zaznamená provoz a události, učení a profilování uživatelé a počítače aktivity v síti. Další a Profilovat aktivity podle počítače v organizaci, ochrana ATP v programu Azure potřebuje k překladu IP adres na účty počítačů. Přeložit IP adresy počítači názvy ochrany ATP v programu Azure senzorů požádat o IP adresu pro název počítače *za* IP adresu. <br>
 
   Požadavky přicházejí jedním ze čtyř způsobů: 
    - NTLM přes RPC (port TCP 135)
    - NetBIOS (port UDP 137)
    - Protokol RDP (portu TCP 3389)
    - Zadat dotaz na server DNS pomocí zpětného vyhledávání DNS IP adresy (UDP 53)
    
    Po přijetí název počítače, služby Azure ATP snímače různé podrobnosti ve službě Active Directory, jestli je objekt korelační počítače se stejným názvem počítače. Pokud se najde shoda, lze vytvářet spojení mezi IP adresu a objekt odpovídající počítače.
2. **Cesty taktiky Lateral Movement (LMP)**<br>
    Ochrana ATP v programu Azure k sestavení potenciální LMPs pro citlivé uživatele, vyžaduje informace o místní správci na počítačích. V tomto scénáři používá senzoru služby Azure ATP SAM-R (TCP 445) k dotazování IP adresu podle síťového provozu, aby bylo možné zjistit místní správci počítači. Další informace o ochrany ATP v programu Azure a SAM-R, najdete v článku [konfigurace SAM-R požadovaná oprávnění](install-atp-step8-samr.md). 

3. **Dotazování služby Active Directory pomocí protokolu LDAP** pro entitu dat<br>
    Azure ATP senzorů dotaz na řadič domény z domény, kam patří entity. Může být snímač stejný nebo jiný řadič domény v této doméně. 

|Protocol (Protokol)|Služba|Port|Source| Direction|
|---------|---------|---------|---------|--------|
|LDAP|TCP a UDP|389|Řadiče domény|Odchozí|
|Zabezpečený LDAP (LDAPS)|TCP|636|Řadiče domény|Odchozí|
|LDAP pro globální katalog|TCP|3268|Řadiče domény|Odchozí|
|LDAPS pro globální katalog|TCP|3269|Řadiče domény|Odchozí|
|

### <a name="why-dont-activities-always-show-both-the-source-user-and-computer"></a>Proč aktivity vždy nezobrazovat uživateli zdroj i počítače?

Ochrana ATP v programu Azure zachycuje prostřednictvím mnoha různých protokolů aktivit. V některých případech se služby Azure ATP neobdrží data zdrojový uživatel v provozu. Ochrana ATP v programu Azure se pokusí porovnat relace uživatele na aktivitu, a když je tento pokus úspěšný, zobrazí se zdrojový uživatel aktivity. Když se nezdaří pokus o korelace uživatele, zobrazí se zdrojový počítač. 

## <a name="troubleshooting"></a>Řešení potíží

### <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>Co mám dělat, když ochrana ATP v programu Azure nebo samostatný senzor nespustí?
Podívejte se na poslední chyba aktuální chybě [protokolu](troubleshooting-atp-using-logs.md) (kde služby Azure ATP je nainstalována ve složce "Protokoly").


## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md)
- [Odstraňování potíží](troubleshooting-atp-known-issues.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
