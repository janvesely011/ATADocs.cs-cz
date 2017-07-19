---
title: "Prošetření eskalace oprávnění prostřednictvím útoků založených na zfalšovaných datech autorizace| Dokumentace Microsoftu"
description: "Tento článek popisuje eskalaci oprávnění prostřednictvím útoků založených na zfalšovaných datech autorizace a poskytuje pokyny k prošetření, pokud byla tato hrozba detekována ve vaší síti."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/4/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f3db435e-9553-40a2-a2ad-278fad4f0ef5
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 842e9866c5fdb447f49600501c4486da6db902f2
ms.sourcegitcommit: 4118dd4bd98994ec8a7ea170b09aa301a4be2c8a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/05/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*

# <a name="investigating-privilege-escalation-using-forged-authorization-data-attacks"></a>Prošetření eskalace oprávnění prostřednictvím útoků založených na zfalšovaných datech autorizace

Microsoft neustále zlepšuje své možnosti bezpečnostních detekcí a schopnost poskytovat analytikům zabezpečení téměř v reálném čase informace, na základě kterých pak můžou jednat. Tuto změnu pomáhá uskutečňovat služba Advanced Threat Analytics (ATA) Microsoftu. Pokud ATA detekuje eskalaci oprávnění prostřednictvím podezřelé aktivity související se zfalšovanými daty autorizace a zobrazí výstrahu, pomůže vám ji tento článek pochopit a prošetřit.

## <a name="what-is-a-privileged-attribute-certificate-pac"></a>Co je PAC (Privileged Attribute Certificate)?

PAC (Privileged Access Certificate) je datová struktura v lístku Kerberosu, která obsahuje autorizační informace, včetně členství ve skupinách, identifikátorů zabezpečení a informací o profilech uživatelů. V doméně Active Directory to umožňuje, aby se autorizační data poskytnutá řadičem domény předala dalším členským serverům a pracovním stanicím pro účely ověřování a autorizace. Kromě informací o členství obsahuje PAC další přihlašovací údaje, informace o profilech a zásadách a pomocná metadata zabezpečení. 

Datovou strukturu PAC používají protokoly ověřování (protokoly, které ověřují identity) k přenosu autorizačních informací, které řídí přístup k prostředkům.

### <a name="pac-validation"></a>Ověření PAC

