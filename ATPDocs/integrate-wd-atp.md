---
title: Integrace Azure Advanced Threat Protection s ochrany ATP v programu Windows Defender | Dokumentace Microsoftu
description: Integrace rozšířené ochrany před internetovými útoky pro Azure pomocí ochrany ATP v programu Windows Defender pro úplné ohrožení rozsahu zjišťování
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 10/18/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9c0cb92ca45c1d70c30f13fbe9821537f03e1062
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/30/2019
ms.locfileid: "58673873"
---
# <a name="integrate-azure-atp-with-windows-defender-atp"></a>Integrace ochrany ATP v programu Azure s programem Windows Defender ATP

Azure Advanced Threat Protection umožňuje integrovat ochrany ATP v programu Azure s Windows Defender ATP pro ještě podrobnější řešení ochrany před hrozbami. Během ochrany ATP v programu Azure monitoruje provoz na řadičích domény, ochrana ATP v programu Windows Defender monitoruje vaše koncové body společně poskytuje tak jednotné rozhraní, ze kterého budete moci chránit vaše prostředí.

Prostřednictvím integrace ochrany ATP v programu Windows Defender do ochrany ATP v programu Azure, můžete plně využívat potenciál obou služeb a zabezpečit vaše prostředí, včetně:

- Azure ochrany ATP v programu senzory a samostatné senzory: Může být umístěn souběžně přímo na řadiče domény nebo zrcadlení portů z řadičů domény do ochrany ATP v programu, k zachycení a parsování síťového provozu různých protokolů (například Kerberos, DNS, RPC, NTLM a další) pro ověřování, autorizaci a shromažďování informací. 

-   Senzory chování koncového bodu: Součástí Windows 10, tyto senzory shromažďovat a zpracovávat chování signály od operačního systému (například proces, registr, souboru a síťovou komunikaci) a odesílat tato data ze senzorů k vaší instanci cloudu privátní, izolované, z ochrany ATP v programu Windows Defender.

