---
title: Integrace Azure Advanced Threat Protection s ochrany ATP v programu Windows Defender | Dokumentace Microsoftu
description: Integrace rozšířené ochrany před internetovými útoky pro Azure pomocí ochrany ATP v programu Windows Defender pro úplné ohrožení rozsahu zjišťování
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/5/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 097769c53eefd1c6e5242086cd56d47b89b36e68
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126259"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*

# <a name="integrating-azure-atp-with-windows-defender-atp"></a>Integrace ochrany ATP v programu Azure s programem Windows Defender ATP

Azure Advanced Threat Protection umožňuje integrovat ochrany ATP v programu Azure s Windows Defender ATP pro ještě podrobnější řešení ochrany před hrozbami. Během ochrany ATP v programu Azure monitoruje provoz na řadičích domény, ochrana ATP v programu Windows Defender monitoruje vaše koncové body společně poskytuje tak jednotné rozhraní, ze kterého budete moci chránit vaše prostředí.

Prostřednictvím integrace ochrany ATP v programu Windows Defender do ochrany ATP v programu Azure, můžete plně využívat potenciál obou služeb a zabezpečit vaše prostředí, včetně:

- Azure ATP senzory a samostatné senzorů: může být umístěn souběžně přímo na řadiče domény nebo zrcadlení portů z řadičů domény do ochrany ATP v programu, k zachycení a parsování síťového provozu různých protokolů (například Kerberos, DNS, RPC, NTLM a další) pro ověřování autorizaci a shromažďování informací. 

-   Senzory chování koncového bodu: vložená ve Windows 10, tyto senzory shromažďovat a zpracovávat chování signály od operačního systému (například proces, registr, souboru a síťovou komunikaci) a odešle tato data ze senzorů do izolovaného, vašeho privátního cloudu instance ochrany ATP v programu Windows Defender.

