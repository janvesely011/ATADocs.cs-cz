---
title: Instalace Azure Advanced Threat Protection – krok 1 | Microsoft Docs
description: Prvním krokem k instalaci Azure ATP zahrnuje vytvoření pracovního prostoru pro vaše nasazení Azure ATP.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/10/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a4c2f03955eddb4615b347fa8a211501546e6f4a
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/16/2018
ms.locfileid: "31007266"
---
*Platí pro: Azure Advanced Threat Protection*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Vytváření pracovního prostoru na portálu správy Azure ATP prostoru – krok 1

>[!div class="step-by-step"]
[Krok 2 »](install-atp-step2.md)

Tento instalační postup uvádí pokyny k vytváření a správě pracovního prostoru v portálu pro správu Azure ATP pracovního prostoru. Informace na architektuře Azure ATP najdete v tématu [Azure ATP architektura](atp-architecture.md).

V Azure ATP máte možnost spravovat a sledovat více pracovní prostory. To je obzvláště užitečné, pokud chcete vytvořit pracovní prostor ukázku a testovací prostoru, ve kterém můžete POC Azure ATP před distribucí v celé organizaci. Také je potřeba pro podporu nasazení s více doménovými strukturami. Jednoho pracovního prostoru můžete monitorovat jenom několika domén z jedné doménové struktury. 

> [!NOTE]
> - Může mít maximálně dvě active pracovních prostorů. Po odstranění pracovního prostoru můžete kontaktovat podporu, aby jej znovu aktivovat. Můžete maximálně tři odstraněné pracovních prostorů. Chcete-li zvýšit počet uložené, odstraněné pracovní prostory, kontaktujte podporu Azure ATP.
> - V současné době datových centrech Azure ATP nasazených v Evropa, Severní Ameriku a střední Amerika nebo karibské a Asii.

## <a name="step-1-enter-the-workspace-management-portal"></a>Krok 1: Přejít na portál pro správu pracovního prostoru

Po ověření, že vaše síť splňuje požadavky na senzoru můžete pokračovat vytváření pracovního prostoru Azure ATP.

> [!NOTE]
>Chcete-li získat přístup k portálu pro správu pracovního prostoru, musíte být globální správce nebo správce zabezpečení na tohoto tenanta.


1.  Zadejte [na portálu Azure ATP prostoru](https://portal.atp.azure.com).

2.  Přihlaste se pomocí účtu uživatele Azure Active Directory.

## <a name="step-2-create-a-workspace"></a>Krok 2: Vytvořit pracovní prostor

1. Klikněte na tlačítko **vytvořit pracovní prostor**.

2. V **vytvořit nový pracovní prostor** dialogové okno, název pracovního prostoru, rozhodnout, zda je vaše primárním pracovním prostorem nebo Ne a vyberte **informace o zeměpisné poloze** pro datového centra. Pouze jednoho pracovního prostoru můžete nastavit jako primární. Nastavení pracovního prostoru, protože primární ovlivňuje integrace – Azure ATP lze pouze integrovat s Windows Defender ATP vašeho primární pracovního prostoru. Můžete změnit, které pracovní prostor je primární později, ale aby bylo možné provést, budete muset odebrat všechny integrace pro aktuální primární pracovní prostor již nastaven.
 > [!NOTE]
 > Vyberte informace o zeměpisné poloze a nelze jej upravovat.
    ![Azure ATP prostoru](media/create-workspace.png)

3. Můžete kliknout na **ATP Azure spravovat uživatelské role** odkaz přímý přístup k [centra pro správu Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) a Správa skupin role.

 > [!NOTE]
 > Chcete-li úspěšně přihlásit k Azure ATP, budete muset přihlásit jako uživatel, který byl přiřazen správné roli Azure ATP pro přístup k portálu Azure ATP pracovního prostoru. Další informace o řízení přístupu na základě role (RBAC) v Azure ATP najdete v tématu [práce se skupinami role Azure ATP](atp-role-groups.md).

4. Klikněte na název nového prostoru přístupu na portálu Azure ATP prostoru pracovního prostoru.

    ![Azure ATP pracovních prostorů](media/atp-workspaces.png)

- Můžete upravit pouze primárním pracovním prostorem. Provést změny jiných pracovních prostorech, můžete je odstranit a znovu přidejte. Pokud chcete odstranit primární pracovní prostor, musíte nejprve vypnout integrace a nastavit v pracovním prostoru neměla být **primární** předtím, než je možné odstranit.
- Chcete-li upravit primárním pracovním prostorem, musí nejprve vypnout existující integrace v pracovním prostoru.

- Uchovávání dat – odstraněné pracovní prostory se nezobrazí v uživatelském rozhraní, ale jejich data se uchovávají podle [zásad uchovávání dat Microsoft](https://www.microsoft.com/trustcenter/privacy/you-own-your-data).


>[!div class="step-by-step"]
[« Předinstalace](configure-port-mirroring.md)
[Krok 2 »](install-atp-step2.md)


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ATP!](https://aka.ms/azureatpcommunity)