Ověření PAC je funkce zabezpečení, která má útočníkovi zabránit v získání neoprávněného přístupu k systému nebo jeho prostředkům pomocí útoku man-in-the-middle, zejména v aplikacích, kde se používá zosobnění uživatele. Zosobnění zahrnuje důvěryhodnou identitu, třeba účet služby, který má zvýšená oprávnění pro přístup k prostředkům a provádění úloh. Ověření PAC posiluje bezpečnější autorizační prostředí v nastavení ověřování Kerberosu, když dojde ke zosobnění. [Ověření PAC](https://blogs.msdn.microsoft.com/openspecification/2009/04/24/understanding-microsoft-kerberos-pac-validation/) zajišťuje, že uživatel předloží přesná autorizační data, jak byla udělena v lístku Kerberosu, a že oprávnění lístku nejsou upravená.

Když se provede ověření PAC, server zakóduje zprávu požadavku obsahující typ a délku podpisu PAC a odešle ji řadiči domény. Řadič domény požadavek dekóduje a extrahuje hodnoty kontrolního součtu serveru a kontrolního součtu KDC. Pokud je ověření kontrolního součtu úspěšné, řadič domény serveru vrátí kód úspěšnosti. Neúspěšný návratový kód znamená, že došlo ke změně PAC. 

Obsah PAC Kerberosu je podepsaný dvakrát: 
- Jednou pomocí hlavního klíče KDC, aby se zabránilo škodlivým službám na straně serveru ve změnách autorizačních dat
- Jednou pomocí hlavního klíče účtu cílového serveru prostředků, aby se zabránilo uživateli v úpravách obsahu PAC a přidání vlastních autorizačních dat

### <a name="pac-vulnerability"></a>Ohrožení zabezpečení PAC
Bulletiny zabezpečení [MS14 068](https://technet.microsoft.com/library/security/MS14-068.aspx) a [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx) řeší ohrožení zabezpečení v KDC Kerberosu, díky kterým by útočník mohl manipulovat s polem PAC v platném lístku Kerberosu a tím si udělit další oprávnění.

## <a name="privilege-escalation-using-forged-authorization-data-attack"></a>Eskalace oprávnění prostřednictvím útoků založených na zfalšovaných datech autorizace

Eskalace oprávnění prostřednictvím útoků založených na zfalšovaných datech autorizace je postup, kterým útočník zneužije chyby zabezpečení certifikátu PAC ke zvýšení svých oprávnění v doménové struktuře nebo doméně služby Active Directory. K provedení tohoto útoku útočník musí:
-   Mít přihlašovací údaje k uživateli domény
-   Mít síťové připojení k řadiči domény, který se dá použít k ověření pomocí zcizených přihlašovacích údajů pro domény
-   Mít správné nástroje. Známým nástrojem, který zfalšuje certifikáty PAC, je Python Kerberos Exploitation Kit (PyKEK).

Pokud má útočník potřebné přihlašovací údaje a připojení, může pak změnit nebo zfalšovat certifikát PAC existujícího přihlašovacího tokenu uživatele Kerberosu (TGT). Útočník změní deklaraci členství skupiny, aby zahrnovala skupinu s vyšší úrovní oprávnění (třeba „Domain Administrators“ nebo „Enterprise Administrators“). Útočník pak upravený PAC přidá do lístku Kerberosu. Tento lístek Kerberosu se pak použije k vyžádání lístku služby z řadiče domény bez opravy zabezpečení. Útočník tak získá vyšší oprávnění v doméně a autorizaci k provádění akcí, které by provádět neměl. Útočník může předložit upravený přihlašovací token uživatele (TGT), aby získal přístup ke všem prostředkům v doméně vyžádáním tokenů přístupu k prostředkům (TGS). To znamená, že útočník může obejít všechny nakonfigurované seznamy ACL prostředků, které omezují přístup v síti, pomocí zfalšování autorizačních dat (PAC) pro libovolného uživatele v Active Directory.

## <a name="discovering-the-attack"></a>Zjištění útoku
Když se útočník pokusí zvýšit svá oprávnění, ATA to zjistí a označí jako upozornění s vysokou závažností.

![Podezřelá aktivita zfalšovaných certifikátů PAC](./media/forged-pac.png)

ATA v upozornění na podezřelou aktivitu označí, jestli byla eskalace oprávnění prostřednictvím zfalšovaných dat autorizace úspěšná nebo neúspěšná. Prověřit by se měla upozornění na úspěšné i neúspěšné útoky, protože neúspěšné pokusy můžou stále indikovat přítomnost útočníka ve vašem prostředí.

## <a name="investigating"></a>Prošetření
Po přijetí upozornění na eskalaci oprávnění prostřednictvím zfalšovaných dat autorizace v ATA musíte zjistit, co je třeba udělat ke zmírnění tohoto útoku. K tomu musíte nejdřív upozornění klasifikovat jako jedno z následujících: 
-   Pravdivě pozitivní: škodlivá akce zjištěná službou ATA
-   Falešně pozitivní: falešné upozornění – k eskalaci oprávnění prostřednictvím zfalšovaných dat autorizace ve skutečnosti nedošlo (jedná se o událost, kterou řešení ATA mylně považovalo za tento typ útoku)
-   Neškodné pravdivě pozitivní: akce zjištěná službou ATA, která je skutečná, ale není škodlivá, třeba test průniku

Následující schéma vám pomůže určit, které kroky byste měli provést:

![Diagram pro útoky v podobě zfalšovaných certifikátů PAC](./media/forged-pac-diagram.png)

1. Nejdříve zkontrolujte upozornění na časové ose útoku ATA, abyste zjistili, jestli byl pokus o zfalšovanou autorizaci úspěšný, neúspěšný nebo ve stadiu pokusu (pokusy o útoky jsou také neúspěšné útoky). Úspěšné a neúspěšné pokusy můžou vést k pravdivě pozitivnímu upozornění, ale s jinou závažností v rámci prostředí.
 
 ![Podezřelá aktivita zfalšovaných certifikátů PAC](./media/forged-pac-sa.png)


2.  Pokud byla detekovaná eskalace oprávnění prostřednictvím útoků založených na zfalšovaných datech autorizace úspěšná:
    -   Pokud má řadič domény, na kterém bylo upozornění vyvoláno, správně nainstalované opravy, jde o falešně pozitivní upozornění. V takovém případě byste měli upozornění zrušit a poslat týmu ATA na ATAEval@microsoft.com oznámení e-mailem, abychom mohli naše zjišťování stále zlepšovat. 
    -   Pokud řadič domény v upozornění nemá správné opravy:
        -   Pokud služba uvedená v upozornění nemá vlastní autorizační mechanismus, jde o pravdivě pozitivní upozornění a měli byste provést proces reagování na incidenty vaší organizace. 
        -   Pokud má služba uvedená v upozornění interní autorizační mechanismus, který vyžaduje data autorizace, může být falešně identifikovaná jako eskalace oprávnění prostřednictvím útoku založeného na zfalšovaných datech autorizace. 

3.  Pokud se zjištěný útok nezdařil:
    -   Pokud se ví, že operační systém aplikace upravuje PAC, pak jde pravděpodobně o neškodné pravdivě pozitivní upozornění a společně s vlastníkem aplikace nebo operačního systému byste toto chování měli opravit.

    -   Pokud není známo, že by operační systém nebo aplikace PAC upravovaly: 

        -   Pokud uvedená služba nemá vlastní autorizační službu, jde o pravdivě pozitivní upozornění a měli byste provést proces reagování na incidenty vaší organizace. I když se útočníkovi svá oprávnění v doméně zvýšit nepodařilo, můžete předpokládat, že se ve vaší síti útočník nachází, a měli byste ho co nejrychleji najít, než se pokusí svá oprávnění zvýšit jinými známými pokročilými vytrvalými útoky. 
        -   Pokud má služba uvedená v upozornění svůj vlastní autorizační mechanismus, který vyžaduje data autorizace, může být falešně identifikovaná jako eskalace oprávnění prostřednictvím útoku založeného na zfalšovaných datech autorizace.

## <a name="post-investigation"></a>Následné prošetření
Microsoft doporučuje využívat profesionální tým Incident Response & Recovery, který můžete kontaktovat prostřednictvím svého týmu účtu Microsoft, aby vám pomohl zjistit, jestli útočník ve vaší síti nenasadil vytrvalé metody.


## <a name="mitigation"></a>Zmírnění dopadů

Použijte bulletiny zabezpečení [MS14-068](https://technet.microsoft.com/library/security/MS14-068.aspx) a [MS11-013](https://technet.microsoft.com/library/security/ms11-013.aspx), které řeší chyby zabezpečení v KDC protokolu Kerberos. 


## <a name="see-also"></a>Viz také
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
