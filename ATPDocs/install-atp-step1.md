---
title: Nainstalovat Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Prvním krokem k instalaci služby Azure ATP zahrnuje vytvoření instance pro nasazení služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8cdb87bb577577f48b45e750f96159d008f72810
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/23/2019
ms.locfileid: "54458542"
---
# <a name="creating-your-azure-atp-instance-in-the-azure-atp-portal---step-1"></a>Vytvoření instance vaší ochrany ATP v programu Azure na portálu ochrany ATP v programu Azure – krok 1

> [!div class="step-by-step"]
> [Krok 2 »](install-atp-step2.md)

Tento instalační postup uvádí pokyny k vytváření a správa vaší instance služby Azure ATP (dříve označované jako pracovní prostor). Informace o architektuře ochrany ATP v programu Azure najdete v tématu [architektura služby Azure ATP](atp-architecture.md).

V ochraně ATP v Azure budete mít jednu instanci umožňuje spravovat několik doménových struktur v podokně ze skla. 

> [!NOTE]
> V současné době datová centra ochrany ATP v programu Azure se nasazují do Evropy a Asie a Severní Amerika/střední Amerika/Karibská oblast. Vaše instance se automaticky vytvoří v datovém centru, který je geograficky nejblíže k AAD. Po vytvoření, Azure instance ochrany ATP v programu nejsou přesouvatelný. 

## <a name="step-1-enter-the-azure-atp-portal"></a>Krok 1. Zadejte ochrany ATP v programu Azure portal

Po ověření, že vaši síť splňuje požadavky senzoru pokračujte ve vytváření vaší instance služby Azure ATP.

> [!NOTE]
>Musíte být globálním správcem nebo správcem zabezpečení u klienta pro přístup k portálu ochrany ATP v programu Azure.


1.  Zadejte [ochrany ATP v programu Azure portal](https://portal.atp.azure.com).

2.  Přihlaste se pomocí uživatelského účtu Azure Active Directory.

## <a name="step-2-create-your-instance"></a>Krok 2. Vytvoření instance

1. Klikněte na tlačítko **vytvořit instanci**. 

    ![Vytvoření instance služby Azure ATP](media/create-instance.png)

2. Vaše instance služby Azure ATP je automaticky názvem počáteční doména AAD a přidělená k datovému centru, které jsou umístěné nejblíž k AAD a vytvořili. 

    ![Vytvoření instance Azure](media/instance-created.png)

    > [!NOTE]
    > K přihlášení do služby Azure ATP, budete muset přihlásit jako uživatel přiřazenou roli služby Azure ATP s oprávněními pro přístup k portálu ochrany ATP v programu Azure. Další informace o řízení přístupu na základě role (RBAC) v ochrany ATP v programu Azure najdete v tématu [práce se skupinami rolí služby Azure ATP](atp-role-groups.md).
 
3. Klikněte na tlačítko **konfigurace**, **spravovat skupiny rolí**a použít [centra pro správu Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) odkaz ke správě skupin rolí. .

    ![Správa skupin rolí](media/creation-manage-role-groups.png)

- Uchovávání dat – dřív Odstraněná instance služby Azure ATP se nezobrazí v uživatelském rozhraní. Další informace o uchovávání dat ochrany ATP v programu Azure najdete v tématu [ochrany ATP v programu Azure dat zabezpečení a ochrana osobních údajů](atp-privacy-compliance.md).


>[!div class="step-by-step"]
[« Předinstalace](atp-prerequisites.md)
[Krok 2 »](install-atp-step2.md)



## <a name="see-also"></a>Viz také
- [Nástroje pro změnu velikosti Azure ATP](http://aka.ms/aatpsizingtool)
- [Konfigurace shromažďování událostí](configure-event-collection.md)
- [Požadavky služby Azure ATP](atp-prerequisites.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
