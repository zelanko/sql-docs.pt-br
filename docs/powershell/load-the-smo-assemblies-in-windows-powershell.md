---
title: Carregar assemblies SMO no Windows PowerShell | Microsoft Docs
description: Saiba como carregar os assemblies do SMO (SQL Server Management Object) em scripts do Windows PowerShell que não usam o provedor do SQL Server PowerShell.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 8ca42b69-da5a-47f4-9085-34e443f0e389
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f3ac67e05f5a94de1c45e44b2fc466d5f4097751
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919100"
---
# <a name="load-the-smo-assemblies-in-windows-powershell"></a>Carregar os assemblies SMO no Windows PowerShell
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Este artigo descreve como carregar os assemblies SMO (SQL Server Management Object) em scripts do Windows PowerShell que não usam o provedor do SQL Server PowerShell.  
  
> [!NOTE]
> Há dois módulos do SQL Server PowerShell; **SqlServer** e **SQLPS**. O módulo **SQLPS** está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está sendo atualizado. O módulo do PowerShell mais atualizado é o módulo do **SqlServer**. O módulo do **SqlServer** contém versões atualizadas dos cmdlets no **SQLPS** e também inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL.  
> As versões anteriores do módulo do **SqlServer** *foram* incluídas no SQL Server Management Studio (SSMS), mas apenas nas versões 16.x do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões posteriores, o módulo do **SqlServer** deve ser instalado da Galeria do PowerShell.
> Para instalar o módulo do **SqlServer**, consulte [Instalar o SQL Server PowerShell](download-sql-server-ps-module.md).


O mecanismo preferido para carregar os assemblies SMO é carregar o módulo do **SqlServer**. O provedor [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] incluído automaticamente no módulo carrega os assemblies SMO e também implementa recursos que estendem a utilidade dos objetos SMO em scripts do PowerShell.
  
Há dois casos em que você pode precisar carregar diretamente os assemblies do SMO:  
  
-   Se o script fizer referência a um objeto do SMO antes do primeiro comando que faz referência ao provedor ou a cmdlets dos snap-ins do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
