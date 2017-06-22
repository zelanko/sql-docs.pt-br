---
title: Carregar assemblies SMO no Windows PowerShell | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8ca42b69-da5a-47f4-9085-34e443f0e389
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 149ba0be18c46dbf2171f7a1fac0641ae81d3515
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="load-the-smo-assemblies-in-windows-powershell"></a>Carregar os assemblies SMO no Windows PowerShell
  Este tópico descreve como carregar os assemblies SMO (SQL Server Management Object) em scripts do Windows PowerShell que não usam o provedor do SQL Server PowerShell.  
  
## <a name="before-you-begin"></a>Antes de começar  
 O mecanismo preferido para carregar os assemblies SMO é carregar o módulo **sqlps** . O provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluído automaticamente no módulo carrega os assemblies SMO e também implementa recursos que estendem a utilidade dos objetos SMO em scripts do PowerShell.  Para obter mais informações, consulte [Importar o módulo SQLPS](../../relational-databases/scripting/import-the-sqlps-module.md).
  
 Há dois casos em que você pode precisar carregar diretamente os assemblies do SMO:  
  
-   Se o script fizer referência a um objeto do SMO antes do primeiro comando que faz referência ao provedor ou a cmdlets dos snap-ins do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Você deseja portar código do SMO de outra linguagem, como C# ou Visual Basic, que não usa o provedor ou cmdlets.  
  
## <a name="example-loading-the-sql-server-management-objects"></a>Exemplo: carregando SQL Server Management Objects  
 O código a seguir carrega os assemblies do SMO:  
  
```  
#  
# Loads the SQL Server Management Objects (SMO)  
#  
  
$ErrorActionPreference = "Stop"  
  
$sqlpsreg="HKLM:\SOFTWARE\Microsoft\PowerShell\1\ShellIds\Microsoft.SqlServer.Management.PowerShell.sqlps"  
  
if (Get-ChildItem $sqlpsreg -ErrorAction "SilentlyContinue")  
{  
    throw "SQL Server Provider for Windows PowerShell is not installed."  
}  
else  
{  
    $item = Get-ItemProperty $sqlpsreg  
    $sqlpsPath = [System.IO.Path]::GetDirectoryName($item.Path)  
}  
  
$assemblylist =   
"Microsoft.SqlServer.Management.Common",  
"Microsoft.SqlServer.Smo",  
"Microsoft.SqlServer.Dmf ",  
"Microsoft.SqlServer.Instapi ",  
"Microsoft.SqlServer.SqlWmiManagement ",  
"Microsoft.SqlServer.ConnectionInfo ",  
"Microsoft.SqlServer.SmoExtended ",  
"Microsoft.SqlServer.SqlTDiagM ",  
"Microsoft.SqlServer.SString ",  
"Microsoft.SqlServer.Management.RegisteredServers ",  
"Microsoft.SqlServer.Management.Sdk.Sfc ",  
"Microsoft.SqlServer.SqlEnum ",  
"Microsoft.SqlServer.RegSvrEnum ",  
"Microsoft.SqlServer.WmiEnum ",  
"Microsoft.SqlServer.ServiceBrokerEnum ",  
"Microsoft.SqlServer.ConnectionInfoExtended ",  
"Microsoft.SqlServer.Management.Collector ",  
"Microsoft.SqlServer.Management.CollectorEnum",  
"Microsoft.SqlServer.Management.Dac",  
"Microsoft.SqlServer.Management.DacEnum",  
"Microsoft.SqlServer.Management.Utility"  
  
foreach ($asm in $assemblylist)  
{  
    $asm = [Reflection.Assembly]::LoadWithPartialName($asm)  
}  
  
Push-Location  
cd $sqlpsPath  
update-FormatData -prependpath SQLProvider.Format.ps1xml   
Pop-Location  
```  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
