---
title: Vytvoření instance quickstart vaší ochrany ATP v programu Azure | Dokumentace Microsoftu
description: Rychlý start k vytvoření instance pro vaše nasazení služby Azure ATP, což je prvním krokem k instalaci služby Azure ATP.
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 02/05/2019
ms.topic: quickstart
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6a8c8458274243d254198914cb7339893a8d890b
ms.sourcegitcommit: 96752da28f43896e7b8e5945947b32c4810bdff6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/07/2019
ms.locfileid: "55831493"
---
# <a name="quickstart-create-your-azure-atp-instance"></a>Rychlý start: Vytvoření instance služby Azure ATP

V tomto rychlém startu vytvoříte instanci služby Azure ATP na portálu ochrany ATP v programu Azure. V ochraně ATP v Azure budete mít jednu instanci, dříve označované jako pracovní prostor. Jedna instance umožňuje spravovat několik doménových struktur v podokně ze skla.

> [!IMPORTANT]
> V současné době datová centra ochrany ATP v programu Azure se nasazují do Evropy a Asie a Severní Amerika/střední Amerika/Karibská oblast. Vaše instance se automaticky vytvoří v datovém centru, který je geograficky nejblíže k Azure Active Directory (Azure AD). Po vytvoření, Azure ATP instancí nejsou přesouvatelný.

## <a name="prerequisites"></a>Požadavky

- [Licencí Azure ATP](atp-technical-faq.md#licensing-and-privacy).
- Musíte být [globálním správcem nebo správcem zabezpečení u klienta](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#available-roles) pro přístup k portálu ochrany ATP v programu Azure.
- Zkontrolujte [architektura služby Azure ATP](atp-architecture.md) článku.
- Zkontrolujte [požadavky služby Azure ATP](atp-prerequisites.md) článku. 

## <a name="sign-in-to-the-azure-atp-portal"></a>Přihlaste se k portálu služby Azure ATP

Po ověření, že vaši síť splňuje požadavky senzoru spusťte vytváření vaší instance služby Azure ATP.

1. Přejděte na [ochrany ATP v programu Azure portal](https://portal.atp.azure.com).

2. Přihlaste se pomocí uživatelského účtu Azure Active Directory.

## <a name="create-your-instance"></a>Vytvoření instance

1. Klikněte na tlačítko **vytvořit instanci**. 

    ![Vytvoření instance služby Azure ATP](media/create-instance.png)

2. Vaše instance služby Azure ATP je automaticky názvem počáteční doména služby Azure AD a vytvořit v datovém centru umístěné nejblíž k Azure AD. 

    ![Vytvoření instance Azure](media/instance-created.png)

    > [!NOTE]
    > K přihlášení do služby Azure ATP budete potřebovat k přihlášení pomocí pověření uživatele, přiřazenou roli služby Azure ATP s oprávněními pro přístup k portálu ochrany ATP v programu Azure. Další informace o řízení přístupu na základě role (RBAC) v ochrany ATP v programu Azure najdete v tématu [práce se skupinami rolí služby Azure ATP](atp-role-groups.md).
 
3. Klikněte na tlačítko **konfigurace**, **spravovat skupiny rolí**a použít [centra pro správu Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal) odkaz ke správě skupin rolí.

    ![Správa skupin rolí](media/creation-manage-role-groups.png)

- Uchovávání dat – dřív Odstraněná instance služby Azure ATP nejsou zobrazeny v uživatelském rozhraní. Další informace o uchovávání dat ochrany ATP v programu Azure najdete v tématu [ochrany ATP v programu Azure dat zabezpečení a ochrana osobních údajů](atp-privacy-compliance.md).

## <a name="next-steps"></a>Další postup

> [!div class="step-by-step"]
> [«Požadavky](atp-prerequisites.md)
> [krok 2 – Připojte se ke službě Active Directory»](install-atp-step2.md)

## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://aka.ms/azureatpcommunity) ještě dnes!

