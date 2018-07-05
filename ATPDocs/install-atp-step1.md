---
title: Instalace Azure Advanced Threat Protection – krok 1 | Dokumentace Microsoftu
description: Prvním krokem k instalaci služby Azure ATP zahrnuje vytvoření pracovního prostoru pro vaše nasazení služby Azure ATP.
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
ms.openlocfilehash: cadd708c20733324b939db1e35d12aae3f2d80f2
ms.sourcegitcommit: 40dbce8045f689376a50275fb12e3c5c32ca8092
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/04/2018
ms.locfileid: "37799072"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Vytvoření pracovního prostoru na portálu ochrany ATP v programu Azure pracovní prostor Správa – krok 1

>[!div class="step-by-step"]
[Krok 2 »](install-atp-step2.md)

Tento instalační postup uvádí pokyny k vytváření a správa pracovního prostoru v portálu pro správu pracovního prostoru služby Azure ATP. Informace o architektuře ochrany ATP v programu Azure najdete v tématu [architektura služby Azure ATP](atp-architecture.md).

V ochraně ATP v Azure máte možnost spravovat a monitorovat víc pracovních prostorů. To je užitečné, pokud chcete vytvořit pracovní prostor ukázku a pracovní prostor testu, ve kterém můžete ochrany ATP v programu Azure POC před distribucí v celé organizaci. To je taky potřeba pro podporu nasazení s více doménovými strukturami. Jeden pracovní prostor můžete monitorovat pouze několika domén z jedné doménové struktury. 

> [!NOTE]
> V současné době datová centra ochrany ATP v programu Azure se nasazují do Evropy a Asie a Severní Amerika/střední Amerika/Karibská oblast.

## <a name="step-1-enter-the-workspace-management-portal"></a>Krok 1: Zadejte na portálu pro správu pracovního prostoru

Po ověření, že senzor požadavkům vaší sítě můžete vytvořit pracovní prostor služby Azure ATP.

> [!NOTE]
>Aby bylo možné získat přístup k portálu pro správu pracovního prostoru, musíte být globálním správcem nebo správcem zabezpečení v tomto tenantovi.


1.  Zadejte [portálu pracovního prostoru služby Azure ATP](https://portal.atp.azure.com).

2.  Přihlaste se pomocí uživatelského účtu Azure Active Directory.

## <a name="step-2-create-a-workspace"></a>Krok 2: Vytvoření pracovního prostoru

1. Klikněte na tlačítko **vytvořit pracovní prostor**.

2. V **vytvořit nový pracovní prostor** dialogového okna, název pracovního prostoru, rozhodnout, zda je vaše primární pracovní prostor nebo Ne a vyberte **informace o zeměpisné poloze** pro vaše datové centrum. Jenom jeden pracovní prostor je možné nastavit jako primární. Nastavení pracovního prostoru jako primární ovlivňuje integrace – můžete pouze integrovat služby Azure ATP ochrany ATP v programu Windows Defender pro váš primární pracovní prostor. Můžete změnit, který pracovní prostor je primární později, ale aby bylo možné provést, je třeba odstranit všechny integrace pro aktuální primární pracovní prostor již nastaven.
 > [!NOTE]
 > Po výběru informace o zeměpisné poloze už ho nelze změnit.
    ![Pracovní prostor Azure ATP](media/create-workspace.png)

3. Můžete kliknout **role uživatel spravovat Azure ATP** odkaz pro přímý přístup k [centra pro správu Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) a spravovat skupiny rolí.

 > [!NOTE]
 > Na úspěšně přihlášení do služby Azure ATP, budete muset přihlásit jako uživatel, který byl přiřazen správné roli ochrany ATP v programu Azure pro přístup k portálu ochrany ATP v programu Azure pracovní prostor. Další informace o řízení přístupu na základě role (RBAC) v ochrany ATP v programu Azure najdete v tématu [práce se skupinami rolí služby Azure ATP](atp-role-groups.md).

4. Klikněte na název nového pracovního prostoru přístup portálu pracovního prostoru ochrana ATP v programu Azure pro tento pracovní prostor.

    ![Pracovní prostory Azure ATP](media/atp-workspaces.png)

- Jenom primární pracovní prostor se dá upravit. Provádět změny jiných pracovních prostorů, můžete je odstranit a znovu přidat. Pokud chcete odstranit primární pracovní prostor, musíte vypnout integrace a nastavit pracovní prostor tak, aby nebyl **primární** dřív, než bude možné odstranit.
- Upravit primární pracovní prostor, musíte nejdřív vypnout existující integrace v pracovním prostoru.

- Uchovávání dat – odstraněný pracovní prostory se nezobrazí v uživatelském rozhraní. Další informace o uchovávání dat ochrany ATP v programu Azure najdete v tématu [ochrany ATP v programu Azure dat zabezpečení a ochrana osobních údajů](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[« Předinstalace](configure-port-mirroring.md)
[Krok 2 »](install-atp-step2.md)


## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
