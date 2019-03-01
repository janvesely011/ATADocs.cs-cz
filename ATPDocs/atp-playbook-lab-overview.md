---
title: Výstraha zabezpečení ochrany ATP v programu testovacího prostředí kurz Přehled služby Azure | Dokumentace Microsoftu
description: Tento kurz přehled popisuje čtyři části výstraha zabezpečení Azure ochrany ATP v programu testovacího prostředí pro simulaci hrozeb pro zjišťování pomocí služby Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: tutorial
author: mlottner
ms.author: mlottner
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: 116f4648026d8f291a1576bb0cbd4bf392ff8a9a
ms.sourcegitcommit: 8681c4ed6ede58ace737f31eeff9a680b8e4256d
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/28/2019
ms.locfileid: "57007445"
---
# <a name="tutorial-overview-atp-security-alert-lab"></a>Přehled kurzu: Ochrana ATP v programu testovacího prostředí výstrahy zabezpečení

Účelem tohoto kurzu výstraha zabezpečení Azure ochrany ATP v programu testovacího prostředí je ilustrovat **ochrany ATP v programu Azure**možnosti v identifikace a detekce podezřelých aktivit a potenciální útoky na vaší síti. V tomto kurzu čtyři části vysvětluje, jak nainstalovat a nakonfigurovat pracovní prostředí pro testování proti některé služby Azure ATP *diskrétní* detekcí. Toto testovací prostředí se zaměřuje na služby Azure ATP *podpis*– na základě funkcí. Testovací prostředí není zahrnují rozšířené strojové učení a uživatele nebo na základě entity behaviorální způsoby detekování, protože tyto detekce vyžadují období učení s skutečné síťový provoz až po dobu 30 dnů.

## <a name="lab-setup"></a>Nastavení testovacího prostředí

Z prvního kurzu této seriál vás provede vytvořením testovacího prostředí pro testování diskrétní detekce služby Azure ATP. Tento kurz zahrnuje informace o počítačích, uživatelích a nástroje, které jsou potřebné k nastavení testovacího prostředí a dokončete její playbooky. Pokyny předpokládají, že se že vám bude vyhovovat nastavení řadiče domény a pracovní stanice pro použití testovacího prostředí společně s další úlohy správy. Čím blíž testovacího prostředí je nastavení navrhované testovacího prostředí, tím snazší bude dodržovat testovacích postupů ochrany ATP v Azure. Po dokončení nastavení testovacího prostředí se použijte pro testování výstraha zabezpečení Azure ATP playbooky.

> [!div class="nextstepaction"]
> [Instalační program ochrany ATP v programu testovacího prostředí výstrahy zabezpečení](atp-playbook-setup-lab.md)

## <a name="reconnaissance-playbook"></a>Rekognoskace playbook

Druhé části kurzu této série čtyř částí je playbook rekognoskace. Aktivity rekognoskace umožnit, aby Seznamte se podrobně a dokončete mapování prostředí pro pozdější použití. Playbook jsou uvedeny některé funkce služby Azure ATP při identifikaci a detekci podezřelých aktivit potenciální útoky pomocí příkladů z běžných, která je veřejně dostupná hackerů a útoku nástroje.

> [!div class="nextstepaction"]
> [Rekognoskace playbook](atp-playbook-reconnaissance.md)


## <a name="lateral-movement-playbook"></a>Playbook taktiky Lateral Movement

Playbook taktiky Lateral Movement je třetí nástroj v čtyř částí série. Taktiky Lateral Movement vyrábí celá útočník při pokusu o získání dominance v doméně. Spuštění playbook uvidíte detekce hrozeb cesty laterální pohyb a služby Výstrahy zabezpečení ze služby Azure ATP simulované taktiky Lateral Movement, které provedete ve vaší laboratoři.  

> [!div class="nextstepaction"]
> [Playbook taktiky Lateral Movement](atp-playbook-lateral-movement.md)

## <a name="domain-dominance-playbook"></a>Playbook dominance v doméně

Je posledním dílem série čtyři části playbook dominance v doméně. Během fáze dominance v doméně útočník už získal legitimních přihlašovacích údajů pro přístup k řadiči domény a pokusí se dosažení dominance v doméně trvalé. Budete simulovat některé běžné metody dominance v doméně chcete podívat, jak že dominance v doméně, zaměřuje detekce hrozeb a zabezpečení upozornění služby Azure ATP.

> [!div class="nextstepaction"]
> [Playbook dominance v doméně](atp-playbook-domain-dominance.md)


## <a name="join-the-community"></a>Připojte se ke komunitě

Máte další dotazy nebo zájem o diskuze o ochrany ATP v programu Azure a souvisejícího zabezpečení s ostatními? Připojte se k [komunita ochrany ATP v programu Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) ještě dnes!
