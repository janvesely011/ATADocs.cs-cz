---
title: "Nejčastější dotazy k Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Seznam nejčastějších dotazů týkajících se ATA a související odpovědi"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 02/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 95513a7170df28529c85ccc3c8d65446c4770bbc
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Platí pro: Advanced Threat Analytics verze 1.7*

# <a name="ata-frequently-asked-questions"></a>Nejčastější dotazy k ATA
Tento článek obsahuje seznam nejčastějších dotazů týkajících se ATA a poskytuje podrobné informace a odpovědi.


## <a name="what-should-i-do-if-the-ata-gateway-wont-start"></a>Co mám dělat, když se ATA Gateway nespustí?
Podívejte se na poslední chybu v aktuálním protokolu chyb (ve složce Logs tam, je software ATA nainstalovaný).

## <a name="how-can-i-test-ata"></a>Jak se dá ATA otestovat?
Pomocí jedné z následujících akcí můžete simulovat podezřelé aktivity a provést tak kompletní test:

1.  Rekognoskace DNS s využitím Nslookup.exe
2.  Vzdálené spuštění s využitím psexec.exe


To je potřeba spustit vzdáleně nikoli z komponenty ATA Gateway, ale nad monitorovaným řadičem domény.

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
ATA se spoléhá na analýzu řady síťových protokolů a událostí shromažďovaných ze systému SIEM nebo prostřednictvím předávání událostí systému Windows, i když se tedy nebude analyzovat šifrovaný provoz (například LDAPS nebo IPSEC ESP) ATA fungovat nepřestane a na většinu detekcí to nebude mít vliv

## <a name="does-ata-work-with-kerberos-armoring"></a>Funguje ATA s obranou protokolu Kerberos?
ATA podporuje povolení obrany protokolu Kerberos, která se také označuje jako architektura FAST (Flexible Authentication Secure Tunneling). Výjimkou je detekce typu over-pass-the-hash, která nebude fungovat.

## <a name="how-many-ata-gateways-do-i-need"></a>Kolik komponent ATA Gateways budu potřebovat?

