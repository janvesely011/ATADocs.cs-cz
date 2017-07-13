---
title: "Nejčastější dotazy k Advanced Threat Analytics | Dokumentace Microsoftu"
description: "Seznam nejčastějších dotazů týkajících se ATA a související odpovědi"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/3/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5beabd2617f55ecbcc717338dc40d9f597cc25d4
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/03/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*

# Nejčastější dotazy k ATA
<a id="ata-frequently-asked-questions" class="xliff"></a>
Tento článek obsahuje seznam nejčastějších dotazů týkajících se ATA a poskytuje podrobné informace a odpovědi.


## Kde získám licenci na Advanced Threat Analytics (ATA)?
<a id="where-can-i-get-a-license-for-advanced-threat-analytics-ata" class="xliff"></a>

Pokud máte aktivní smlouvu Enterprise, můžete si tento software stáhnout z centra multilicencí Microsoftu (VLSC).

Pokud jste licenci na Microsoft Enterprise Mobility + Security (EMS) pořídili přímo přes portál Office 365 nebo prostřednictvím licenčního modelu partnera cloudových řešení (CSP) a nemáte k ATA přístup přes centrum multilicencí Microsoftu (VLSC), požádejte zákaznickou podporu Microsoftu o zpracování aktivace řešení ATA (Advanced Threat Analytics).

## Co mám dělat, když se ATA Gateway nespustí?
<a id="what-should-i-do-if-the-ata-gateway-wont-start" class="xliff"></a>
Podívejte se na poslední chybu v aktuálním protokolu chyb (ve složce Logs tam, je software ATA nainstalovaný).

## Jak se dá ATA otestovat?
<a id="how-can-i-test-ata" class="xliff"></a>
Pomocí jedné z následujících akcí můžete simulovat podezřelé aktivity a provést tak kompletní test:

1.  Rekognoskace DNS s využitím Nslookup.exe
2.  Vzdálené spuštění s využitím psexec.exe


To je potřeba spustit vzdáleně nikoli z komponenty ATA Gateway, ale nad monitorovaným řadičem domény.

## Které sestavení ATA odpovídá jednotlivým verzím?
<a id="which-ata-build-corresponds-to-each-version" class="xliff"></a>

|Verze|Číslo sestavení|
|----|----|
|1.6|1.6.4103|
|1.6 Update 1|1.6.4317|
|1.7|1.7.5402| 
|1.7 Update 1|1.7.5647|
|1.7 Update 2|1.7.5757|
|1.8|1.8.6645|

## Jakou verzi mám použít k upgradu aktuálního nasazení ATA na nejnovější verzi?
<a id="what-version-should-i-use-to-upgrade-my-current-ata-deployment-to-the-latest-version" class="xliff"></a>

![Tabulka upgradu verzí ATA](./media/version-matrix.png)


## Jak ověřím předávání událostí systému Windows?
<a id="how-do-i-verify-windows-event-forwarding" class="xliff"></a>
Do souboru můžete vložit tento kód a pak jej z příkazového řádku v adresáři: **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** můžete spustit následovně:

mongo.exe název souboru ATA

        db.getCollectionNames().forEach(function(collection) {
        if (collection.substring(0,10)=="NtlmEvent_") {
                if (db[collection].count() > 0) {
                                  print ("Found "+db[collection].count()+" NTLM events") 
                                }
                }
        });

## Funguje ATA při šifrovaném provozu?
<a id="does-ata-work-with-encrypted-traffic" class="xliff"></a>
ATA spoléhá na analýzu různých síťových protokolů a událostí shromažďovaných ze serveru SIEM nebo prostřednictvím předávání událostí Windows. Přestože se šifrovaný provoz (například LDAPS nebo IPSEC ESP) nebude analyzovat, bude ATA pořád fungovat a na většinu detekcí to nebude mít vliv.

## Funguje ATA s obranou protokolu Kerberos?
<a id="does-ata-work-with-kerberos-armoring" class="xliff"></a>
ATA podporuje povolení obrany protokolu Kerberos, která se také označuje jako architektura FAST (Flexible Authentication Secure Tunneling). Výjimkou je detekce typu over-pass-the-hash, která nebude fungovat.

## Kolik komponent ATA Gateways budu potřebovat?
<a id="how-many-ata-gateways-do-i-need" class="xliff"></a>

