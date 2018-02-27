---
title: "Advanced Threat Protection integrace se službou Azure s Windows Defender ATP | Microsoft Docs"
description: "Postup pro integraci Azure Advanced Threat Protection pro pokrytí detekce hrozeb úplné Windows Defender ATP"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: f6f3ed75-d6bb-4966-a9a7-5339c4f3ebac
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3521e500548b04febbff37d3dfe9150cf6f2d35b
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/21/2018
---
*Platí pro: Azure Advanced Threat Protection*

# <a name="integrating-azure-atp-with-windows-defender-atp"></a>Integrování Azure ATP programu Windows Defender ATP

Azure Advanced Threat Protection umožňuje integrovat Azure ATP Windows Defender ATP neexistuje i více dokončení ochrany řešení hrozeb. Při Azure ATP monitoruje provoz na řadičích domény, Windows Defender ATP monitoruje koncové body, a současně poskytuje jediné rozhraní, ze kterého budete moci chránit vaše prostředí.

> [!NOTE]
> Integrace je aktuálně povoleno pouze v případě, že jste zákazník s Windows Defender ATP privátní Preview verzi.
 
Díky integraci Windows Defender ATP do Azure ATP, můžete využít potenciál obě služby a zabezpečit vaše prostředí, včetně:

- Azure ATP senzory a samostatné snímače: můžete pohodlně přímo na řadiči domény nebo zrcadlení portů z řadičů domény na ATP, k zaznamenání a analyzovat síťový provoz více protokolů (například protokolu Kerberos, DNS, RPC, protokol NTLM a dalších) pro ověřování, autorizace a shromažďování informací. 

-   Koncový bod chování snímače: vložených v systému Windows 10, podobných senzorů shromažďovat a zpracovávat chování signály z operačního systému (například procesu, registr, souboru a síťovou komunikaci) a odešle tato data snímače do cloudu privátní, izolované, instance Windows Defender ATP.

- Zabezpečení analýzy v cloudu: využívat Microsoft zobrazení velkých objemů dat, strojové učení a jedinečný mezi ekosystému Windows (například [nástroj pro odstranění škodlivého softwaru Microsoft](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx)), produkty enterprise cloud (např. Office 365), a online prostředky (například Bing a adresy URL SmartScreen urs), jsou chování signály přeložit na statistiky, detekce a doporučené odpovědi na pokročilé hrozby.

- Hrozby intelligence: generovaného myslivci Microsoft zabezpečení týmy a rozšířen o analýzou hrozeb, které zajišťují partneři, threat intelligence umožňuje Windows Defender ATP k identifikaci útočník nástrojů, technik a postupů a generování výstrah při To je možné vysledovat v datech shromážděných senzor.

Azure technologie ATP zjištění několik podezřelých aktivit, zaměřené na několik fází internetový útoku kill řetězu včetně:

- Rekognoskace, během které útočníci shromažďovat informace o tom, jak je integrovaná prostředí, jaké jiné prostředky jsou a entit, které neexistuje. Obecně se vytváření jejich plán pro další fáze útoku.

- Cyklus laterálního pohybu, během kterého útočník investuje čas a úsilí do rozšíření prostoru pro útoky uvnitř vaší sítě.

- Dominance v doméně (trvalost), během které útočník zachytává informace, což jim umožní obnovit jejich kampaň použití různých sad vstupních bodů, přihlašovací údaje a techniky.

Ve stejnou dobu Windows Defender ATP využívá technologie společnosti Microsoft a odborných znalosti ke zjištění sofistikované internetovými útoky, poskytuje:

- Detekce útoku na základě chování, používá technologii cloudu, Upřesnit<br></br>Vyhledá útoky provedené za všechny ostatní obrany (post porušení detekce), poskytuje řešitelné, korelační výstrahy pro známé a Neznámý nežádoucí pokusu skrýt jejich aktivity koncové body.

- Časová osa bohaté u forenzního vyšetřování a zmírnění<br></br>Zjistěte, snadno rozsahu porušení nebo podezřelé chování z jakéhokoli počítače prostřednictvím časová osa bohaté počítače. Soubor, adresy URL a inventáře síťové připojení přes síť. Získáte další informace o použití hloubkové sběru a analýzy ("detonaci") pro libovolný soubor nebo adresy URL.

