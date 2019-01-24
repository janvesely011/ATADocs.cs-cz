---
title: Kurz Azure šetření počítače ochrany ATP v programu | Dokumentace Microsoftu
d|Description: This article explains how to use Azure ATP security alerts to investigate a suspicious computer.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/14/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3c707376635facd0fe9ba8e3c3f32f36f5a71c25
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/24/2019
ms.locfileid: "54839542"
---
# <a name="tutorial-investigate-a-computer"></a>Kurz: Prozkoumat počítače

Azure důkazy upozornění ochrany ATP v programu poskytuje zrušte označení, když počítače mít podíl na podezřelé aktivity nebo pokud existují označení, že na počítači dojde k narušení. Pomocí návrhy šetření můžete určit rizika pro vaši organizaci, rozhodněte se, jak opravit a určit nejlepší způsob, jak podobné útokům v budoucnu.  

## <a name="investigation-steps-for-suspicious-computers"></a>Kroky šetření pro podezřelé počítače

Na stránce profil počítače, klikněte na tlačítko na konkrétní počítače uvedené ve výstraze, kterou chcete prozkoumat. Abychom šetření výstrahy důkazy zobrazí všechny počítače (a [uživatelé](investigate-a-user.md)) připojené k každá podezřelá aktivita.

Zkontrolujte a prozkoumat profilu počítače následující podrobnosti a aktivit:

- Co se stalo v době výskytu podezřelé aktivity?  
  1. Které [uživatele](investigate-a-user.md) byl přihlášen k počítači?
  2. Tento uživatel normálně přihlásit nebo přístup ke zdrojové nebo cílové počítače?
  3. Které prostředky jsou-li získat přístup? Které uživatelé?
      - Pokud byly přistupovat k prostředkům, byly jejich prostředky vysoké hodnoty?
  4. Byl uživatel má k těmto prostředkům přístup?
  5. Nebyla [uživatele](investigate-a-user.md) , ke kterým přistupuje počítač provádět další podezřelé aktivity?

- Další podezřelé aktivity byste měli prozkoumat:
    1. Otevřely ostatní výstrahy přibližně ve stejnou dobu jako tato výstraha v ochrany ATP v programu Azure nebo v jiných nástrojích zabezpečení, jako je ochrana ATP v programu Windows Defender, Azure Security Center a/nebo Microsoft CAS?
    2. Byla neúspěšná přihlášení?


- Pokud je povolená ochrana ATP v programu Windows Defender integrace, klikněte na oznámení "BADGE" ochrany ATP v programu Windows Defender k hlubšímu prošetření počítače. V programu Windows Defender ATP uvidíte výstrahy a procesy k nimž došlo přibližně ve stejnou dobu jako upozornění.
    1. Byly všechny programy pro nové nasazení nebo nainstalovat?

## <a name="see-also"></a>Viz také

- [Prošetřování uživatelů](investigate-a-user.md)
- [Práce s výstrahami zabezpečení](working-with-suspicious-activities.md)
- [Práce s cesty taktiky Lateral Movement](use-case-lateral-movement-path.md)
- [Výstrahy před hrozbami „osahávání“ (reconnaissance)](atp-reconnaissance-alerts.md)
- [Výstrahy před ohrožením zabezpečení přihlašovacích údajů](atp-compromised-credentials-alerts.md)
- [Výstrahy před taktikou lateral movement](atp-lateral-movement-alerts.md)
- [Výstrahy před dominancí v doméně](atp-domain-dominance-alerts.md)
- [Výstrahy před exfiltrací](atp-exfiltration-alerts.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)
