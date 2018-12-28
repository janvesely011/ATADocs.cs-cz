---
title: Azure – ochrana ATP v programu známé problémy | Dokumentace Microsoftu
description: Popisuje aktuální známé problémy v Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/17/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 59da5e27433ba4ce38e05d4e723f763cf48ca23d
ms.sourcegitcommit: c3ee9495b9d4db985783dcabcc4fa77c7c8eaed4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/17/2018
ms.locfileid: "53454474"
---
*Platí pro: Azure Advanced Threat Protection*

# <a name="azure-atp-known-issues"></a>Azure – ochrana ATP v programu známé problémy

Ochrana ATP v programu Azure má občas inženýrství nebo funkce omezení, které mohou omezit nebo změnit způsob, jak vaše organizace používá služby Azure ATP. Známá omezení potíže, které mají žádné známé alternativní řešení nebo stav probíhající práce bez časové osy konkrétní aktualizace jsou zde popsány. 

Služby Azure ATP známé problémy s známé alternativní řešení, najdete v části [řešení potíží s Azure ATP známé problémy](troubleshooting-atp-known-issues.md). Chcete-li zkontrolovat stav tenanta ochrany ATP v programu Azure, navštivte [Health Center ochrany ATP v programu Azure](atp-health-center.md). 

## <a name="suspected-brute-force-attack-ldap-security-alert-display"></a>Podezřelý útok hrubou silou výstraha zabezpečení zobrazení útoku (LDAP)
> [!div class="mx-tableFixed"] 

|Problém|Stav|
|----|----|
*Vzbuzovat podezření na útok hrubou silou útoku (LDAP)* výstrahu zabezpečení se vždy nezobrazí podle očekávání. V některých scénářích se zobrazí popis výstrahy mimo pořadí.| Engineering aktuálně pracuje na vyřešení tohoto problému.| 

## <a name="ad-groups-with-more-than-1000-members-have-limited-detail-sync"></a>Skupiny AD s více než 1000 členů mají omezenou podrobnosti synchronizace
> [!div class="mx-tableFixed"]  
|Problém|Stav|
|----|----|
|Ochrana ATP v programu Azure nepodporuje podrobnosti synchronizace entit ve skupinách AD s více než 1000 členů na skupinu. Při zkoumání entit ve skupinách s více než 1 000 členů, může selhat některé entity k synchronizaci nebo zobrazení podrobností.|Omezení inženýrství. Žádné známé řešení.|

## <a name="report-downloads-cannot-contain-more-than-100000-entries"></a>Soubory ke stažení sestavy nemůže obsahovat více než 100 000 položek
> [!div class="mx-tableFixed"]  
|Problém|Stav|
|----|----|
|Ochrana ATP v programu Azure nepodporuje soubory ke stažení sestavy, které obsahují více než 100 000 položek na sestavu. Sestavy se zobrazí takto neúplný, pokud více než 100 000 položek, které jsou zahrnuty.|Omezení inženýrství. Žádné známé řešení.|

## <a name="closed-issues"></a>Uzavřené problémy

Tato skupina známých problémů už jsou uzavřené. Zkontrolujte číslo verze opravy pro referenci.   
### <a name="remote-code-execution-attempts-using-remote-powershell-commands-or-scripts-are-not-detected-when-using-windows-server-2016---v257-december-2-2018"></a>Vzdálené spuštění kódu pokusí pomocí vzdáleného prostředí PowerShell příkazů nebo skriptů nejsou zjištěny při použití Windows serveru 2016 - v.2.57 (2. prosince 2018)
> [!div class="mx-tableFixed"]  
|Problém|Stav|
|----|----|
|Vzdálené pokusy o spuštění kódu pomocí příkazů Powershellu vzdáleného nejsou aktuálně zjištěna senzor počítače s Windows serverem 2016. Související detekcí a výsledné výstrahy nejsou k dispozici.|Engineering aktuálně pracuje na vyřešení tohoto problému a přidání podpory systému Windows Server 2016.|

## <a name="see-also"></a>Viz také

- [Řešení potíží s Azure – ochrana ATP v programu známé problémy](troubleshooting-atp-known-issues.md)
- [Řešení potíží pomocí protokolů služby Azure ATP](troubleshooting-atp-using-logs.md)
- [Co je nového v Azure ATP](atp-whats-new.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)