- Součástí znalostní báze intelligence jedinečný hrozeb<br></br>Kabel bezkonkurenční threat poskytuje podrobnosti objektu actor a záměrné kontext pro všechny procesory intel detekce hrozeb – kombinování první a třetí strany intelligence zdroje.

## <a name="prerequisites"></a>Požadavky

Chcete-li povolit tuto funkci, potřebujete licenci pro Azure ATP a Windows Defender ATP. 


## <a name="how-to-integrate-azure-atp-with-windows-defender-atp"></a>Postup pro integraci Azure ATP Windows Defender ATP

1. Nastavení pracovního prostoru, kterou chcete integrovat jako **primární**. Jenom jeden pracovní prostor může být primárním pracovním prostorem a pouze primární pracovní prostor můžete integrovat s jinými službami. Pokud v určitém okamžiku v budoucnu, měli chcete tohoto pracovního prostoru už primárním pracovním prostorem, je nutné nejprve odebrat integraci, než budete moct nastavit jako není primární.

 ![primárním pracovním prostorem](./media/primary-workspace.png)

2. Klikněte na tlačítko **konfigurace**a v části **zdroje dat** vyberte **Windows Defender ATP**. Pak klikněte na odkaz na **pracovního prostoru Správa**. To je k dispozici pouze v případě, že máte licenci pro Windows Defender ATP a jste již provedli proces Startovní pro Windows Defender ATP. 

3. V primárním pracovním prostorem klikněte na ikonu nastavení.

 ![pracovní prostor integrace](./media/edit-workspace.png)
 
3. Nastavení integrace **na**. 

 ![Povolit integraci](./media/enable-integration.png)

4. V [portál Windows Defender ATP](https://beta.securitycenter.windows.com/preferences/advanced), přejděte na **nastavení**, **pokročilé funkce** a nastavte **integrace Azure ATP** k  **ON**. 

 ![Povolení integrace Windows Defender ATP](./media/wd-atp-enable.png)

5. Chcete-li zkontrolovat stav integraci, na portálu Azure ATP pracovního prostoru, přejděte na **nastavení** a potom **integrace Windows Defender ATP**. Zobrazí se stav integrace; Pokud je něco špatně zobrazí chybu. Můžete také zjistit, které pracovní prostor je integrována Windows Defender ATP.

## <a name="how-it-works"></a>Jak to funguje

Po Azure ATP a Windows Defender ATP jsou plně integrované, na portálu Azure ATP pracovního prostoru, v místní nabídce zkrácený profil a na stránce profil entity Každá entita, která existuje v systému Windows Defender ATP zahrnuje oznámení "BADGE" zobrazit, že je integrovaná s Windows Defender ATP. 

 ![Windows Defender ATP výstrahy](./media/profile-alerts-wd.png)

Pokud entita obsahuje výstrahy v systému Windows Defender ATP, je číslo vedle oznámení "BADGE" umožňují vědět, kolik výstrahy byly vyvolány.

 ![Azure ATP výstrahy](./media/atp-integrated-wd-icon-alerts.png)

Pokud kliknete na oznámení "BADGE", budete přesměrováni na portálu Windows Defender ATP, kde můžete zobrazit a zmírnit výstrahy. Pokud entita není rozpoznáno Windows Defender ATP, je zobrazena šedě oznámení "BADGE". 

 ![Šedá Windows Defender ATP](./media/wd-grey.png)

Na portálu Windows Defender ATP po kliknutí na koncový bod, můžete zobrazit výstrahy Azure ATP. Pokud kliknete na výstrahy pro tuto entitu v systému Windows Defender ATP, otevře se stránka profilu entity v Azure ATP. 

 ![Windows Defender ATP výstrahy](./media/wd-atp-alerts.png)


## <a name="see-also"></a>Viz také

- [Příčin laterální pohyb cesty s Azure ATP](use-case-lateral-movement-path.md)
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Architektura služby Azure ATP](atp-architecture.md)
- [Nainstalujte ATP](install-atp-step1.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)