- Analýzy zabezpečení cloudu: Využití velkých objemů dat, machine learning a jedinečný Microsoft zobrazení v ekosystému Windows (například [nástroj pro odstranění škodlivého softwaru Microsoft](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), cloudové produkty enterprise (např. Office 365) a online prostředků (například Bing a adresu URL SmartScreen urs) chování signály jsou přeloženy na přehledy, detekce a doporučuje pokročilé hrozby.

- Analýza hrozeb: Generovaný myslivci Microsoft teams zabezpečení a rozšířen o poskytovaných partnery analýzy hrozeb, analýzy hrozeb umožňuje programu Windows Defender ATP identifikovat útočník nástroje, technik, postupy a generovat výstrahy, když jsou tyto aktivity pozorovaná v daty ze snímačů shromážděná.

Technologie ochrany ATP v programu Azure detekuje různé podezřelé aktivity, zaměřuje se na několik fází v řetězci kill internetového útoku včetně:

- Rekognoskace, během které útočníci shromáždit informace o tom, jak je sestavená prostředí, jaké různé formáty jsou a entit, které neexistuje. Obvykle vytváří si plán pro další fáze útoku v tomto poli.

- Cyklus laterálního pohybu, během kterého útočník investuje čas a úsilí do rozšíření prostoru pro útoky uvnitř vaší sítě.

- Dominance domény (trvalost), během které útočník zachycuje informace, které mu umožňují pokračovat v kampani pomocí různých sad vstupních bodů, přihlašovacích údajů a technik.

Ve stejnou dobu ochrana ATP v programu Windows Defender využívá technologie Microsoftu a odborných znalostí ke zjištění sofistikovaného kybernetických útoků, poskytuje:

- Detekce útoku na základě chování, s využitím cloudu, Upřesnit<br></br>Vyhledá útoků, které provedli za všechny ostatní ochrany (odeslání detekce porušení zabezpečení), poskytuje praktické, korelační výstrahy známými i neznámými nežádoucí osoby začít pokusu skrýt jejich aktivity u koncových bodů.

- Bohaté časovou osu pro forenzní šetření a zmírnění distribuovaných útoků<br></br>Snadno prozkoumejte rozsahu porušení nebo podezřelé chování na jakýkoli počítač pomocí časové osy bohaté počítače. Soubor, adresy URL a inventáře síťové připojení přes síť. Získejte další informace, pomocí hluboké shromažďování a analýze ("výbuchu") pro kterýkoli soubor nebo adresy URL.

- Součástí jedinečný threat intelligence znalostní báze<br></br>Zjišťování – kombinace první a třetí strany intelligence zdroje na základě bezkonkurenční hrozeb optická poskytuje podrobnosti objektu actor a záměru kontextu pro každý analýzy hrozeb.

## <a name="prerequisites"></a>Požadavky

Pokud chcete povolit tuto funkci, potřebujete licenci pro služby Azure ATP a ochrana ATP v programu Windows Defender. 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>Postup při integraci služby Azure ATP s ochrany ATP v programu Windows Defender

1. Na portálu ochrany ATP v programu Azure otevřete **konfigurace**. 

    ![Nabídka Azure Konfigurace ochrany ATP v programu](./media/atp-configuration-wd.png)
2. Vyberte v seznamu konfigurací **ochrany ATP v programu Windows Defender** a nastavte přepínač integrace na **na**. 

    ![Povolení integrace Windows Defender](./media/enable-integration.png)


3. V [portál ochrany ATP v programu Windows Defender](https://securitycenter.windows.com/preferences/advanced), přejděte na stránku **nastavení**, **pokročilé funkce** a nastavte **integrace služby Azure ATP** k  **DÁLE**. 

    ![Povolení integrace ochrany ATP v programu Windows Defender](./media/wd-atp-enable.png)

4. Chcete-li zkontrolovat stav integrace portálu ochrany ATP v programu Azure, přejděte na **nastavení** > **integrace ochrany ATP v programu Windows Defender**. Zobrazí se stav integrace a pokud se něco stalo, zobrazí se chyba. 

## <a name="how-it-works"></a>Jak to funguje

Po ochrany ATP v programu Azure a ochrana ATP v programu Windows Defender jsou plně integrované, na portálu ochrany ATP v programu Azure, v místní nabídce miniprofilu a na stránce profil entity obsahuje každá entita, která existuje v programu Windows Defender ATP oznámení "BADGE" k zobrazení, že je integrovaná s ochrany ATP v programu Windows Defender. 

 ![Oznámení ochrany ATP v programu Windows Defender](./media/profile-alerts-wd.png)

Pokud entita obsahuje výstrah ve službě ochrana ATP v programu Windows Defender, je číslo vedle Odznáček dali vám vědět, kolik upozornění byla aktivována.

 ![Upozornění Azure ATP](./media/atp-integrated-wd-icon-alerts.png)

Vyberete-li u odznáčku, budete přesměrováni na portál ochrany ATP v programu Windows Defender, kde můžete zobrazit a zmírnit výstrahy. Pokud subjektem není rozpoznána ochrany ATP v programu Windows Defender, je zobrazena šedě odznáčku. 

 ![Šedé ochrany ATP v programu Windows Defender](./media/wd-grey.png)

Z portálu ochrany ATP v programu Windows Defender klikněte na koncový bod chcete-li zobrazit výstrahy služby Azure ATP. Pokud kliknete na upozornění pro tuto entitu v ochrany ATP v programu Windows Defender, otevře se stránka profil entity v ochrany ATP v programu Azure. 
 
 > [!NOTE]
 > V současné době podporuje integraci služby Azure ATP s ochrany ATP v programu Windows Defender pouze uživatelé a počítače z místní AD. Uživatele z Azure AD a nebude se zobrazovat virtuální počítače, které jsou spravované v Azure jako součást Integrace 

![Oznámení ochrany ATP v programu Windows Defender](./media/wd-atp-alerts.png)


## <a name="see-also"></a>Viz také

- [Prošetřování laterálních průnikových tras pomocí služby Azure ATP](use-case-lateral-movement-path.md)
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Architektura služby Azure ATP](atp-architecture.md)
- [Instalace ochrany ATP v programu](install-atp-step1.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)

