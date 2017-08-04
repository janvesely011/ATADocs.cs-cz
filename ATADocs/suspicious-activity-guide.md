---
title: "Průvodce podezřelými aktivitami ATA | Dokumentace Microsoftu"
d|Description: This article provides a list of the suspicious activities ATA can detect and steps for remediation.
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 8c93f4485998bbb1b2b440f01fed8d96ad4e2842
ms.sourcegitcommit: 7bc04eb4d004608764b3ded1febf32bc4ed020be
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/02/2017
---
*Platí pro: Advanced Threat Analytics verze 1.8*


# <a name="introduction"></a>Úvod

ATA zajišťuje detekci pro následující fáze pokročilých útoků: rekognoskace, zneužití přihlašovacích údajů, laterální pohyb, zvýšení úrovně oprávnění, dominance v doméně a další.

V tomto diagramu jsou vyznačené fáze v řetězu událostí, kde ATA aktuálně poskytuje detekce.

![Zaměření řešení ATA na postranní aktivity v řetězci úkonů útočníka](media/attack-kill-chain-small.jpg)

Tento článek obsahuje podrobnosti o jednotlivých činnostech v každé fázi.


## <a name="reconnaissance-using-account-enumeration"></a>Rekognoskace pomocí výčtu účtů

> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Útok zaměřený na výčet účtů je technika, kterou útočníci používají k hádání názvů účtů s využitím pokusů o ověření protokolem Kerberos, aby zjistili, jestli uživatel existuje v síti. Úspěšně uhádnuté účty lze použít v následných krocích útoku. | Podívejte se na dotyčný počítač a snažte se zjistit, jestli existuje rozumný důvod, proč by měl spouštět tolik procesů ověřování protokolem Kerberos. Jedná se o procesy, které se snažily neúspěšně zjistit několik účtů, protože uživatel neexistuje (chyba Client_Principal_Unknown) a nejméně jeden úspěšný pokus o přístup. <br></br>**Výjimky:** Tato detekce spoléhá na hledání několika neexistujících účtů a pokusy o ověření z jednoho počítače. Pokud nějaký uživatel při ručním zadávání uživatelského jména nebo domény udělá chybu, považuje se tento pokus o ověření za pokus o přihlášení k neexistujícímu účtu. U serverů vzdálené plochy, které vyžadují přihlášení mnoha uživatelů, může oprávněně docházet k velkému počtu neúspěšných pokusů o přihlášení. |Prošetřete proces, který způsobuje generování těchto žádostí.  Pomoc s určením procesů na základě zdrojového portu najdete v článku [Chtěli jste někdy vědět, který proces Windows pošle určitý paket do sítě?](https://blogs.technet.microsoft.com/nettracer/2010/08/02/have-you-ever-wanted-to-see-which-windows-process-sends-a-certain-packet-out-to-network/)|Střední|

## <a name="reconnaissance-using-directory-services-enumeration-sam-r"></a>Rekognoskace pomocí výčtu adresářových služeb (SAM-R)

> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
irectory služby rekognoskace je technika používaných útočníky k namapování strukturu adresáře a cíle privilegované účty na pozdější kroky útoku. Jednou z metod používaných k dotazování adresáře je protokol SAM-R (Security Account Manager Remote). | Zjistěte, proč dotyčný počítač provádí dotazy MS-SAMR (Security Accounts Manager - Remote). Tato operace probíhá neobvyklým způsobem, pravděpodobně kvůli dotazování citlivých entit. <br></br>**Výjimky:** Tato detekce spoléhá na profilaci normálního chování uživatelů, kteří provádějí dotazy SAM-R, a upozorní vás při zpozorování neobvyklého dotazu. Citliví uživatelé, kteří se přihlašují k jiným než svým počítačům, můžou aktivovat dotaz SAM-R, který bude detekován jako neobvyklý, přestože jde o součást normálního pracovního procesu. Běžně se to může stávat členům IT oddělení. Pokud se toto chování označí za podezřelé, ale jednalo se o výsledek normálního používání, je tomu tak proto, že toto chování nebylo řešením ATA dříve pozorováno. | V takovém případě se doporučuje prodloužit dobu učení a zlepšit pokrytí ATA v doméně pro každou doménovou strukturu služby Active Directory.<br></br>[Stáhněte a spusťte nástroj SAMRi10](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b). Nástroj SAMRi10, vydaný týmem ATA, posiluje zabezpečení vašeho prostředí vůči dotazům SAM-R. | Střední|

## <a name="reconnaissance-using-dns"></a>Rekognoskace pomocí DNS


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Server DNS obsahuje mapu všech počítačů, IP adres a služeb ve vaší síti. Tyto údaje používají útočníci ke zmapování struktury vaší sítě a zacílení zajímavých počítačů v pozdějších krocích útoku. | Zjistěte, proč dotyčný počítač provádí dotaz na přenos celé zóny (AXFR), aby získal všechny záznamy v doméně DNS. <br></br>**Výjimky:** Tato detekce identifikuje jiné servery než DNS, které vydávají žádosti o přenos zóny DNS. O některých řešeních pro kontrolu zabezpečení je známo, že vůči serverům DNS vydávají tyto druhy žádostí. <br></br>Kvůli vyloučení falešně pozitivních hlášení zároveň ověřte, jestli komponenty ATA Gateway můžou se servery DNS komunikovat přes port 53.| Omezte přenosy zóny pečlivou volbou hostitelů, kteří si je mohou vyžádat. Další podrobnosti najdete v článku [Zabezpečení DNS](https://technet.microsoft.com/library/cc770474(v=ws.11).aspx) a [Kontrolní seznam: Zabezpečení serveru DNS](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx). |Střední|

## <a name="reconnaissance-using-smb-session-enumeration"></a>Rekognoskace pomocí výčtu relací SMB


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Výčet SMB (Server Message Block) umožňuje útočníkovi získat informace o tom, ze kterých IP adres ve vaší síti se uživatelé nedávno přihlašovali. Jakmile má útočník tyto informace, může je použít k zacílení konkrétních účtů a laterálnímu pohybu v síti. | Zjistěte, proč dotyčný počítač provádí výčet relací SMB.<br></br>**Výjimky:** Tato detekce staví na předpokladu, že výčet relací SMB nemá v podnikové síti rozumné využití, některá řešení pro kontrolu zabezpečení (například Websense) ale takové žádosti vydávají. | [Posilte zabezpečení svého prostředí pomocí nástroje Net Cease](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b). | Střední   |

## <a name="brute-force-ldap-kerberos-ntlm"></a>Hrubá síla (LDAP, Kerberos, NTLM)


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Při útoku hrubou silou zkouší útočník množství hesel a doufá, že ho nakonec uhádne. Útočník systematicky zkouší všechna možná hesla (nebo velkou množinu možných hesel), dokud neuhádne to správné. Jakmile útočník uhádne správné heslo, může se přihlásit do sítě, jako kdyby byl uživatel. ATA momentálně podporuje horizontální útoky hrubou silou (více účtů) využívající protokol Kerberos nebo NTLM, a horizontální a vertikální útoky (jeden účet, více pokusů o uhádnutí hesla) využívající jednoduchou vazbu protokolu LDAP. | Zjistěte, proč se dotyčnému počítači nedaří ověřit několik uživatelských účtů (se zhruba stejným počtem pokusů o ověření několika uživatelů) nebo proč u jednoho uživatele došlo k velkému počtu neúspěšných ověření. <br></br>**Výjimky:** Tato detekce spoléhá na profilaci normálního chování účtů, které se ověřují vůči různým prostředkům, a aktivuje upozornění při zpozorování neobvyklého vzoru. Tento vzor bývá běžný u skriptů, které se ověřují automaticky, ale můžou používat zastaralé přihlašovací údaje (například špatné heslo nebo uživatelské jméno). | Nezbytnou první úroveň zabezpečení proti útokům hrubou silou zajišťují složitá a dlouhá hesla. | Střední   |

## <a name="sensitive-account-exposed-in-plain-text-authentication-and-service-exposing-accounts-in-plain-text-authentication"></a>Zveřejnění citlivých účtů při ověřování pomocí prostého textu a služba zveřejňující účty při ověřování pomocí prostého textu


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Některé služby v počítači posílají přihlašovací údaje účtu v prostém textu, a to i u citlivých účtů. Útočníci, kteří monitorují provoz, můžou tyto přihlašovací údaje odchytit a zneužít ke škodlivým účelům. Jakékoli heslo citlivého účtu uložené ve formě nešifrovaného textu aktivuje upozornění. | Najděte dotyčný počítač a zjistěte, proč používá jednoduché vazby protokolu LDAP. | Ověřte konfiguraci na zdrojových počítačích a zajistěte, aby nepoužívaly jednoduchou vazbu protokolu LDAP. Místo jednoduchých vazeb protokolu LDAP použijte LDAP SALS nebo LDAPS. Dodržujte architekturu vrstev zabezpečení a omezením přístupu přes různé vrstvy zabraňte eskalaci oprávnění. | Nízká pro zveřejnění služby; střední pro citlivé účty |

## <a name="honey-token-account-suspicious-activities"></a>Podezřelé aktivity účtu sloužícího jako návnada (honeytoken)


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Účty honeytokenu slouží jako návnada a umožňují odchytit, identifikovat a sledovat škodlivou aktivitu v síti, jejíž jsou součástí. Jedná se účty, které se ve vaší síti nepoužívají a jsou nečinné, přičemž náhlá aktivita u některého účtu honeytokenu může znamenat, že se ho snaží použít kyberzločinec. | Zjistěte, proč se z tohoto počítače ověřuje účet honeytokenu. | Projděte profilové stránky ATA jiných citlivých (privilegovaných) účtů ve vašem prostředí a zjistěte, jestli nedochází k potenciálně podezřelým aktivitám. | Střední   |

## <a name="unusual-protocol-implementation"></a>Neobvyklá implementace protokolu


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
|Útočníci můžou používat nástroje implementující protokoly SMB/Kerberos určitými způsoby, které jim přes síť umožní docílit jistých schopností. To svědčí o škodlivých technikách sloužících k vynechání hodnoty hash (Over-pass-the-Hash) nebo útokům hrubou silou. | Zjistěte, proč by dotyčný počítač používal ověřovací protokol nebo protokol SMB neobvyklým způsobem. <br></br>Následujícím postupem určete, jestli se jedná o útok WannaCry:<br></br> 1.    Stáhněte export této podezřelé aktivity do Excelu.<br></br>2.    Otevřete kartu se síťovou aktivitou, přejděte na pole Json a zkopírujte související objekty JSON Smb1SessionSetup a Ntlm.<br></br>3.   Pokud má Smb1SessionSetup.OperatingSystem hodnotu „Windows 2000 2195“, Smb1SessionSetup.IsEmbeddedNtlm má hodnotu „true“ a Ntlm.SourceAccountId má hodnotu „null“, jedná se o WannaCry.<br></br><br></br>**Výjimky:** Tato detekce se může v ojedinělých případech aktivovat při použití legitimních nástrojů, které tyto protokoly implementují nestandardním způsobem. Sem patří některé aplikace pro testování průniku. | Zachyťte síťový provoz a určete, který proces generuje provoz s neobvyklou implementací protokolu.| Střední|

## <a name="malicious-data-protection-private-information-request"></a>Škodlivá žádost o soukromé informace přes Data Protection


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
|Rozhraní Data Protection API (DPAPI) používá několik součástí Windows k bezpečnému ukládání hesel, šifrovacích klíčů a jiných citlivých dat. Na řadičích domény se nachází záložní hlavní klíč, který můžou počítače s Windows připojené k doméně použít k dešifrování všech tajných kódů zašifrovaných pomocí rozhraní DPAPI. Útočníci můžou doménový záložní hlavní klíč rozhraní DPAPI použít k dešifrování všech tajných kódů na všech počítačích připojených k doméně (hesel v prohlížečích, zašifrovaných souborů atd.).| Zjistěte, proč počítač učinil žádost pomocí tohoto nedokumentovaného volání rozhraní API o hlavní klíč rozhraní DPAPI.|Další informace o rozhraní DPAPI najdete v článku [Windows Data Protection](https://msdn.microsoft.com/library/ms995355.aspx).|Vysoká|

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>Podezření na krádež identity na základě neobvyklého chování


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Po sestavení behaviorálního modelu (což vyžaduje nejméně 50 aktivních účtů po dobu 3 týdnů) se při neobvyklém chování aktivuje upozornění. Chování, které se neshoduje s modelem sestaveným pro konkrétní uživatelský účet, může značit krádež identity. | Zjistěte, proč se dotyčný uživatel může chovat jinak. <br></br>**Výjimky:** Pokud ATA pokrývá jen část sítě (na ATA Gateway nejsou směrovány všechny řadiče domény), pozná se jen částečná aktivita konkrétního uživatele. Pokud po více než 3 týdnech začne náhle ATA kontrolovat veškerý provoz, může úplná aktivita tohoto uživatele aktivovat upozornění. | Zajistěte nasazení ATA na všechny řadiče domény. <br></br>1.  Ověřte, jestli uživatel nemá novou pozici v organizaci.<br></br>2.  Zkontrolujte, jestli nejde o sezónního pracovníka.<br></br>3.  Zjistěte, jestli se uživatel nevrátil po dlouhé absenci.| Střední pro všechny uživatele a vysoká pro citlivé uživatele |


## <a name="pass-the-ticket"></a>Pass-the-ticket


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Útok předáním lístku (Pass-the-Ticket) je technika laterálního pohybu, kdy útočník ukradne lístek Kerberos z jednoho počítače a použije ho ke získání přístupu k jinému počítači předstíráním nějaké entity v síti. | Tato detekce spoléhá na použití stejných lístků Kerberos na dvou (nebo více) odlišných počítačích. Při rychlých změnách IP adres nemusí v některých případech ATA zjistit, jestli jsou různé IP adresy používané stejným počítačem nebo odlišnými počítači. To je běžný problém při použití poddimenzovaných fondů DHCP (VPN, Wi-Fi atd.) a sdílených IP adres (zařízení s překladem adres NAT). | Dodržujte architekturu vrstev zabezpečení a omezením přístupu přes různé vrstvy zabraňte eskalaci oprávnění. | Vysoká     |

## <a name="pass-the-hash"></a>Pass-the-hash


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Při útoku předáním hodnoty hash (Pass-the-Hash) se útočník vůči vzdálenému serveru nebo službě ověří pomocí zdrojové hodnoty hash NTLM uživatelského hesla místo přidruženého hesla v prostém textu jako normálně. | Zjistěte, jestli účet neprováděl v době tohoto upozornění nějaké neobvyklé aktivity. | Implementujte doporučení popsaná v článku [Předání hodnoty hash (Pass-the-Hash)](http://aka.ms/PtH). Dodržujte architekturu vrstev zabezpečení a omezením přístupu přes různé vrstvy zabraňte eskalaci oprávnění. | Vysoká|

## <a name="over-pass-the-hash"></a>Over-pass-the-hash


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Útok vynecháním hodnoty hash (Over-pass-the-Hash) zneužívá slabin v implementaci ověřovacího protokolu Kerberos, kdy se k vytvoření lístku Kerberos používá hodnota hash NTLM, což útočníkovi umožňuje, aby se vůči službám v síti ověřil bez uživatelského hesla. | Oslabení šifrování: Zjistěte, proč dotyčný účet používá v protokolu Kerberos šifrování RC4 potom, co se začalo používat šifrování AES. <br></br>**Výjimky:** Tato detekce spoléhá na profilaci šifrovacích metod používaných v doméně a upozorní vás při zpozorování jakékoli neobvyklé nebo slabší metody. V některých případech bude použita slabší šifrovací metoda a ATA ji detekuje jako neobvyklou, přestože může být součástí normálního (i když vzácného) pracovního procesu. To se může stát, pokud takové chování nebylo v minulosti řešením ATA pozorováno. Pomůže lepší pokrytí domény řešením ATA. | Implementujte doporučení popsaná v článku [Předání hodnoty hash (Pass-the-Hash)](http://aka.ms/PtH). Dodržujte architekturu vrstev zabezpečení a omezením přístupu přes různé vrstvy zabraňte eskalaci oprávnění. | Vysoká     |

## <a name="privilege-escalation-using-forged-authorization-data-ms14-068-exploit-forged-pac--ms11-013-exploit-silver-pac"></a>Eskalace oprávnění pomocí zfalšovaných dat autorizace (zneužití MS14-068 (zfalšovaný certifikát PAC) / zneužití MS11-013 (stříbrný certifikát PAC))


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Známé chyby zabezpečení ve starších verzích Windows Serveru umožňují útočníkům manipulovat s certifikátem PAC (Privileged Attribute Certificate), což je pole v lístku Kerberos, které obsahuje data autorizace uživatele (u služby Active Directory jde o členství ve skupině) a uděluje útočníkovi dodatečná oprávnění. | Zkontrolujte, jestli na dotyčném počítači neběží nějaká speciální služba, která může používat jinou metodu ověřování než certifikát PAC. <br></br>**Výjimky:** V některých speciálních situacích můžou upozornění ATA aktivovat prostředky, které implementují vlastní ověřovací mechanismy. | Zajistěte, aby na všech řadičích domény s operačním systémem až do verze Windows Server 2012 R2 byla nainstalovaná aktualizace [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) a na všech členských serverech a řadičích domény až do verze 2012 R2 byla nainstalovaná aktualizace KB2496930. Další informace najdete v článku [Stříbrný certifikát PAC](https://technet.microsoft.com/library/security/ms11-013.aspx) a [Zfalšovaný certifikát PAC](https://technet.microsoft.com/library/security/ms14-068.aspx). | Vysoká     |

## <a name="abnormal-sensitive-group-modification"></a>Neobvyklá úprava citlivých skupin


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
|Jako součást fáze eskalace oprávnění upravují útočníci skupiny s vysokými oprávněními, aby získali přístup k citlivým prostředkům.| Ověřte, že je změna skupiny oprávněná. <br></br>**Výjimky:** Tato detekce spoléhá na profilaci normálního chování uživatelů, kteří upravují citlivé skupiny, a upozorní vás při zpozorování neobvyklé změny. Oprávněné změny můžou aktivovat upozornění, pokud řešení ATA v minulosti takové chování nezpozorovalo. Pomůže delší doba učení a lepší pokrytí domény řešením ATA. | Zajistěte, aby skupina osob, které mají autorizaci k úpravě citlivých skupin, byla co nejmenší. Pokud je to možné, používejte oprávnění za běhu (just-in-time). | Střední   |

## <a name="encryption-downgrade---skeleton-key-malware"></a>Oslabení šifrování – malware Skeleton Key


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Skeleton Key je malware, který běží na řadičích domény a umožňuje ověření vůči doméně pomocí libovolného účtu bez znalosti jeho hesla. Tento malware často používá slabší šifrovací algoritmy k zakódování hesel uživatelů na řadiči domény. | Oslabení šifrování: Zjistěte, proč dotyčný účet používá v protokolu Kerberos šifrování RC4 potom, co se začalo používat šifrování AES. <br></br>**Výjimky:** Tato detekce spoléhá na profilaci šifrovacích metod používaných v doméně. V některých případech bude použita slabší šifrovací metoda a ATA ji detekuje jako neobvyklou, přestože je součástí normálního (i když vzácného) pracovního procesu. | Pomocí [kontroly vytvořené týmem ATA](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73) můžete zkontrolovat, jestli jsou vaše řadiče domény infikované malwarem Skeleton Key. | Vysoká |

## <a name="golden-ticket"></a>Zlatý lístek


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Pokud má útočník práva správce domény, může vytvořit lístek Kerberos udělující lístek (TGT), který poskytuje autorizaci pro všechny prostředky v síti, a nastavit čas vypršení platnosti tohoto lístku na libovolnou hodnotu. To útočníkům umožňuje dosáhnout trvalého průniku do sítě. | Oslabení šifrování: Zjistěte, proč dotyčný účet používá v protokolu Kerberos šifrování RC4 potom, co se začalo používat šifrování AES. <br></br>**Výjimky:** Tato detekce spoléhá na profilaci šifrovacích metod používaných v doméně a zobrazí upozornění při zpozorování jakékoli neobvyklé nebo slabší metody. V některých případech se slabší šifrovací metoda má používat a ATA ji detekuje jako neobvyklou, ačkoli je součástí normálního (i když vzácného) pracovního procesu. To se může stát, pokud takové chování nebylo v minulosti řešením ATA pozorováno. Zajistěte, aby byla doména plně pokryta řešením ATA. | Následujícími způsoby zajistěte, aby byl hlavní klíč KRBTGT (Kerberos Ticket Granting Ticket) co nevíce zabezpečený:<br></br>1.  Fyzické zabezpečení<br></br>2.  Fyzické zabezpečení virtuálních počítačů<br></br>3. Posílení zabezpečení řadičů domény<br></br>4.  Izolace LSA (Local Security Authority) / ochrana Credential Guard<br></br>Při detekci zlatých lístků je potřeba provést podrobnější prošetření a vyhodnotit, jestli je zapotřebí taktické obnovení.<br></br>Podle pokynů v [článku o dostupnosti skriptů pro resetování hesla účtu KRBTGT na blogu Microsoftu](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) měňte [nástrojem pro resetování hesla/klíčů účtu KRBTGT](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) dvakrát pravidelně lístek KRBTGT (Kerberos Ticket Granting Ticket). <br></br>Implementujte tato [doporučení pro předání hodnoty hash (Pass-the-Hash)](http://aka.ms/PtH). | Střední   |



## <a name="remote-execution"></a>Vzdálené spuštění


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Útočníci, kteří získali přihlašovací údaje správce, mohou na řadiči domény spouštět vzdálené příkazy. Toho mohou využít k trvalému průniku do sítě, shromažďování informací, útokům DoS (Denial of Service) nebo z jakéhokoli jiného důvodu. | Zjistěte, jestli je u dotyčného účtu povolené vzdálené spuštění vůči vašemu řadiči domény. <br></br>**Výjimky:** Toto upozornění mohou aktivovat legitimní uživatelé, kteří občas spouštějí příkazy na řadiči domény, ačkoli je to součástí normálního procesu správy. Většinou se jedná o členy IT týmu nebo účty služeb provádějící úlohy, které souvisejí se správou řadiče domény. | Zakažte vzdálený přístup k řadičům domény z počítačů, které nejsou ve vrstvě 0. Odstraňte všechny podezřelé, zastaralé a nepotřebné soubory a složky. Implementujte silné zásady řízení uživatelských účtů. Pro správce implementujte [PAW](https://technet.microsoft.com/en-us/windows-server-docs/security/securing-privileged-access/securing-privileged-access) umožňující připojení k řadičům domény jen počítačům s posíleným zabezpečením. | Nízká      |

## <a name="malicious-replication-requests"></a>Požadavky na škodlivou replikaci


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Replikace služby Active Directory je proces, při kterém se změny provedené na jednom řadiči domény synchronizují s jinými řadiči domény v doméně nebo doménové struktuře, na kterých jsou uložené kopie stejných dat. Pokud má útočník příslušná oprávnění, může iniciovat žádost o replikaci jako by byl řadičem domény, což mu umožní získat data uložená ve službě Active Directory včetně hodnot hash hesel. | Zjistěte, proč počítač může používat rozhraní API pro replikaci řadiče domény. Tato detekce spoléhá na to, že ATA pomocí konfiguračního oddílu doménové struktury adresáře určuje, jestli je počítač řadičem domény. <br></br>**Výjimky:** Toto upozornění může aktivovat synchronizace adresáře služby Azure AD. | Ověřte následující oprávnění: – Replikace změn adresáře <br></br>– Replikace změn adresáře AI<br></br>Další informace najdete v článku [Udělení službě Active Directory Domain Services oprávnění k synchronizaci profilu v SharePoint Serveru 2013](https://technet.microsoft.com/library/hh296982.aspx).<br></br>Pokud chcete zjistit, kdo má v doméně tato oprávnění, můžete využít nástroj [AD ACL Scanner](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) nebo vytvořit powershellový skript. | Střední   |



## <a name="broken-trust-between-domain-and-computers"></a>Porušený vztah důvěryhodnosti mezi doménou a počítači


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| Porušený vztah důvěryhodnosti znamená, že nemusí platit požadavky na zabezpečení služby Active Directory. To se často považuje za nedostatek základního zabezpečení a dodržování předpisů a za snadný cíl pro útočníky. Pokud v průběhu 24 hodin dojde u nějakého počítače k více než 5 po sobě jdoucím chybám ověření protokolem Kerberos, aktivuje se v ATA upozornění. Protože tento počítač nekomunikuje s řadičem domény, (1) nemá aktualizované zásady skupiny a (2) přihlášení je omezené na přihlašovací údaje v mezipaměti. | Kontrolou protokolů událostí ověřte, jestli je vztah důvěryhodnosti počítače a domény v pořádku. | V případě potřeby připojte počítač znovu k doméně nebo resetujte jeho heslo. | Nízká      |

## <a name="massive-object-deletion"></a>Hromadné odstranění objektů


> [!div class="mx-tableFixed"]
|Popis|Šetření|Doporučení|Závažnost|
|------|----|------|----------|
| ATA zobrazí toto upozornění při odstranění více než 5 % všech účtů. To vyžaduje oprávnění ke čtení kontejneru odstraněných položek. | Zjistěte, proč bylo náhle odstraněno 5 % všech účtů. | Odeberte oprávnění uživatelům, kteří mohou odstraňovat účty ve službě Active Directory. Podrobnosti najdete v článku [Zobrazení nebo nastavení oprávnění u objektu adresáře](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx). | Nízká |

## <a name="see-also"></a>Viz také
- [Práce s podezřelými aktivitami](working-with-suspicious-activities.md)
- [Prošetření útoků v podobě zfalšovaných certifikátů PAC](use-case-forged-pac.md)
- [Řešení známých chyb ATA](troubleshooting-ata-known-errors.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