Počet komponent ATA Gateway závisí na rozvržení sítě, objemu paketů a objemu událostí, které konzola ATA zaznamená. Pokud chcete určit přesný počet, přejděte do části [Velikosti pro ATA Lightweight Gateway](ata-capacity-planning.md#ata-lightweight-gateway-sizing). 

## Jak velké úložiště budu pro ATA potřebovat?
<a id="how-much-storage-do-i-need-for-ata" class="xliff"></a>
Pro jeden plný den s průměrem 1000 paketů/s budete potřebovat 0,3 GB úložiště.<br /><br />Další informace o určení velikosti pro ATA Center najdete v tématu [Plánování kapacity ATA](ata-capacity-planning.md).


## Proč se některé účty považují za citlivé?
<a id="why-are-certain-accounts-considered-sensitive" class="xliff"></a>
Dojde k tomu, když je účet členem konkrétních skupin, které označujeme jako citlivé (například Domain Admins).

Pokud chcete pochopit, proč je účet citlivý, můžete zkontrolovat jeho členství ve skupinách a zjistit, do kterých citlivých skupin patří (skupina, do které patří, může být citlivá také kvůli jiné skupině, takže je potřeba celý proces opakovat tak dlouho, až zjistíte citlivou skupinu nejvyšší úrovně).

## Jak můžu ATA využít k monitorování virtuálního řadiče domény?
<a id="how-do-i-monitor-a-virtual-domain-controller-using-ata" class="xliff"></a>
Většina virtuálních řadičů domény se dá pokrýt komponentami ATA Lightweight Gateway. K určení, jestli je komponenta ATA Lightweight Gateway pro vaše prostředí vhodná, použijte informace v tématu [Plánování kapacity ATA](ata-capacity-planning.md).

Pokud se virtuální řadič domény nedá pokrýt komponentou ATA Lightweight Gateway, můžete komponenty ATA Gateway mít virtuální nebo fyzické, jak popisuje téma [Konfigurace zrcadlení portů](configure-port-mirroring.md).  <br />Nejjednodušší je mít virtuální ATA Gateway na každém hostiteli, kde existují virtuální řadiče domény.<br />Pokud se virtuální řadiče domény přesunují mezi hostiteli, je třeba provést jednu z následujících akcí:

-   Pokud se virtuální řadič domény přesune na jiného hostitele, pro ATA Gateway na tomto hostiteli předem nakonfigurujte příjem provozu z nedávno přesunutého virtuálního řadiče domény.
-   Zkontrolujte, že jste virtuální ATA Gateway přidružili k virtuálnímu řadiči domény, takže pokud se přesune, ATA Gateway se přesune s ním.
-   Některé virtuální přepínače mohou odesílat provoz mezi hostiteli.

## Jak se ATA dá zálohovat?
<a id="how-do-i-back-up-ata" class="xliff"></a>

Přečtěte si článek [Zotavení po havárii ATA](disaster-recovery.md).



## Co ATA dokáže rozpoznat?
<a id="what-can-ata-detect" class="xliff"></a>

ATA rozpoznává známé nebezpečné útoky a techniky, problémy zabezpečení a rizika.
Úplný seznam detekcí ATA najdete v tématu [Jaké detekce ATA provádí?](ata-threats.md).

## Jaký druh úložiště budu pro ATA potřebovat?
<a id="what-kind-of-storage-do-i-need-for-ata" class="xliff"></a>
Doporučujeme rychlé úložiště (nikoli disky s 7200 ot./min) s nízkými hodnotami latence (méně než 10 ms). Konfigurace RAID vy měla podporovat velkou zátěž při zápisu (nikoli RAID-5/6 nebo odvozené konfigurace).

## Kolik síťových karet ATA Gateway vyžaduje?
<a id="how-many-nics-does-the-ata-gateway-require" class="xliff"></a>
ATA Gateway vyžaduje minimálně dva síťové adaptéry:<br>1. Síťovou kartu pro připojení k interní síti a komponentě ATA Center<br>2. Síťovou kartu, která se použije pro zachycení síťového provozu na řadiči domény prostřednictvím zrcadlení portů<br>* To neplatí pro komponentu ATA Lightweight Gateway, která nativně využívá všechny síťové adaptéry využívané řadičem domény.

## Jaký druh integrace se systémy SIEM ATA využívá?
<a id="what-kind-of-integration-does-ata-have-with-siems" class="xliff"></a>
Se systémy SIEM ATA využívá obousměrnou integraci:

1. Pro případ podezřelých aktivit se v ATA dá nakonfigurovat odesílání výstrahy Syslog na libovolný server SIEM s využitím formátu CEF.
2. ATA lze nakonfigurovat tak, aby se z těchto [serverů SIEM](install-ata-step6.md) přijímaly zprávy Syslog pro události Windows.

## Může ATA monitorovat řadiče domény virtualizované ve vašem řešení IaaS?
<a id="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution" class="xliff"></a>
Ano, ATA Lightweight Gateway se dá použít k monitorování řadičů domény, které jsou v libovolném řešení IaaS.

## Jedná se o místní nebo cloudovou nabídku?
<a id="is-this-an-on-premises-or-in-cloud-offering" class="xliff"></a>
Microsoft Advanced Threat Analytics je místní produkt.

## Bude součástí Azure Active Directory nebo místní služby Active Directory?
<a id="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory" class="xliff"></a>
Toto řešení se v současnosti nabízí samostatně. Není součástí Azure Active Directory ani místní služby Active Directory.

## Je potřeba psát vlastní pravidla a určovat prahové nebo základní hodnoty?
<a id="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline" class="xliff"></a>
Microsoft Advanced Threat Analytics nevyžaduje vytváření pravidel ani prahových nebo základních hodnot a jejich následné vyladění. ATA analyzuje chování uživatelů, zařízení a prostředků a také jejich vzájemné vztahy. Dokáže rychle detekovat podezřelé aktivity a známé útoky. Tři týdny po nasazení ATA začne detekovat behaviorálně podezřelé aktivity. Naproti tomu známé útoky se zlými úmysly a problémy zabezpečení začne ATA detekovat bezprostředně po nasazení.

## Pokud už došlo k porušení zabezpečení, dokáže nástroj Microsoft Advanced Threat Analytics identifikovat neobvyklé chování?
<a id="if-you-are-already-breached-will-microsoft-advanced-threat-analytics-be-able-to-identify-abnormal-behavior" class="xliff"></a>
Ano, i když se ATA nainstaluje až po porušení zabezpečení, dokáže rozpoznat podezřelé aktivity hackerů. ATA nejenom zkoumá chování uživatelů, ale současně se taky dívá na ostatní uživatele v organizační mapě zabezpečení. Pokud je chování útočníka během počáteční analýzy nestandardní, je identifikovaný jako „outlier“ a ATA bude toto nestandardní chování dál hlásit. ATA může dál detekovat podezřelou aktivitu, pokud se hacker pokusí ukrást přihlašovací údaje jiných uživatelů, třeba Pass-the-Ticket, nebo se pokusí provést vzdálené spuštění na jednom z řadičů domény.

## Využívají se přitom jenom přenosy služby Active Directory?
<a id="does-this-only-leverage-traffic-from-active-directory" class="xliff"></a>
Kromě analýzy provozu služby Active Directory pomocí technologie hloubkové kontroly paketů ATA taky shromažďuje relevantní události ze služby SIEM (Security Information and Event Management) a na základě informací získaných ze služby Active Directory Domain Services vytváří profily entit. Pokud organizace nakonfiguruje předávání Protokolu událostí systému Windows, může ATA taky shromažďovat události z protokolů událostí.

## Co je zrcadlení portů?
<a id="what-is-port-mirroring" class="xliff"></a>
Zrcadlení portů, které se taky označuje jako SPAN (Switched Port Analyzer), je metoda monitorování síťových aktivit. Pokud je zrcadlení portů povolené, přepínač odešle kopii všech síťových paketů zjištěných na jednom portu (nebo v celé síti VLAN) na jiný port, kde se tyto pakety dají analyzovat.

## Monitoruje ATA jenom zařízení připojená k doméně?
<a id="does-ata-monitor-only-domain-joined-devices" class="xliff"></a>
Ne. ATA monitoruje všechna zařízení v síti, která zpracovávají požadavky ověřování a autorizace pro službu Active Directory, včetně zařízení s jiným systémem než Windows a mobilních zařízení.

## Monitoruje ATA jak účty počítačů, tak uživatelské účty?
<a id="does-ata-monitor-computer-accounts-as-well-as-user-accounts" class="xliff"></a>
Ano. Vzhledem k tomu, že účty počítačů se (stejně jako ostatní entity) dají využít k provádění škodlivých aktivit, ATA monitoruje chování všech účtů počítačů a všechny ostatní entity v příslušném prostředí.

## Může ATA podporovat několik domén a doménových struktur?
<a id="can-ata-support-multi-domain-and-multi-forest" class="xliff"></a>
Microsoft Advanced Threat Analytics podporuje prostředí s více doménami v rámci stejné doménové struktury. Více doménových struktur vyžaduje nasazení ATA pro každou doménovou strukturu.

## Dá se zjistit celkový stav nasazení?
<a id="can-you-see-the-overall-health-of-the-deployment" class="xliff"></a>
Ano, můžete zobrazit celkový stav nasazení a taky konkrétní problémy související s konfigurací, možnostmi připojení atd. Když k nim dojde, dostanete upozornění.


## Viz také
<a id="see-also" class="xliff"></a>
- [Požadavky ATA](ata-prerequisites.md)
- [Plánování kapacity ATA](ata-capacity-planning.md)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Konfigurace předávání událostí systému Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

