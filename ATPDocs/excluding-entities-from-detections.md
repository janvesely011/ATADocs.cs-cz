---
title: Vyloučení entit z detekce ve službě Azure Advanced Threat Protection | Dokumentace Microsoftu
description: Popisuje, jak zastavit zjišťování aktivit konkrétních entit jako podezřelých služby Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/11/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: cae3ed45-8fbc-4f25-ba24-3cc407c6ea93
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 77c85c161ac3a62f67a1bc0983544f6dcef5e596
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196966"
---
# <a name="excluding-entities-from-detections"></a>Vyloučení entit z detekce
Tento článek vysvětluje, jak vyloučení entit, která aktivuje upozornění. Některé entity budou vyloučeny, chcete-li minimalizovat neškodné pravdivě pozitivní během provádění, je možné zachytit pravdivě pozitivní. Pokud chcete zabránit vytvoření šumu o aktivitách, které určitých uživatelů, může být součástí vaší běžné podnikové činnosti ochrany ATP v programu Azure, můžete potlačit – nebo vyloučit – konkrétní entity nemají vyvolávat výstrahy. Kromě toho jsou vyloučeny některé oblíbené entity ve výchozím nastavení. 

Například pokud máte kontrolu zabezpečení, která provádí rekognoskaci DNS, nebo správce, který spouští na dálku skripty na řadiči domény – a jedná se o schválené aktivity, jehož cílem je součástí normálního provozu IT ve vaší organizaci, ty můžete vyloučit. Další informace o jednotlivých detekci ochrany ATP v programu Azure vám pomohou rozhodnout entit, které chcete vyloučit, najdete v článku [výstraha zabezpečení průvodce](suspicious-activity-guide.md).

## <a name="entities-excluded-by-default-from-raising-alerts"></a>Ve výchozím nastavení nemají vyvolávat výstrahy vyloučit entity
 Pro některé výstrahy, jako například **podezřelá komunikace prostřednictvím DNS**, domény Automatická vyloučení jsou přidány pomocí služby Azure ATP na základě zpětné vazby od zákazníků a výzkumu. 
 
![Podezřelá komunikace prostřednictvím DNS automatické vyloučení](./media/dns-auto-exclusions.png) 

## <a name="exclude-entities-from-raising-alerts"></a>Vyloučit entity nemají vyvolávat výstrahy

Existují dva způsoby, jak můžete ručně vyloučit entity, přímo z dané výstraze zabezpečení nebo z **vyloučení** kartě **konfigurace** stránky. 

- **Z dané výstraze zabezpečení**: V časové osy aktivity, když obdržíte výstrahu týkající se aktivity uživatele, počítače nebo IP adresy, které jsou **je** povoleno určitou aktivitu a můžou Uděláte to tak často, proveďte následující:
  - Klikněte pravým tlačítkem na tři tečky na konci řádku pro dané výstraze zabezpečení na dané entitě a vyberte **zavřít a vyloučit**. Tím přidáte uživatele, počítače nebo IP adresu do seznamu vyloučení pro tuto výstrahu zabezpečení. Zavření výstrahy zabezpečení a upozornění už není uvedený v **otevřít** v seznamu událostí **výstrah časová osa**.

    ![Vyloučení entity](./media/exclude-in-sa.png)

- **Na stránce konfigurace**:  Kontrola nebo úprava jakékoli vyloučení: v části **konfigurace**, klikněte na tlačítko **vyloučení** a pak vyberte příslušnou výstrahu zabezpečení použít vyloučení, jako například **rekognoskace DNS** .

    ![Konfigurace vyloučení](./media/exclusions.png)

Chcete-li přidat entitu z **vyloučení** konfigurace: Zadejte název entity, pak klikněte na tlačítko plus a pak klikněte na tlačítko **Uložit** v dolní části stránky.

Chcete-li odebrat entitu z **vyloučení** konfigurace: klikněte na minus vedle názvu entity a potom klikněte na **Uložit** v dolní části stránky.

Doporučujeme přidat vyloučení k detekcím až po získání výstrah tohoto konkrétního typu *a* určení, že se neškodné pravdivě pozitivní. 

> [!NOTE]
> Abychom vás ochránili, není možné nastavit vyloučení u všech detekcí. 

U některých detekcí jsou k dispozici tipy, které vám pomohou se rozhodnout, co chcete vyloučit. 

Každé vyloučení závisí na kontextu, v některých můžete nastavit uživatele a pro ostatní uživatele můžete nastavit počítače nebo IP adresy. 

Až budete mít možnost vyloučit IP adresu nebo počítač, můžete vyloučit jednu z nich – nemusíte zadávat obě dvě.

> [!NOTE]
> Konfigurační stránky lze upravit pouze správci služby Azure ATP.


## <a name="see-also"></a>Viz také

- [Příručka ke službě Azure ATP výstraha zabezpečení](suspicious-activity-guide.md)
- [Integraci se službou ochrana ATP v programu Windows Defender](integrate-wd-atp.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