Počet komponent ATA Gateway závisí na rozvržení sítě, objemu paketů a objemu událostí, které konzola ATA zaznamená. Pokud chcete určit přesný počet, přejděte do části [Velikosti pro ATA Lightweight Gateway](/advanced-threat-analytics/plan-design/ata-capacity-planning#ata-lightweight-gateway-sizing). 

## <a name="how-much-storage-do-i-need-for-ata"></a>Jak velké úložiště budu pro ATA potřebovat?
Pro jeden plný den s průměrem 1000 paketů/s budete potřebovat 0,3 GB úložiště.<br /><br />Další informace o určení velikosti pro ATA Center najdete v tématu [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).


## <a name="why-are-certain-accounts-considered-sensitive"></a>Proč se některé účty považují za citlivé?
Dojde k tomu, když je účet členem konkrétních skupin, které označujeme jako citlivé (například Domain Admins).

Pokud chcete pochopit, proč je účet citlivý, můžete zkontrolovat jeho členství ve skupinách a zjistit, do kterých citlivých skupin patří (skupina, do které patří, může být citlivá také kvůli jiné skupině, takže je potřeba celý proces opakovat tak dlouho, až zjistíte citlivou skupinu nejvyšší úrovně).

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-ata"></a>Jak můžu ATA využít k monitorování virtuálního řadiče domény?
Většina virtuálních řadičů domény se dá pokrýt komponentami ATA Lightweight Gateway. K určení, jestli je komponenta ATA Lightweight Gateway pro vaše prostředí vhodná, použijte informace v tématu [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning).

Pokud se virtuální řadič domény nedá pokrýt komponentou ATA Lightweight Gateway, můžete komponenty ATA Gateway mít virtuální nebo fyzické, jak popisuje téma [Konfigurace zrcadlení portů](/advanced-threat-analytics/deploy-use/configure-port-mirroring).  <br />Nejjednodušší je mít virtuální ATA Gateway na každém hostiteli, kde existují virtuální řadiče domény.<br />Pokud se virtuální řadiče domény přesunují mezi hostiteli, je třeba provést jednu z následujících akcí:

-   Pokud se virtuální řadič domény přesune na jiného hostitele, pro ATA Gateway na tomto hostiteli předem nakonfigurujte příjem provozu z nedávno přesunutého virtuálního řadiče domény.
-   Zkontrolujte, že jste virtuální ATA Gateway přidružili k virtuálnímu řadiči domény, takže pokud se přesune, ATA Gateway se přesune s ním.
-   Některé virtuální přepínače mohou odesílat provoz mezi hostiteli.

## <a name="how-do-i-back-up-ata"></a>Jak se ATA dá zálohovat?
Musí se zálohovat dvě věci:

-   Provoz a události, které ATA ukládá. K jejich zálohování se dá využít libovolná podporovaná procedura zálohování databází. Další informace najdete v tématu [Správa databází ATA](/advanced-threat-analytics/deploy-use/ata-database-management). 
-   Konfigurace konzoly ATA. Konfigurace je uložena v databázi a každou hodinu se automaticky zálohuje do složky **Zálohování** v umístění v rámci nasazení ATA Center.  Další informace získáte v části [Správa databáze ATA](https://docs.microsoft.com/advanced-threat-analytics/deploy-use/ata-database-management).



## <a name="what-can-ata-detect"></a>Co ATA dokáže rozpoznat?

ATA rozpoznává známé nebezpečné útoky a techniky, problémy zabezpečení a rizika.
Úplný seznam detekcí ATA najdete v tématu [Jaké detekce ATA provádí?](ata-threats.md).

## <a name="what-kind-of-storage-do-i-need-for-ata"></a>Jaký druh úložiště budu pro ATA potřebovat?
Doporučujeme rychlé úložiště (nikoli disky s 7200 ot./min) s nízkými hodnotami latence (méně než 10 ms). Konfigurace RAID vy měla podporovat velkou zátěž při zápisu (nikoli RAID-5/6 nebo odvozené konfigurace).

## <a name="how-many-nics-does-the-ata-gateway-require"></a>Kolik síťových karet ATA Gateway vyžaduje?
ATA Gateway vyžaduje minimálně dva síťové adaptéry:<br>1. Síťovou kartu pro připojení k interní síti a komponentě ATA Center<br>2. Síťovou kartu, která se použije pro zachycení síťového provozu na řadiči domény prostřednictvím zrcadlení portů<br>* To neplatí pro komponentu ATA Lightweight Gateway, která nativně využívá všechny síťové adaptéry využívané řadičem domény.

## <a name="what-kind-of-integration-does-ata-have-with-siems"></a>Jaký druh integrace se systémy SIEM ATA využívá?
Se systémy SIEM ATA využívá obousměrnou integraci:

1. Pro případ podezřelých aktivit se v ATA dá nakonfigurovat odesílání výstrahy Syslog na libovolný server SIEM s využitím formátu CEF.
2. V ATA se dá nakonfigurovat příjem zpráv z [těchto systémů SIEM](/advanced-threat-analytics/deploy-use/configure-event-collection#siem-support) pro všechny události systému Windows s ID 4776.

## <a name="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Může ATA monitorovat řadiče domény virtualizované ve vašem řešení IaaS?
Ano, ATA Lightweight Gateway se dá použít k monitorování řadičů domény, které jsou v libovolném řešení IaaS.

## <a name="is-this-an-on-premises-or-in-cloud-offering"></a>Jedná se o místní nebo cloudovou nabídku?
Microsoft Advanced Threat Analytics je místní produkt.

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>Bude součástí Azure Active Directory nebo místní služby Active Directory?
Toto řešení se v současnosti nabízí samostatně. Není součástí Azure Active Directory ani místní služby Active Directory.

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>Je potřeba psát vlastní pravidla a určovat prahové nebo základní hodnoty?
Microsoft Advanced Threat Analytics nevyžaduje vytváření pravidel ani prahových nebo základních hodnot a jejich následné vyladění. ATA analyzuje chování uživatelů, zařízení a prostředků a také jejich vzájemné vztahy. Dokáže rychle detekovat podezřelé aktivity a známé útoky. Tři týdny po nasazení ATA začne detekovat behaviorálně podezřelé aktivity. Naproti tomu známé útoky se zlými úmysly a problémy zabezpečení začne ATA detekovat bezprostředně po nasazení.

## <a name="if-you-are-already-breached-will-microsoft-advanced-threat-analytics-be-able-to-identify-abnormal-behavior"></a>Pokud už došlo k porušení zabezpečení, dokáže nástroj Microsoft Advanced Threat Analytics identifikovat neobvyklé chování?
Ano, i když se ATA nainstaluje až po porušení zabezpečení, dokáže rozpoznat podezřelé aktivity hackerů. ATA nejenom zkoumá chování uživatelů, ale současně se taky dívá na ostatní uživatele v organizační mapě zabezpečení. Pokud je chování útočníka během počáteční analýzy nestandardní, je identifikovaný jako „outlier“ a ATA bude toto nestandardní chování dál hlásit. ATA může dál detekovat podezřelou aktivitu, pokud se hacker pokusí ukrást přihlašovací údaje jiných uživatelů, třeba Pass-the-Ticket, nebo se pokusí provést vzdálené spuštění na jednom z řadičů domény.

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>Využívají se přitom jenom přenosy služby Active Directory?
Kromě analýzy provozu služby Active Directory pomocí technologie hloubkové kontroly paketů ATA taky shromažďuje relevantní události ze služby SIEM (Security Information and Event Management) a na základě informací získaných ze služby Active Directory Domain Services vytváří profily entit. Pokud organizace nakonfiguruje předávání Protokolu událostí systému Windows, může ATA taky shromažďovat události z protokolů událostí.

## <a name="what-is-port-mirroring"></a>Co je zrcadlení portů?
Zrcadlení portů, které se taky označuje jako SPAN (Switched Port Analyzer), je metoda monitorování síťových aktivit. Pokud je zrcadlení portů povolené, přepínač odešle kopii všech síťových paketů zjištěných na jednom portu (nebo v celé síti VLAN) na jiný port, kde se tyto pakety dají analyzovat.

## <a name="does-ata-monitor-only-domain-joined-devices"></a>Monitoruje ATA jenom zařízení připojená k doméně?
Ne. ATA monitoruje všechna zařízení v síti, která zpracovávají požadavky ověřování a autorizace pro službu Active Directory, včetně zařízení s jiným systémem než Windows a mobilních zařízení.

## <a name="does-ata-monitor-computer-accounts-as-well-as-user-accounts"></a>Monitoruje ATA jak účty počítačů, tak uživatelské účty?
Ano. Vzhledem k tomu, že účty počítačů se (stejně jako ostatní entity) dají využít k provádění škodlivých aktivit, ATA monitoruje chování všech účtů počítačů a všechny ostatní entity v příslušném prostředí.

## <a name="can-ata-support-multi-domain-and-multi-forest"></a>Může ATA podporovat několik domén a doménových struktur?
Microsoft Advanced Threat Analytics podporuje prostředí s více doménami v rámci stejné doménové struktury. Více doménových struktur vyžaduje nasazení ATA pro každou doménovou strukturu.

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>Dá se zjistit celkový stav nasazení?
Ano, můžete zobrazit celkový stav nasazení a taky konkrétní problémy související s konfigurací, možnostmi připojení atd. Když k nim dojde, dostanete upozornění.


## <a name="see-also"></a>Viz také
- [Požadavky ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Plánování kapacity ATA](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurace shromažďování událostí](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurace předávání událostí systému Windows](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

