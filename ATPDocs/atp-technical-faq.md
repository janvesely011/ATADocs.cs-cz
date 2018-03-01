---
title: "Nejčastější dotazy k Azure Advanced Threat Protection | Microsoft Docs"
description: "Obsahuje seznam nejčastějších dotazů týkajících se Azure ATP a související odpovědi"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/27/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6a6a34b9a2aae0e507fe18872a31368cf3f3e9d0
ms.sourcegitcommit: 21d8f9abf909fc5f0e0da03cd100fa8fb950baa4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/27/2018
---
*Platí pro: Azure Advanced Threat Protection*

# <a name="azure-atp-frequently-asked-questions"></a>Nejčastější dotazy k Azure ATP
Tento článek obsahuje seznam nejčastějších dotazů týkajících Azure ATP a poskytuje podrobné informace a odpovědi.


## <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>Kde lze získat licenci pro Azure Advanced Threat Protection (ATP)?

Pokud jste získali licenci pro Enterprise Mobility + Security 5 (EMS E5) přímo prostřednictvím portálu služeb Office 365 nebo prostřednictvím licenčním modelu cloudové řešení partnera (CSP) a nemáte přístup k Azure ATP prostřednictvím webu Microsoft Volume Licensing Center (VLSC), obraťte se na Zákaznická podpora Microsoftu získat proces aktivace Azure Advanced Threat Protection (ATP).

## <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>Co je třeba udělat, pokud se nespustí senzor Azure ATP nebo samostatné senzor?
Podívejte se na poslední chybu v aktuálním protokolu chyb (kde ATP Azure je nainstalován ve složce "Protokoly").

## <a name="how-can-i-test-azure-atp"></a>Jak můžete otestovat Azure ATP?
Spuštěním následujícího příkazu můžete simulovat podezřelé aktivity jako test začátku do konce:

-  Rekognoskace DNS s využitím Nslookup.exe


To je potřeba spustit vzdáleně nikoli z senzoru samostatné Azure ATP ale nad monitorovaným řadičem domény.


## <a name="does-azure-atp-work-with-encrypted-traffic"></a>Pracuje Azure ATP při šifrovaném provozu?
Azure ATP spoléhá na analýze více síťových protokolů, jakož i událostí shromážděných ze systému SIEM nebo pomocí předávání událostí systému Windows. Detekce podle síťové protokoly s šifrovaný provoz (Příklad: LDAPS a protokolu IPSEC) nejsou analyzovány.


## <a name="does-azure-atp-work-with-kerberos-armoring"></a>Funguje s obranou protokolu Kerberos Azure ATP?
Povolení obrany protokolu Kerberos, také známé jako FAST Flexible Authentication Secure Tunneling (), je podporována ATP, s výjimkou over-pass detekci hash, která nefunguje s obranou protokolu Kerberos.

## <a name="how-many-azure-atp-sensors-do-i-need"></a>Kolik senzorů Azure ATP potřebuji?

