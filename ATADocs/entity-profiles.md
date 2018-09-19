---
title: Práce s profily entit v konzole Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje, jak zkoumat entity z obrazovky uživatelské profily v konzole ATA
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 581a3257-32dc-453f-b84e-b9f99186f5d3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a34d25e59183e496350216f5d3043430cd65bca6
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133445"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="investigating-entity-profiles"></a>Zkoumání profily entit

Profil entity obsahuje, můžete s řídicím panelem určená pro celý podrobný rozbor šetření uživatelů, počítačů, zařízení a prostředky, které mají přístup k a jejich historie. Na stránce Profil využívá nové translator logické aktivity ATA, která může podívat na skupinu aktivit, ke kterým dochází (souhrn až minutu) a seskupovat je do jedné logické aktivity umožňují lépe pochopit skutečné aktivity vaší uživatelé.

Chcete-li získat přístup stránku profil entity, klikněte na název sady entit, jako je například uživatelské jméno na časové ose podezřelé aktivity.

V levé nabídce poskytuje všechny služby Active Directory informace k dispozici na entitu, e-mailovou adresu, domény, první zjištěný datum. Pokud je entita citlivé to zjistíte, proč. Například uživatel označené jako citlivé nebo člen citlivou skupinu?
Pokud je citlivé uživatele zobrazí ikonu v části uživatelské jméno.

## <a name="view-entity-activities"></a>Zobrazení entity aktivity

Zobrazit všechny aktivity prováděné uživateli, nebo provést u entity, klikněte na **aktivity** kartu. 

 ![aktivity profilu uživatele](media/user-profile-activities.png)

Ve výchozím nastavení zobrazí v hlavním podokně profil entity časové osy aktivity entity s historií až 6 měsíců zpět, ze kterého můžete také přecházet do entity přistupovat uživatelem nebo pro entity, uživatelé, kteří přístup entity.

V horní části stránky můžete zobrazit souhrn dlaždic, které získáte rychlý přehled toho, co je potřeba pochopit v přehledu o vaší entity. Tyto dlaždice, které se mění v závislosti na jaký typ entity pro uživatele, se zobrazí:
- Kolik otevřených podezřelé aktivity, které jsou pro uživatele
- Kolik počítačů přihlášený uživatel
- Kolik prostředků uživatele přístup
- Z umístění přihlášení do sítě VPN

  ![Nabídka entity](media/entity-menu.png)

Pro počítače se zobrazí:
- Kolik otevřených podezřelé aktivity, které jsou pro počítač
- Kolik uživatelů přihlášení na počítači
- Kolik prostředků získat přístup k počítači
- Kolik umístění sítě VPN se použila v počítači
- Seznam IP adres počítače, z nichž se používá.

  ![počítač nabídky entity](media/entity-computer.png)

Použití **filtrovat podle** tlačítko nad časové osy aktivity můžete filtrovat aktivity podle typu aktivity. Můžete také filtrovat konkrétní (hlučného) typu aktivity. To je velmi užitečné pro zkoumání, pokud chcete pochopit základy toho, co dělá entity v síti. Můžete také přejít na konkrétní datum a jak jsou vyfiltrovaná do aplikace Excel můžete exportovat aktivity. Exportovaný soubor obsahuje stránky pro změny v adresáři služby (věci, které se změnily v Active Directory pro účet) a samostatnou stránku aktivity. 

## <a name="view-directory-data"></a>Zobrazení dat adresáře

**Data adresáře** karta obsahuje statické informace, které jsou k dispozici ze služby Active Directory, včetně příznaky zabezpečení ovládacích prvků přístupu uživatele. ATA také zobrazí členství ve skupinách pro uživatele, takže můžete říct, jestli má uživatel přímého členství nebo rekurzivní členství. U skupin ATA uvádí členy skupiny.

 ![adresář data uživatelského profilu](media/user-profile-dir-data.png)

V **řízení uživatelských účtů** části ATA poskytuje informace nastavení zabezpečení, které může být nutné vaše attentions. Můžete zobrazit důležité příznaky informace o uživateli, jako je můžete uživatele stisknutím klávesy enter obejít heslo, uživatel nemá heslo, které je platné stále atd. 

## <a name="view-lateral-movement-paths"></a>Zobrazení cesty taktiky Lateral Movement

Kliknutím **laterální pohyb cesty** kartě se zobrazí plně dynamického a kliknout, čímž mapu, která vám poskytne vizuální reprezentace cesty taktiky Lateral Movement do a z tohoto uživatele, které je možné na míru vaší sítě.

Mapa vám poskytne přehled o tom, kolik segmentů směrování mezi počítači nebo uživatelé útočník bude mít do a z tohoto uživatele k ohrožení citlivých účtů a pokud uživatel sami má citlivých účtů, uvidíte, kolik prostředky a účty jsou přímo připojení. Další informace najdete v tématu [laterální pohyb cesty](use-case-lateral-movement-path.md). 

 ![cesty taktiky Lateral Movement profilu uživatele](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>Viz také
[Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
