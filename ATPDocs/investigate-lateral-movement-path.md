---
title: Zkoumání cest po přesunu s využitím Azure ATP | Microsoft Docs
description: Tento článek popisuje, jak zjistit a prozkoumat potenciální útoky na přenosové cesty pomocí Azure Advanced Threat Protection (ATP).
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9295dc09-ecdb-44c0-906b-cba4c5c8f17c
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3428a95fd77252bf7384c8e733842134bc8141d2
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/15/2019
ms.locfileid: "71004734"
---
# <a name="tutorial-use-lateral-movement-paths-lmps"></a>Návodu Použít cesty bočního pohybu (LMPs)

> [!NOTE]
> Funkce ATP Azure, které jsou na této stránce popsané, jsou dostupné taky pomocí nového [portálu](https://portal.cloudappsecurity.com).

Útoky na boční pohyb se obvykle dosahují pomocí řady různých technik. Některé z nejoblíbenějších metod používaných útočníky jsou [odcizení přihlašovacích údajů](suspicious-activity-guide.md#) a [předávali útoky na lístky](suspicious-activity-guide.md) . V obou metodách útočníci necitlivých účtů využívají necitlivé počítače, které sdílejí uložené přihlašovací údaje v účtech, skupinách a počítačích s citlivými účty.

V tomto kurzu se naučíte, jak používat Azure ATP LMPs k [prozkoumání](#investigate) potenciálních cest k pohybu a společně s výstrahami zabezpečení ATP Azure. získáte lepší informace o tom, co se stalo ve vaší síti a jak. Kromě toho se naučíte, jak pomocí [sestavy LMP k citlivým](#discover-your-at-risk-sensitive-accounts) účtům zjistit všechny citlivé účty s možnými případnými možnostmi pohybu ve vaší síti podle časového období.

> [!div class="checklist"]
> * Prozkoumat LMPs
> * Zjištění citlivých účtů na riziko
> * Přístup k **přepravním cestám k sestavě citlivých účtů**


## <a name="investigate"></a>Prošetření

Existuje několik způsobů, jak použít a prozkoumat LMPs. Na portálu Azure ATP Najděte entitu a pak ji Prozkoumejte podle cesty nebo aktivity.

1. Na portálu vyhledejte uživatele nebo počítač. Všimněte si, že se v profilu entity přidala Boční Poznámka k pohybu. Označení se zobrazí pouze v případě, že je entita zjištěna v potenciálním LMP během posledních 48 hodin.  

   ![boční ikona](./media/lateral-movement-icon.png) or ![ikona cesty](./media/paths-icon.png).

2. Na stránce profil uživatele, který se otevře, klikněte na kartu **cesty přesunu** .

   ![Karta pro cestu k bočnímu pohybu Azure ATP (LMP)](./media/lateral-movement-path-tab.png)

3. Zobrazený graf poskytuje mapu možných cest k citlivým uživatelům během doby 48. Pokud během posledních dvou dnů nebyla zjištěna žádná aktivita, graf se nezobrazí. Chcete-li zobrazit graf pro vyhledávání předchozích cest k pohybu pro danou entitu, použijte možnost **zobrazit jinou možnost data** .

   ![LMP zobrazení jiného data](./media/atp-view-different-date.png)

4. V grafu si můžete přečíst, co se dozvíte o expozici přihlašovacích údajů citlivých uživatelů. Například v cestě použijte šedé šipky **přihlášené** k zobrazení, abyste viděli, kde se v rámci svých privilegovaných přihlašovacích údajů přihlásila Přezdívka. V tomto případě byly uloženy citlivé přihlašovací údaje v počítači SHAREPOINT – SRV. Nyní si všimněte, k jakým uživatelům se přihlásili, které počítače vytvářely nejvíce pro vystavení a ohrožení zabezpečení. Podívejte se na to tak, že si prohlížíte na černé šipky **správce** a zjistíte, kdo má pro daný prostředek oprávnění správce. V tomto příkladu má každý z HelpDesku skupiny možnost získat přístup k přihlašovacím údajům uživatele z daného prostředku.  

   ![Cesta k postrannímu pohybu Azure ATP (LMP)](./media/atp-lmp.png)

## <a name="discover-your-at-risk-sensitive-accounts"></a>Zjištění citlivých účtů v nebezpečí

Při zjišťování všech citlivých účtů ve vaší síti, které jsou vystavené z důvodu jejich připojení k necitlivým účtům, skupinám a počítačům v cestách pohybu, postupujte podle těchto kroků. 

1. V nabídce portálu Azure ATP klikněte na ikonu sestavy. ![ikona sestav](./media/atp-report-icon.png).

2. V rámci cest přenosů **citlivých na citlivé účty**nejsou v případě, že se nenašly žádné možnosti bočních cest pohybu, sestava šedá. Pokud jsou k dispozici možné cesty bočního pohybu, sestava automaticky vybere první datum, kdy jsou relevantní data. Sestava cesty bočního pohybu poskytuje data po dobu až 60 dnů.

   ![sestavy](./media/reports.png)

3. Klikněte na tlačítko **Stáhnout**.

4. Vytvoří se excelový soubor, který poskytuje podrobné informace o potenciálních cestách přesunu a citlivých účtech pro vybraná data. Karta **Souhrn** poskytuje grafy, které podrobně popisují počet citlivých účtů, počítačů a průměry pro přístup s rizikem. Karta **Podrobnosti** poskytuje seznam citlivých účtů, které byste měli prozkoumat.

## <a name="schedule-report"></a>Naplánovat sestavu

Pohyb na sestavu citlivý účet lze také naplánovat pomocí funkce nastavit naplánované sestavy.

Všimněte si, že vlastní LMPs popsané v sestavě ke stažení již nemusí být k dispozici, protože byly zjištěny v minulosti a mohly být změněny, upraveny nebo opraveny od jejich zjištění.

Pokud si chcete prohlédnout historické LMPs, vyberte v kalendáři při vytváření sestavy jiná dostupná data.

## <a name="next-steps"></a>Další postup

V tomto kurzu jste se naučili, jak pomocí LMPs prozkoumat podezřelé aktivity. Pokud chcete získat další informace o entitách, které jsou součástí LMPs, přejděte k kurzu prozkoumat entity.
> [!div class="nextstepaction"]
> [Prošetřování entit](investigate-entity.md)

## <a name="see-also"></a>Viz také

- [Porozumění cestám k příčnému pohybu Azure ATP](use-case-lateral-movement-path.md)
- [Konfigurace služby Azure ATP pro vzdálená volání do SAM](install-atp-step8-samr.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
