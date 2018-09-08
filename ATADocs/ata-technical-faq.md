---
title: Nejčastější dotazy k Advanced Threat Analytics | Dokumentace Microsoftu
description: Seznam nejčastějších dotazů týkajících se ATA a související odpovědi
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/6/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c28783170764c117a07fa19946c83638f24dc1a6
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166489"
---
*Platí pro: Advanced Threat Analytics verze 1.9*

# <a name="ata-frequently-asked-questions"></a>Nejčastější dotazy k ATA
Tento článek obsahuje seznam nejčastějších dotazů týkajících se ATA a poskytuje podrobné informace a odpovědi.


## <a name="where-can-i-get-a-license-for-advanced-threat-analytics-ata"></a>Kde získám licenci na Advanced Threat Analytics (ATA)?

Pokud máte aktivní smlouvu Enterprise, můžete si tento software stáhnout z centra multilicencí Microsoftu (VLSC).

Pokud jste licenci na Microsoft Enterprise Mobility + Security (EMS) pořídili přímo přes portál Office 365 nebo prostřednictvím licenčního modelu partnera cloudových řešení (CSP) a nemáte k ATA přístup přes centrum multilicencí Microsoftu (VLSC), požádejte zákaznickou podporu Microsoftu o zpracování aktivace řešení ATA (Advanced Threat Analytics).

## <a name="what-should-i-do-if-the-ata-gateway-wont-start"></a>Co mám dělat, když se ATA Gateway nespustí?
Podívejte se na poslední chybu v aktuálním protokolu chyb (ve složce Logs tam, je software ATA nainstalovaný).

## <a name="how-can-i-test-ata"></a>Jak se dá ATA otestovat?
Pomocí jedné z následujících akcí můžete simulovat podezřelé aktivity a provést tak kompletní test:

1.  Rekognoskace DNS s využitím Nslookup.exe
2.  Vzdálené spuštění s využitím psexec.exe


To je potřeba spustit vzdáleně nikoli z komponenty ATA Gateway, ale nad monitorovaným řadičem domény.

## <a name="which-ata-build-corresponds-to-each-version"></a>Které sestavení ATA odpovídá jednotlivým verzím?

Informace o upgradu verzi, naleznete v tématu [Cesta upgradu ATA](upgrade-path.md).

## <a name="what-version-should-i-use-to-upgrade-my-current-ata-deployment-to-the-latest-version"></a>Jakou verzi mám použít k upgradu aktuálního nasazení ATA na nejnovější verzi?

Tabulka upgradu verzí ATA, naleznete v tématu [Cesta upgradu ATA](upgrade-path.md).


## <a name="how-does-the-ata-center-update-its-latest-signatures"></a>Jak komponenty ATA Center aktualizovat své nejnovější podpisy?

Při instalaci nové verze v komponentě ATA Center je vylepšená mechanismus detekce ATA. System Center můžete upgradovat pomocí webu Microsoft Update (MU) nebo ručně stáhněte si novou verzi ze služby Stažení softwaru nebo svazek licence webu.

## <a name="how-do-i-verify-windows-event-forwarding"></a>Jak ověřím předávání událostí systému Windows?
Do souboru můžete vložit tento kód a pak jej z příkazového řádku v adresáři: **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** můžete spustit následovně:

mongo.exe název souboru ATA

        db.getCollectionNames().forEach(function(collection) {
        if (collection.substring(0,10)=="NtlmEvent_") {
                if (db[collection].count() > 0) {
                                  print ("Found "+db[collection].count()+" NTLM events") 
                                }
                }
        });

## <a name="does-ata-work-with-encrypted-traffic"></a>Funguje ATA při šifrovaném provozu?
ATA se spoléhá na analýzu více síťových protokolů, událostí shromážděných ze systému SIEM nebo prostřednictvím předávání událostí Windows. Detekce založené na síťové protokoly s šifrovaný provoz (například LDAPS nebo IPSEC) nebude analyzováno.


## <a name="does-ata-work-with-kerberos-armoring"></a>Funguje ATA s obranou protokolu Kerberos?
ATA podporuje povolení obrany protokolu Kerberos, která se také označuje jako architektura FAST (Flexible Authentication Secure Tunneling). Výjimkou je detekce typu over-pass-the-hash, která nebude fungovat.

## <a name="how-many-ata-gateways-do-i-need"></a>Kolik komponent ATA Gateways budu potřebovat?

