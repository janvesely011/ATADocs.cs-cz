---
title: Nainstalovat Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Prvním krokem k instalaci služby Azure ATP zahrnuje vytvoření instance pro nasazení služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/4/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 97cce3de3a1cbe049523c54901ecbc9228aaee53
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783006"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*


# <a name="creating-your-azure-atp-instance-in-the-portal---step-1"></a>Vytvoření instance vaší ochrany ATP v programu Azure na portálu – krok 1

> [!div class="step-by-step"]
> [Krok 2 »](install-atp-step2.md)

Tento instalační postup uvádí pokyny k vytváření a správa vaší instance služby Azure ATP nebo pracovního prostoru. Informace o architektuře ochrany ATP v programu Azure najdete v tématu [architektura služby Azure ATP](atp-architecture.md).

Ochrana ATP v programu Azure, budete mít v jedné instance nebo pracovní prostor umožňuje spravovat několik doménových struktur v podokně ze skla. 

> [!NOTE]
> V současné době datová centra ochrany ATP v programu Azure se nasazují do Evropy a Asie a Severní Amerika/střední Amerika/Karibská oblast.

## <a name="step-1-enter-the-azure-atp-portal"></a>Krok 1: Zadejte ochrany ATP v programu Azure portal

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
 > Na úspěšně přihlášení do služby Azure ATP, budete muset přihlásit jako uživatel, který byl přiřazen správné roli ochrany ATP v programu Azure pro přístup k portálu ochrany ATP v programu Azure. Další informace o řízení přístupu na základě role (RBAC) v ochrany ATP v programu Azure najdete v tématu [práce se skupinami rolí služby Azure ATP](atp-role-groups.md).

4. Klikněte na název pracovního prostoru pro přístup k portálu ochrany ATP v programu Azure.

    ![Pracovní prostory Azure ATP](media/atp-workspaces.png)

- Jenom primární pracovní prostor se dá upravit. Pokud chcete odstranit primární pracovní prostor, je nutné nejprve vypnout integrace dřív, než bude možné odstranit.

- Uchovávání dat – dříve odstraněné pracovní prostory se nezobrazí v uživatelském rozhraní. Další informace o uchovávání dat ochrany ATP v programu Azure najdete v tématu [ochrany ATP v programu Azure dat zabezpečení a ochrana osobních údajů](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[« Předinstalace](atp-prerequisites.md)
[Krok 2 »](install-atp-step2.md)



## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