Každý řadič domény v prostředí měly být pokryté komponentami ATP senzoru nebo samostatné senzor. Další informace najdete v tématu [Azure ATP senzor Změna velikosti](atp-capacity-planning.md#sizing). 


## <a name="why-are-certain-accounts-considered-sensitive"></a>Proč se některé účty považují za citlivé?
To se stane, když je účet členem skupiny, které jsou určeny jako velká a malá písmena (například: "Domain Admins").

Pokud chcete pochopit, proč je účet citlivý, můžete zkontrolovat jeho členství ve skupinách a zjistit, do kterých citlivých skupin patří (skupina, do které patří, může být citlivá také kvůli jiné skupině, takže je potřeba celý proces opakovat tak dlouho, až zjistíte citlivou skupinu nejvyšší úrovně). Můžete také [značky jako citlivé účty ručně](sensitive-accounts.md).

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>Jak můžu monitorování virtuálního řadiče domény pomocí Azure ATP?
Většina virtuálních řadičů domény se dá pokrýt komponentami Azure ATP senzoru, chcete-li zjistit, zda Azure ATP senzor je vhodné pro vaše prostředí, najdete v části [plánování kapacity ATP Azure](atp-capacity-planning.md).

Pokud se virtuální řadič domény nedá pokrýt komponentou senzoru Azure ATP, jak je popsáno v může mít buď virtuální nebo fyzická Azure ATP samostatné senzoru [konfigurace zrcadlení portů](configure-port-mirroring.md).  <br />Nejjednodušší je mít virtuální senzor samostatné Azure ATP na každém hostiteli, kde existují virtuální řadiče domény.<br />Pokud virtuální řadiče domény přesunují mezi hostiteli, je třeba provést jednu z následujících kroků:

-   Pokud se virtuální řadič domény přesune na jiného hostitele, předem nakonfigurujte senzor samostatné Azure ATP na tomto hostiteli příjem provozu z nedávno přesunutého virtuálního řadiče domény.
-   Ujistěte se, že jste přidružili virtuální senzoru samostatné Azure ATP s virtuálního řadiče domény tak, že pokud se přesune, senzoru samostatné Azure ATP přesune s ním.
-   Některé virtuální přepínače mohou odesílat provoz mezi hostiteli.


## <a name="what-can-azure-atp-detect"></a>Co dokáže rozpoznat Azure ATP?

Azure ATP detekuje známé nebezpečné útoky a techniky, problémy zabezpečení a rizika.
Úplný seznam detekce Azure ATP najdete v tématu [jaké detekce Azure ATP provádět?](suspicious-activity-guide.md).

## <a name="how-many-nics-does-the-azure-atp-standalone-sensor-require"></a>Kolik síťových karet senzoru samostatné Azure ATP vyžaduje?
Senzor samostatné Azure ATP vyžaduje minimálně dva síťové adaptéry:<br>1. Síťový adaptér pro připojení k interní síti a cloudové služby Azure ATP<br>2. Síťovou kartu, která se používá k zachycení síťového provozu řadiče domény prostřednictvím zrcadlení portů.<br>* To neplatí pro senzor Azure ATP, která nativně využívá všechny síťové adaptéry, které řadič domény používá.

## <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Se systémy Siem jaký druh integrace má Azure ATP?
Azure ATP má obousměrnou integraci se systémy Siem následujícím způsobem:

1. Azure ATP může být nakonfigurován pro odesílání výstrahy Syslog na libovolný server SIEM s využitím formátu CEF, pro stavu výstrahy, když se detekuje podezřelá aktivita.
2. Azure ATP dá nakonfigurovat příjem zpráv pro události systému Windows z [těchto systémů Siem](configure-event-collection.md).

## <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>Konfigurování snímače Azure ATP ke komunikaci s Azure ATP cloudové služby, pokud proxy server

Pro řadiče domény ke komunikaci s cloudovou službou, je nutné otevřít: *. atp.azure.com port 443 brány firewall nebo proxy serveru. Pokyny o tom, jak to udělat najdete v tématu [konfigurace proxy serveru nebo brány firewall tak, aby komunikace snímači Azure ATP](configure-proxy.md).
 

## <a name="can-azure-atp-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Můžete monitorovat Azure ATP ve vašem řešení IaaS virtualizovaného řadiče domény?
Ano, můžete Azure ATP senzoru k monitorování řadičů domény, které jsou v libovolném řešení IaaS.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Bude součástí Azure Active Directory nebo místní služby Active Directory?
Toto řešení je aktuálně samostatné nabídky. Není součástí Azure Active Directory, nebo místní služby Active Directory.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Je potřeba psát vlastní pravidla a určovat prahové nebo základní hodnoty?
S Azure Advanced Threat Protection je potřeba vytvořit pravidla, prahové hodnoty nebo směrné plány a jejich následné vyladění. Analyzuje chování uživatelů, zařízení a prostředky Azure ATP – i jejich vzájemných vztazích – dokáže rychle detekovat podezřelé aktivity a známé útoky rychlé. Tři týdny po nasazení Azure ATP začne detekovat behaviorálně podezřelé aktivity. Na druhé straně Azure ATP se spustí hned po nasazení detekuje známé útoky se zlými úmysly a problémy se zabezpečením.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>Využívají se přitom jenom přenosy služby Active Directory?
Kromě analýzy provozu služby Active Directory pomocí technologie hloubkové kontroly paketů, Azure ATP taky shromažďuje relevantní události ze Security Information and Event Management (SIEM) a vytváří profily entit na základě informací ze služby Active Directory Domain Services. Pokud používáte Azure ATP senzoru, extrahuje tyto události automaticky. Předávání událostí systému Windows můžete použít k odesílání těchto událostí na samostatné senzoru Azure ATP. Azure ATP také podporuje přijímající monitorování účtů protokolu RADIUS VPN protokoly od různých dodavatelů (Microsoft, Cisco, F5 a kontrolního bodu).

## <a name="what-is-port-mirroring"></a>Co je zrcadlení portů?
Zrcadlení portů, které se taky označuje jako SPAN (Switched Port Analyzer), je metoda monitorování síťových aktivit. Pokud je zrcadlení portů povolené, přepínač odešle kopii všech síťových paketů zjištěných na jednom portu (nebo v celé síti VLAN) na jiný port, kde se tyto pakety dají analyzovat.

## <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Azure ATP monitorovat pouze zařízení připojená k doméně?
Ne. Azure ATP monitoruje všechna zařízení v síti, která zpracovávají požadavky ověřování a autorizace pro službu Active Directory, včetně jiný systém než Windows a mobilní zařízení.

## <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Azure ATP monitorování účtů počítačů a také uživatelské účty?
Ano. Vzhledem k tomu, že počítač účty (stejně jako ostatní entity) slouží k provádění škodlivých aktivit, Azure ATP monitoruje chování všech účtů počítačů a všechny ostatní entity v prostředí.

## <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Azure ATP může podporovat několik domén a doménových struktur?
Azure Advanced Threat Protection podporuje prostředí s více doménami v rámci stejné hranice doménové struktury. Několik doménových struktur vyžadují pracovní prostor služby Azure ATP pro jednotlivé doménové struktury.

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Dá se zjistit celkový stav nasazení?
Ano, můžete zobrazit celkový stav nasazení a taky konkrétní problémy související s konfigurací, možnostmi připojení atd se zobrazí výstraha, když k nim dojde.

## <a name="what-data-does-azure-atp-collect"></a>Jaká data Azure ATP shromáždit? 
Azure ATP shromažďuje a ukládá informace z vašeho nakonfigurované servery (řadiče domény, členské servery atd.) v databázi specifické pro službu pro správu, sledování a vytváření sestav pro účely. Informace shromážděné zahrnuje síťový provoz do a z řadiče domény (například ověřování protokolem Kerberos, ověřování NTLM, dotazy DNS), protokoly zabezpečení (například události zabezpečení systému Windows), informace služby Active Directory (struktura, podsítě, weby), a entity informace (například názvy, e-mailových adres a telefonních čísel). 

Společnost Microsoft používá tato data: 

-   Aktivně Identifikujte indikátory útoku (IOAs) ve vaší organizaci 
-   Generovat výstrahy, pokud byl zjištěn možný útok 
-   Zadejte vaše operace zabezpečení se zobrazením do entity související threat signály z vaší sítě umožňuje prozkoumat a prozkoumejte přítomnost bezpečnostní hrozby v síti. 

Microsoft, ne já data pro inzerování nebo k jiným účelům než poskytování služby. 

## <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>Jsou možnost vyberte, kam chcete uložit svá data? 

Při vytváření pracovního prostoru Azure ATP, které můžete ukládat data, můžete k ukládání dat v datových centrech Microsoft Azure v USA a Evropě. Po nakonfigurování nelze změnit umístění, kde jsou uložené vaše data. Microsoft nebude přenést data ze zadaného umístění. 

## <a name="is-my-data-isolated-from-other-customer-data"></a>Jsou má data izolované od ostatních zákazníků dat? 

Ano, vaše data jsou izolované prostřednictvím ověřování přístupu k a logické oddělení podle identifikátor zákazníka. Každý zákazník může přístup jenom k data shromážděná z vlastní organizace a obecná data, která společnost Microsoft poskytuje. 

## <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Jak Microsoft zabraňuje zevnitř aktivity a zneužití vysoká oprávnění rolí? 

Vývojáři a správci, návrh mít dostatečná oprávnění k provádění svých povinností pro provoz a momentální službu. Microsoft nasadí kombinace prevence, detektiv a reaktivní ovládací prvky, včetně následujících mechanismů, kvůli ochraně před neoprávněným vývojáře nebo aktivita správy: 

-   Ovládací prvek úzkou přístup k citlivým datům 
-   Kombinace ovládacích prvků, které výrazně zvýšit nezávislé odhalování škodlivých aktivit 
-   Více úrovní sledování, protokolování a vytváření sestav 

Kromě toho společnost Microsoft provádí ověřovací kontroly na určité operace pracovníky a omezuje přístup k aplikacím, systémy a síťové infrastruktury v poměru k úroveň ověřování pozadí. Operace pracovníky podle formální proces vyžádání přístup k účtu zákazníka nebo související informace ve výkonu jejich funkce. 

## <a name="see-also"></a>Viz také
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Plánování kapacity v Azure ATP](atp-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