Počet komponent ATA Gateway závisí na rozvržení sítě, objemu paketů a objemu událostí, které konzola ATA zaznamená. Pokud chcete určit přesný počet, přejděte do části [Velikosti pro ATA Lightweight Gateway](ata-capacity-planning.md#ata-lightweight-gateway-sizing). 

## <a name="how-much-storage-do-i-need-for-ata"></a>Jak velké úložiště budu pro ATA potřebovat?
Pro jeden plný den s průměrem 1000 paketů/s budete potřebovat 0,3 GB úložiště.<br /><br />Další informace o určení velikosti pro ATA Center najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md).


## <a name="why-are-certain-accounts-considered-sensitive"></a>Proč se některé účty považují za citlivé?
Dojde k tomu, když je účet členem konkrétních skupin, které označujeme jako citlivé (například Domain Admins).

Pokud chcete pochopit, proč je účet citlivý, můžete zkontrolovat jeho členství ve skupinách a zjistit, do kterých citlivých skupin patří (skupina, do které patří, může být citlivá také kvůli jiné skupině, takže je potřeba celý proces opakovat tak dlouho, až zjistíte citlivou skupinu nejvyšší úrovně). 

Kromě toho můžete ručně označit uživatele, skupiny nebo počítače jako citlivé. Další informace najdete v tématu [označit citlivých účtů](tag-sensitive-accounts.md).

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-ata"></a>Jak můžu ATA využít k monitorování virtuálního řadiče domény?
Většina virtuálních řadičů domény se dá pokrýt komponentami ATA Lightweight Gateway. K určení, jestli je komponenta ATA Lightweight Gateway pro vaše prostředí vhodná, použijte informace v tématu [Plánování kapacity ATA](ata-capacity-planning.md).

Pokud se virtuální řadič domény nedá pokrýt komponentou ATA Lightweight Gateway, jak je popsáno v může mít buď virtuálním nebo fyzickém ATA Gateway [konfigurace zrcadlení portů](configure-port-mirroring.md).  <br />Nejjednodušší je mít virtuální ATA Gateway na každém hostiteli, kde existují virtuální řadiče domény.<br />Pokud virtuální řadiče domény přesunují mezi hostiteli, je třeba provést jednu z následujících kroků:

-   Pokud se virtuální řadič domény přesune na jiného hostitele, pro ATA Gateway na tomto hostiteli předem nakonfigurujte příjem provozu z nedávno přesunutého virtuálního řadiče domény.
-   Zkontrolujte, že jste virtuální ATA Gateway přidružili k virtuálnímu řadiči domény, takže pokud se přesune, ATA Gateway se přesune s ním.
-   Některé virtuální přepínače mohou odesílat provoz mezi hostiteli.

## <a name="how-do-i-back-up-ata"></a>Jak se ATA dá zálohovat?

Přečtěte si článek [Zotavení po havárii ATA](disaster-recovery.md).



## <a name="what-can-ata-detect"></a>Co ATA dokáže rozpoznat?

ATA rozpoznává známé nebezpečné útoky a techniky, problémy zabezpečení a rizika.
Úplný seznam detekcí ATA najdete v tématu [Jaké detekce ATA provádí?](ata-threats.md).

## <a name="what-kind-of-storage-do-i-need-for-ata"></a>Jaký druh úložiště budu pro ATA potřebovat?
Doporučujeme rychlé úložiště (disky s 7200 ot. / min se nedoporučuje) s diskem s nízkou latencí (méně než 10 ms). Konfigurace RAID vy měla podporovat velkou zátěž při zápisu (nikoli RAID-5/6 nebo odvozené konfigurace).

## <a name="how-many-nics-does-the-ata-gateway-require"></a>Kolik síťových karet ATA Gateway vyžaduje?
ATA Gateway vyžaduje minimálně dva síťové adaptéry:<br>1. Síťovou kartu pro připojení k interní síti a komponentě ATA Center<br>2. Síťové rozhraní, který se používá k zachycení síťového provozu na řadiči domény prostřednictvím zrcadlení portů.<br>* To neplatí pro komponentu ATA Lightweight Gateway, která nativně využívá všechny síťové adaptéry využívané řadičem domény.

## <a name="what-kind-of-integration-does-ata-have-with-siems"></a>Jaký druh integrace se systémy SIEM ATA využívá?
Se systémy SIEM ATA využívá obousměrnou integraci:

1. ATA lze nakonfigurovat odesílání výstrahy Syslog na libovolný server SIEM pomocí formátu CEF, když zjistí podezřelou aktivitu.
2. ATA lze nakonfigurovat tak, aby se z těchto [serverů SIEM](install-ata-step6.md) přijímaly zprávy Syslog pro události Windows.

