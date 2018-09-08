---
title: Ověření zrcadlení portů v Advanced Threat Analytics | Dokumentace Microsoftu
description: Popisuje jak ověřit, že je zrcadlení portů nakonfigurované správně.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: ebd41719-c91a-4fdd-bcab-2affa2a2cace
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 37ec9f60c0d77260039748d57762555cae958f93
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125970"
---
*Platí pro: Advanced Threat Analytics verze 1.9*



# <a name="validate-port-mirroring"></a>Ověření zrcadlení portů
> [!NOTE] 
> Tento článek se týká jenom nasazení komponent ATA Gateway, nikoli komponent ATA Lightweight Gateway. Pokud chcete určit, jestli potřebujete ATA Gateway, přečtěte si téma [Volba vhodných bran pro vaše nasazení](ata-capacity-planning.md#choosing-the-right-gateway-type-for-your-deployment).
 
Následující kroky vás provedou procesem ověření, že je zrcadlení portů správně nakonfigurované. Pro správnou funkci ATA potřebuje, aby ATA Gateway mohla sledovat provoz do a z řadiče domény. Hlavní zdroj dat používaný ATA je hloubková kontrola paketů síťového provozu do a z řadičů domény. ATA potřebuje ke sledování síťového provozu správně nakonfigurované zrcadlení portů. Zrcadlení portů kopíruje provoz z jednoho portu (zdrojový port) na jiný port (cílový port).

## <a name="validate-port-mirroring-using-a-windows-powershell-script"></a>Ověření zrcadlení portů pomocí skriptu prostředí Windows PowerShell

1. Uložte text tohoto skriptu do souboru s názvem *ATAdiag.ps1*.
2. Spusťte tento skript na bráně ATA Gateway, kterou chcete ověřit.
Tento skript generuje přenos dat protokolu ICMP z ATA Gateway do řadiče domény a hledá tento přenos dat na síťové kartě pro zachytávání na řadiči domény.
Pokud ATA Gateway vidí přenos dat ICMP s cílovou IP adresou, která se shoduje s IP adresou řadiče domény, kterou jste zadali v konzole ATA, považuje zrcadlení portů za nakonfigurované. 

Ukázka spuštění tohoto skriptu:

    # ATAdiag.ps1 -CaptureIP n.n.n.n -DCIP n.n.n.n -TestCount n
    
    param([parameter(Mandatory=$true)][string]$CaptureIP, [parameter(Mandatory=$true)][string]$DCIP, [int]$PingCount = 10)

    # Set variables
    
        $ErrorActionPreference = "stop"
    $starttime = get-date
    $byteIn = new-object byte[] 4
    $byteOut = new-object byte[] 4
    $byteData = new-object byte[] 4096  # size of data
    
    $byteIn[0] = 1  # for promiscuous mode
    $byteIn[1-3] = 0
    $byteOut[0-3] = 0



    # Convert network data to host format
        function NetworkToHostUInt16 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt16($value,0)
        }
    
    function NetworkToHostUInt32 ($value)
        {
        [Array]::Reverse($value)
        [BitConverter]::ToUInt32($value,0)
        }
    
    function ByteToString ($value)
        {
        $AsciiEncoding = new-object system.text.asciiencoding
        $AsciiEncoding.GetString($value)
            }
    
    Write-Host "Testing Port Mirroring..." -ForegroundColor Yellow
    Write-Host ""
    Write-Host "Here is a summary of the connection we will test." -ForegroundColor Yellow

    # Initialize a first ping connection
    Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue
    Write-Host ""
    
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    Write-Host ""
    Write-Host "Sending ICMP and Capturing data..." -ForegroundColor Yellow
    
    # Open a socket
    
    $socket = new-object system.net.sockets.socket([Net.Sockets.AddressFamily]::InterNetwork,[Net.Sockets.SocketType]::Raw,[Net.Sockets.ProtocolType]::IP)
    
    # Include the IP header
    $socket.setsocketoption("IP","HeaderIncluded",$true)
    
    $socket.ReceiveBufferSize = 10000
    
    $ipendpoint = new-object system.net.ipendpoint([net.ipaddress]"$CaptureIP",0)
    $socket.bind($ipendpoint)
    
    # Enable promiscuous mode
    [void]$socket.iocontrol([net.sockets.iocontrolcode]::ReceiveAll,$byteIn,$byteOut)
    
    # Initialize test variables
    $tests = 0
    $TestResult = "Noise"
    $OneSuccess = 0
    
    while ($tests -le $PingCount)
        {
        if (!$socket.Available)  # see if any packets are in the queue
            {
            start-sleep -milliseconds 500
            continue
            }
    
    # Capture traffic
        $rcv = $socket.receive($byteData,0,$byteData.length,[net.sockets.socketflags]::None)
    
    # Decode the header so we can read ICMP
    
        $MemoryStream = new-object System.IO.MemoryStream($byteData,0,$rcv)
        $BinaryReader = new-object System.IO.BinaryReader($MemoryStream)
    
    # Set IP version & header length
        $VersionAndHeaderLength = $BinaryReader.ReadByte()
    
        # TOS
        $TypeOfService= $BinaryReader.ReadByte()
    
        # More values, and the Protocol Number for ICMP traffic
        # Convert network format of big-endian to host format of little-endian 
        $TotalLength = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
    
        $Identification = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $FlagsAndOffset = NetworkToHostUInt16 $BinaryReader.ReadBytes(2)
        $TTL = $BinaryReader.ReadByte()
        $ProtocolNumber = $BinaryReader.ReadByte()
        $Checksum = [Net.IPAddress]::NetworkToHostOrder($BinaryReader.ReadInt16())
    
        # The source and destination IP addresses
        $SourceIPAddress = $BinaryReader.ReadUInt32()
        $DestinationIPAddress = $BinaryReader.ReadUInt32()
    
        # The source and destimation ports
        $sourcePort = [uint16]0
        $destPort = [uint16]0
            
        # Close the stream reader
        $BinaryReader.Close()
        $memorystream.Close()
    
        # Cast DCIP into an IPaddress type
        $DCIPP = [ipaddress] $DCIP
        $DestinationIPAddressP = [ipaddress] $DestinationIPAddress
    
        #Ping the DC at the end after starting the capture
        Test-Connection -Count 1 -ComputerName $DCIP -ea SilentlyContinue | Out-Null
            
        # This is the match logic - check to see if Destination IP from the Ping sent matches the DCIP entered by in the ATA Console  
        # The only way the ATA Gateway should see a destination of the DC is if Port Spanning is configured
        
            if ($DestinationIPAddressP -eq $DCIPP)  # is the destination IP eq to the DC IP? 
            {
            $TestResult = "Port Spanning success!"
            $OneSuccess = 1
            } else {
                $TestResult = "Noise"
            }
        
        # Put source, destination, test result in Powershell object
        
        new-object psobject | add-member -pass noteproperty CaptureSource $([system.net.ipaddress]$SourceIPAddress) | add-member -pass noteproperty CaptureDestination $([system.net.ipaddress]$DestinationIPAddress) | Add-Member -pass NoteProperty Result $TestResult | Format-List | Out-Host
        #Count tests
        $tests ++
        }
    
        If ($OneSuccess -eq 1){
            Write-Host "Port Spanning Success!" -ForegroundColor Green
            Write-Host ""
            Write-Host "At least one packet which was addressed to the DC, was picked up by the Gateway." -ForegroundColor Yellow
            Write-Host "A little noise is OK, but if you don't see a majority of successes, you might want to re-run." -ForegroundColor Yellow
        } Else {
            Write-Host "No joy, all noise.  You may want to re-run, increase the number of Ping Counts, or check your config." -ForegroundColor Red
        }
    
    Write-Host ""
    Write-Host "Press any key to continue..." -ForegroundColor Red
    [void][System.Console]::ReadKey($true)
    
    