- Analýzy zabezpečení v cloudu: využití velkých objemů dat, machine learning a jedinečný Microsoft zobrazení v ekosystému Windows (například [nástroj pro odstranění škodlivého softwaru Microsoft](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), cloudové produkty enterprise (např. Office 365) a online prostředků (jako je Bing a adresu URL SmartScreen urs) chování signály přeložit na přehledy, detekce a doporučuje pokročilé hrozby.

- Hrozeb: generovaný myslivci Microsoft teams zabezpečení a rozšířen o analýzy hrozeb, které jsou k dispozici od partnerů, threat intelligence umožňuje programu Windows Defender ATP identifikovat útočník nástroje, techniky a postupy, a generovat upozornění pro případ Tyto jsou dodržovány v datech shromážděných senzoru.

Technologie ochrany ATP v programu Azure detekuje různé podezřelé aktivity, zaměřuje se na několik fází v řetězci kill internetového útoku včetně:

- Rekognoskace, během které útočníci shromáždit informace o tom, jak je sestavená prostředí, jaké různé formáty jsou a entit, které neexistuje. Se připravují si plán pro další fáze útoku.

- Cyklus laterálního pohybu, během kterého útočník investuje čas a úsilí do rozšíření prostoru pro útoky uvnitř vaší sítě.

- Dominance domény (trvalost), během které útočník zachycuje informace, které mu umožňují pokračovat v kampani pomocí různých sad vstupních bodů, přihlašovacích údajů a technik.

Ve stejnou dobu ochrana ATP v programu Windows Defender využívá technologie Microsoftu a odborných znalostí ke zjištění sofistikovaného kybernetických útoků, poskytuje:

- Detekce útoku na základě chování, s využitím cloudu, Upřesnit<br></br>Vyhledá útoků, které provedli za všechny ostatní ochrany (odeslání detekce porušení zabezpečení), poskytuje praktické, korelační výstrahy známými i neznámými nežádoucí osoby začít pokusu skrýt jejich aktivity u koncových bodů.

- Bohaté časovou osu pro forenzní šetření a zmírnění distribuovaných útoků<br></br>Snadno prozkoumejte rozsahu porušení nebo podezřelé chování na jakýkoli počítač pomocí časové osy bohaté počítače. Soubor, adresy URL a inventáře síťové připojení přes síť. Získejte další informace, pomocí hluboké shromažďování a analýze ("výbuchu") pro kterýkoli soubor nebo adresy URL.

- Součástí jedinečný threat intelligence znalostní báze<br></br>Bezkonkurenční hrozeb optická poskytuje podrobnosti objektu actor a záměru kontext pro každé platformy intel detekce hrozeb – kombinace první a třetí strany řady zdrojů.

## <a name="prerequisites"></a>Požadavky

Pokud chcete povolit tuto funkci, potřebujete licenci pro služby Azure ATP a ochrana ATP v programu Windows Defender. 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>Postup při integraci služby Azure ATP s ochrany ATP v programu Windows Defender

1. Nastavit pracovní prostor má být integrován jako **primární**. Jenom jeden pracovní prostor může být primární pracovní prostor a pouze primární pracovní prostor můžete integrovat s dalšími službami. Potřebujete, v určitém okamžiku v budoucnu, by měl provádět tento pracovní prostor už primárním pracovním prostorem, budete nejdřív muset odebrat tuto integraci, než budete moct nastavit jako jiné než primární.

 ![primární pracovní prostor](./media/primary-workspace.png)

2. Klikněte na tlačítko **konfigurace**a v části **zdroje dat** vyberte **ochrany ATP v programu Windows Defender**. Pak klikněte na odkaz na **Správa pracovních prostorů**. To je k dispozici pouze v případě, že máte licenci pro ochrany ATP v programu Windows Defender a jste už provedli procesu zavádění pro ochrany ATP v programu Windows Defender. 

3. V primárním pracovním prostorem klikněte na ikonu nastavení.

 ![integrace pracovní prostor](./media/edit-workspace.png)
 
3. Nastavení integrace **na**. 

 ![povolení integrace](./media/enable-integration.png)

4. V [portál ochrany ATP v programu Windows Defender](https://beta.securitycenter.windows.com/preferences/advanced), přejděte na stránku **nastavení**, **pokročilé funkce** a nastavte **integrace služby Azure ATP** k  **DÁLE**. 

 ![Povolení integrace ochrany ATP v programu Windows Defender](./media/wd-atp-enable.png)

5. Chcete-li zkontrolovat stav integrace na portálu ochrany ATP v programu Azure pracovní prostor, přejděte na **nastavení** a potom **integrace ochrany ATP v programu Windows Defender**. Zobrazí se stav integrace; Pokud se něco stalo, že se zobrazí chyba. Můžete také zobrazit, který pracovní prostor je integrovaná s ochrany ATP v programu Windows Defender.

## <a name="how-it-works"></a>Jak to funguje

Po ochrany ATP v programu Azure a ochrana ATP v programu Windows Defender jsou plně integrované, na portálu ochrany ATP v programu Azure pracovní prostor, v místní nabídce miniprofilu a na stránce profil entity, každá entita, která existuje v ochrany ATP v programu Windows Defender zahrnuje oznámení "BADGE" k zobrazení, že je integrovaná s Windows Ochrana ATP v programu Defender. 

 ![Oznámení ochrany ATP v programu Windows Defender](./media/profile-alerts-wd.png)

Pokud entita obsahuje výstrah ve službě ochrana ATP v programu Windows Defender, je číslo vedle Odznáček dali vám vědět, kolik upozornění byla aktivována.

 ![Upozornění Azure ATP](./media/atp-integrated-wd-icon-alerts.png)

Vyberete-li u odznáčku, budete přesměrováni na portál ochrany ATP v programu Windows Defender, kde můžete zobrazit a zmírnit výstrahy. Pokud subjektem není rozpoznána ochrany ATP v programu Windows Defender, je zobrazena šedě odznáčku. 

 ![Šedé ochrany ATP v programu Windows Defender](./media/wd-grey.png)

Na portálu ochrany ATP v programu Windows Defender po kliknutí na koncový bod, můžete zobrazit výstrahy služby Azure ATP. Pokud kliknete na upozornění pro tuto entitu v ochrany ATP v programu Windows Defender, otevře se stránka profil entity v ochrany ATP v programu Azure. 
 
 > ! [POZNÁMKA] V současné době podporuje integraci služby Azure ATP s ochrany ATP v programu Windows Defender pouze uživatelé a počítače z místní AD. Uživatele z Azure AD a nebude se zobrazovat virtuální počítače, které jsou spravované v Azure jako součást Integrace 

![Oznámení ochrany ATP v programu Windows Defender](./media/wd-atp-alerts.png)


## <a name="see-also"></a>Viz také

- [Prošetřování laterálních průnikových tras pomocí služby Azure ATP](use-case-lateral-movement-path.md)
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Architektura služby Azure ATP](atp-architecture.md)
- [Instalace ochrany ATP v programu](install-atp-step1.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)

