---
title: Azure – ochrana ATP v programu známé problémy | Dokumentace Microsoftu
description: Popisuje aktuální známé problémy v Azure ATP
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 11/12/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: feea1982-ba23-48be-a468-98d2586cf840
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c1c5aa0359ac0d24d2bf3fc3033986657c3fc897
ms.sourcegitcommit: 2afc1486b40431f442d51a53df06e289796de87e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/12/2018
ms.locfileid: "51561440"
---
*Platí pro: Azure Rozšířená ochrana před internetovými útoky*

# <a name="azure-atp-known-issues"></a>Azure – ochrana ATP v programu známé problémy

Ochrana ATP v programu Azure má občas inženýrství nebo funkce omezení, které mohou omezit nebo změnit způsob, jak vaše organizace používá služby Azure ATP. Známá omezení potíže, které mají žádné známé alternativní řešení nebo stav probíhající práce bez časové osy konkrétní aktualizace jsou zde popsány. 

Služby Azure ATP známé problémy s známé alternativní řešení, najdete v části [řešení potíží s Azure ATP známé problémy](troubleshooting-atp-known-issues.md). Chcete-li zkontrolovat stav tenanta ochrany ATP v programu Azure, navštivte [Health Center ochrany ATP v programu Azure](atp-health-center.md). 

## <a name="winrm-not-supported-using-windows-server-2016"></a>Služba WinRM není podporován pomocí Windows serveru 2016
> [!div class="mx-tableFixed"]  
|Problém|Stav|
|----|----|
|WinRM v současné době nepodporuje Windows serveru 2016. Související zjišťování a výsledné výstrahy (vzdálený kód pokusy o provedení) nejsou k dispozici pro počítače s Windows serverem 2016.|Engineering aktuálně pracuje na vyřešení tohoto problému a přidání podpory systému Windows Server 2016.|

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

## <a name="see-also"></a>Viz také

- [Řešení potíží s Azure – ochrana ATP v programu známé problémy](troubleshooting-atp-known-issues.md)
- [Řešení potíží pomocí protokolů služby Azure ATP](troubleshooting-atp-using-logs.md)
- [Co je nového v Azure ATP](atp-whats-new.md)
- [Podívejte se na fórum služby Azure ATP.](https://aka.ms/azureatpcommunity)