## <a name="validate-port-mirroring-using-net-mon"></a>Ověření zrcadlení portů pomocí Net Mon
1.  Nainstalujte [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865) v komponentě ATA Gateway, kterou chcete ověřit.

    > [!IMPORTANT]
    > Neinstalujte na komponentu ATA Gateway Microsoft Message Analyzer nebo jiný software pro zachycení provozu.

2.  Otevřete Sledování sítě a vytvořte novou kartu zachycení.

    1.  Vyberte pouze síťový adaptér pro **zachytávání** nebo síťový adaptér připojený k portu přepínače, který je nakonfigurovaný jako cíl zrcadlení portů.

    2.  Ověřte, že je povolený režim P.

    3.  Klikněte na tlačítko **Nové zachytávání**.

        ![Obrázek karty Vytvořit nové zachytávání](media/ATA-Port-Mirroring-Capture.jpg)

3.  V okně filtru zobrazení zadejte filtr **KerberosV5 nebo LDAP** a potom klikněte na **Použít**.

    ![Obrázek použití filtru KerberosV5 nebo LDAP](media/ATA-Port-Mirroring-filter-settings.jpg)

4.  Kliknutím na **Spustit** spusťte relaci zachytávání. Pokud nevidíte provoz do a z řadiče domény, zkontrolujte konfiguraci zrcadlení portů.

    ![Obrázek spuštění relace zachytávání](media/ATA-Port-Mirroring-Capture-traffic.jpg)

    > [!NOTE]
    > Je důležité se ujistit, že vidíte provoz do a z řadičů domény.
    

5.  Pokud se zobrazí přenos jenom v jednom směru, obraťte se na týmy podpory sítí nebo virtualizace, aby vám pomohly vyřešit potíže s konfigurací zrcadlení portů.

## <a name="see-also"></a>Viz také

- [Konfigurace zrcadlení portů](configure-port-mirroring.md)
- [Podívejte se na fórum ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