## <a name="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Může ATA monitorovat řadiče domény virtualizované ve vašem řešení IaaS?
Ano, ATA Lightweight Gateway se dá použít k monitorování řadičů domény, které jsou v libovolném řešení IaaS.

## <a name="is-this-an-on-premises-or-in-cloud-offering"></a>Jedná se o místní nebo cloudovou nabídku?
Microsoft Advanced Threat Analytics je místní produkt.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Bude součástí Azure Active Directory nebo místní služby Active Directory?
Toto řešení se v současnosti nabízí samostatně. Není součástí Azure Active Directory ani místní služby Active Directory.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Je potřeba psát vlastní pravidla a určovat prahové nebo základní hodnoty?
Microsoft Advanced Threat Analytics nevyžaduje vytváření pravidel ani prahových nebo základních hodnot a jejich následné vyladění. ATA analyzuje chování uživatelů, zařízení a prostředků a také jejich vzájemné vztahy. Dokáže rychle detekovat podezřelé aktivity a známé útoky. Tři týdny po nasazení ATA začne detekovat behaviorálně podezřelé aktivity. Naproti tomu známé útoky se zlými úmysly a problémy zabezpečení začne ATA detekovat bezprostředně po nasazení.

## <a name="if-you-are-already-breached-can-microsoft-advanced-threat-analytics-identify-abnormal-behavior"></a>Pokud jsou již nedodržení, Microsoft Advanced Threat Analytics identifikovat neobvyklé chování
Ano, i když se ATA nainstaluje až po porušení zabezpečení, dokáže rozpoznat podezřelé aktivity hackerů. ATA nejenom zkoumá chování uživatelů, ale současně se taky dívá na ostatní uživatele v organizační mapě zabezpečení. Pokud je chování útočníka během počáteční analýzy nestandardní, je identifikovaný jako „outlier“ a ATA bude toto nestandardní chování dál hlásit. ATA může dál detekovat podezřelou aktivitu, pokud se hacker pokusí ukrást přihlašovací údaje jiných uživatelů, třeba Pass-the-Ticket, nebo se pokusí provést vzdálené spuštění na jednom z řadičů domény.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>Využívají se přitom jenom přenosy služby Active Directory?
Kromě analýzy provozu služby Active Directory pomocí technologie hloubkové kontroly paketů ATA taky shromažďuje relevantní události ze služby SIEM (Security Information and Event Management) a na základě informací získaných ze služby Active Directory Domain Services vytváří profily entit. Pokud organizace nakonfiguruje předávání Protokolu událostí systému Windows, může ATA taky shromažďovat události z protokolů událostí.

## <a name="what-is-port-mirroring"></a>Co je zrcadlení portů?
Zrcadlení portů, které se taky označuje jako SPAN (Switched Port Analyzer), je metoda monitorování síťových aktivit. Pokud je zrcadlení portů povolené, přepínač odešle kopii všech síťových paketů zjištěných na jednom portu (nebo v celé síti VLAN) na jiný port, kde se tyto pakety dají analyzovat.

## <a name="does-ata-monitor-only-domain-joined-devices"></a>Monitoruje ATA jenom zařízení připojená k doméně?
Ne. ATA monitoruje všechna zařízení v síti, která zpracovávají požadavky ověřování a autorizace pro službu Active Directory, včetně zařízení s jiným systémem než Windows a mobilních zařízení.

## <a name="does-ata-monitor-computer-accounts-as-well-as-user-accounts"></a>Monitoruje ATA jak účty počítačů, tak uživatelské účty?
Ano. Protože počítače účty (stejně jako ostatní entity) lze použít k provádění škodlivých aktivit, ATA monitoruje chování všech účtů počítačů a všechny ostatní entity v příslušném prostředí.

## <a name="can-ata-support-multi-domain-and-multi-forest"></a>Může ATA podporovat několik domén a doménových struktur?
Microsoft Advanced Threat Analytics podporuje prostředí s více doménami v rámci stejné doménové struktury. Více doménových struktur vyžaduje nasazení ATA pro každou doménovou strukturu.

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Dá se zjistit celkový stav nasazení?
Ano, můžete zobrazit celkový stav nasazení a také konkrétní problémy související s konfigurací, připojení atd. kde se zobrazí výstraha při jejich výskytu.


## <a name="see-also"></a>Viz také
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

