---
title: Instalace Azure Advanced Threat Protection – krok 1 | Dokumentace Microsoftu
description: Prvním krokem k instalaci služby Azure ATP zahrnuje vytvoření instance pro nasazení služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8a6238b6d3cd05c3896b88701c15d17404db43cf
ms.sourcegitcommit: 04ed0b9faf72d82cd10bf84efd9dc5aa525be212
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/03/2018
ms.locfileid: "48245345"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>Vytvoření pracovního prostoru na portálu ochrany ATP v programu Azure pracovní prostor Správa – krok 1

> [!div class="step-by-step"]
> [Krok 2 »](install-atp-step2.md)

Tento instalační postup uvádí pokyny k vytváření a správa vaší instance služby Azure ATP. Informace o architektuře ochrany ATP v programu Azure najdete v tématu [architektura služby Azure ATP](atp-architecture.md).

V ochraně ATP v Azure budete mít jeden pracovní prostor nebo instance umožňuje spravovat několik doménových struktur v podokně ze skla. 

> [!NOTE]
> V současné době datová centra ochrany ATP v programu Azure se nasazují do Evropy a Asie a Severní Amerika/střední Amerika/Karibská oblast.

## <a name="step-1-enter-the-management-portal"></a>Krok 1: Zadejte na portálu pro správu

Po ověření, že senzor požadavkům vaší sítě můžete vytvořit pracovní prostor služby Azure ATP.

> [!NOTE]
>Aby bylo možné získat přístup k portálu pro správu, musíte být globálním správcem nebo správcem zabezpečení v tomto tenantovi.


1.  Zadejte [ochrany ATP v programu Azure portal](https://portal.atp.azure.com).

2.  Přihlaste se pomocí uživatelského účtu Azure Active Directory.

## <a name="step-2-create-your-workspace"></a>Krok 2: Vytvoření pracovního prostoru

1. Klikněte na tlačítko **vytvořit pracovní prostor**.

2. V **vytvořit nový pracovní prostor** dialogové okno, zadejte název pracovního prostoru a vyberte **informace o zeměpisné poloze** pro vaše datové centrum. Váš pracovní prostor je **primární** ve výchozím nastavení. 
 > [!NOTE]
 > Po výběru informace o zeměpisné poloze už ho nelze změnit.
    ![Pracovní prostor Azure ATP](media/create-workspace.png)

3. Můžete kliknout **role uživatel spravovat Azure ATP** odkaz pro přímý přístup k [centra pro správu Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) a spravovat skupiny rolí.

 > [!NOTE]
 > Na úspěšně přihlášení do služby Azure ATP, budete muset přihlásit jako uživatel, který byl přiřazen správné roli ochrany ATP v programu Azure pro přístup k portálu ochrany ATP v programu Azure pracovní prostor. Další informace o řízení přístupu na základě role (RBAC) v ochrany ATP v programu Azure najdete v tématu [práce se skupinami rolí služby Azure ATP](atp-role-groups.md).

4. Klikněte na název pracovního prostoru pro přístup k portálu ochrany ATP v programu Azure pracovní prostor.

    ![Pracovní prostory Azure ATP](media/atp-workspaces.png)

- Jenom primární pracovní prostor se dá upravit. Pokud chcete odstranit aktivního pracovního prostoru, je nutné nejprve vypnout integrace dřív, než bude možné odstranit.

- Uchovávání dat – dříve odstraněné pracovní prostory se nezobrazí v uživatelském rozhraní. Další informace o uchovávání dat ochrany ATP v programu Azure najdete v tématu [ochrany ATP v programu Azure dat zabezpečení a ochrana osobních údajů](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[« Předinstalace](atp-prerequisites.md)
[Krok 2 »](install-atp-step2.md)



## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum ochrany ATP v programu.](https://aka.ms/azureatpcommunity)
