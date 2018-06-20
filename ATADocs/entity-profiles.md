---
title: Práce s profily entit v konzole Advanced Threat Analytics | Microsoft Docs
description: Popisuje, jak prozkoumat entity na obrazovce uživatelské profily v konzole ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 581a3257-32dc-453f-b84e-b9f99186f5d3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f2fd6f28eb6bf11aa3705f5320fcdae01d02f6d0
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/28/2018
ms.locfileid: "30202312"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="investigating-entity-profiles"></a>Zkoumání profily entit

Profil entity slouží k dispozici řídicí panel určený pro úplné přímým – podrobnější prošetření uživatelů, počítačů, zařízení a prostředky, které mají přístup a jejich historii. Stránka profilu využívá výhod nového překladač logické aktivity ATA, který můžete prohlížet skupinu aktivit, ke kterým dochází (agregovat až několik minut) a seskupovat je do jedné logické aktivity umožňují lépe porozumět skutečné aktivity vašeho uživatelé.

Pro přístup k stránku profil entity, klikněte na název entity, jako je například uživatelské jméno v časové osy podezřelých aktivit.

V levé nabídce poskytuje všechny služby Active Directory informace k dispozici u entity - e-mailovou adresu, domény, první zobrazené datum. Pokud je entita citlivé oznámí, proč. Například je uživatel označené jako velká a malá písmena nebo člen skupiny citlivé?
Pokud je uživatel citlivé uvidíte na ikonu v části uživatelské jméno.

## <a name="view-entity-activities"></a>Zobrazit entity aktivity

Zobrazit všechny aktivity prováděné uživateli nebo provést s entitou, klikněte na **aktivity** kartě. 

 ![aktivity profilu uživatele](media/user-profile-activities.png)

Ve výchozím nastavení zobrazí hlavním podokně profilu entity termín entity aktivit s historii až 6 měsíců zpět, ze kterého můžete také přejít dolů do entity přístupu uživatelem, nebo pro entity, uživatelé, kteří přístup entity.

V horní části můžete zobrazit souhrn dlaždice, které získáte rychlý přehled toho, co je potřeba pochopit v přehledu o entitě. Tyto dlaždice, které se mění v závislosti na co typ entity, pro uživatele, zobrazí se:
- Kolik otevřete podezřelé aktivity, které jsou pro uživatele
- Kolik počítačů přihlášený uživatel
- Tom, kolik prostředků uživatele přístup
- Z umístění, které uživatel přihlášen do sítě VPN

  ![entity nabídky](media/entity-menu.png)

Pro počítače se zobrazí:
- Kolik otevřete podezřelé aktivity, které jsou pro počítač
- Počet uživatelů, kteří se protokolují do počítače
- Tom, kolik prostředků získat přístup k počítači
- Kolik umístění sítě VPN byl získat přístup z počítače
- Seznam IP adres počítače, které se používá.

  ![počítač nabídky entity](media/entity-computer.png)

Pomocí **filtrovat podle** tlačítko výše časové ose aktivity můžete filtrovat aktivity podle typu aktivity. Můžete také filtrovat na konkrétní (aktivní) typ aktivity. To je velmi užitečné pro šetření, když chcete pochopit základy toho, co je to entity v síti. Můžete také přejít na určité datum a aktivity můžete exportovat jako filtruje tak, aby aplikace Excel. Exportovaný soubor obsahuje na stránce pro změny directory services (věcí, které změnily ve službě Active Directory pro účet) a samostatné stránce pro aktivity. 

## <a name="view-directory-data"></a>Zobrazení dat adresáře

**Dat adresáře** karta poskytuje statické informace, které jsou k dispozici ze služby Active Directory, včetně příznaky zabezpečení ovládacích prvků přístupu uživatele. ATA také zobrazuje členství ve skupinách pro uživatele tak, aby se dá zjistit, jestli má uživatel přímé členství nebo rekurzivní členství. Pro skupiny ATA uvádí členy skupiny.

 ![data uživatelského profilu adresáře](media/user-profile-dir-data.png)

V **řízení přístupu uživatelů** části ATA poskytuje nastavení zabezpečení, které může být nutné vaše attentions. Uvidíte důležité příznaky o uživateli, například můžete stiskněte klávesu uživatele zadejte obejít heslo, uživatel nemá heslo, které je platné stále atd. 

## <a name="view-lateral-movement-paths"></a>Zobrazení laterální pohyb cesty

Kliknutím **pomoci odhalit laterální pohyb cesty** si můžete prohlédnout plně dynamické a můžete kliknout mapování, které vám poskytne vizuální reprezentace cesty laterální pohyb do a z tohoto uživatele, který slouží k proniknout vaší sítě.

Mapy vám poskytne seznam o tom, kolik segmentů směrování mezi počítači, nebo by mají uživatelé na útočník do a z tohoto uživatele k ohrožení citlivých účet a pokud uživatel sami má citlivé účet, můžete podívat, kolik prostředků a účty jsou přímo připojení. Další informace najdete v tématu [pomoci odhalit laterální pohyb cesty](use-case-lateral-movement-path.md). 

 ![cesty laterální pohyb profilu uživatele](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
