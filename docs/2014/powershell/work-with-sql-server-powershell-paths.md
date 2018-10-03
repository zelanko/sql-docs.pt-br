---
title: Trabalhar com caminhos do SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: f31d8e2c-8d59-4fee-ac2a-324668e54262
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: af8f20f14ed02a351101580566ab7b6393c24c52
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48059736"
---
# <a name="work-with-sql-server-powershell-paths"></a>Trabalhar com caminhos do SQL Server PowerShell
  Depois de navegar para um nó em um caminho de provedor do [!INCLUDE[ssDE](../includes/ssde-md.md)] , pode executar trabalho ou recuperar informações usando os métodos e as propriedades do objeto de gerenciamento do [!INCLUDE[ssDE](../includes/ssde-md.md)] associado com o nó.  
  
1.  [Antes de começar](#BeforeYouBegin)  
  
2.  **To work on a path node:**  [Listing Methods and Properties](#ListPropMeth), [Using Methods and Properties](#UsePropMeth)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
 Depois de navegar até um nó em um caminho do provedor do [!INCLUDE[ssDE](../includes/ssde-md.md)] , você poderá executar dois tipos de ações:  
  
-   Você pode executar os cmdlets do Windows PowerShell que funcionam em nós, como **Rename-Item**.  
  
-   Você pode chamar os métodos do modelo de objeto de gerenciamento associado do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , como SMO. Por exemplo, se você navegar até o nó Banco de Dados em um caminho, poderá usar os métodos e as propriedades da classe <xref:Microsoft.SqlServer.Management.Smo.Database> .  
  
 O provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é usado para gerenciar os objetos em uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)]. Ele não é usado para trabalhar com dados em bancos de dados. Se você navegou até uma tabela ou exibição, não é possível usar o provedor para selecionar, inserir, atualizar ou excluir dados. Use o cmdlet **Invoke-Sqlcmd** para consultar ou alterar dados em tabelas e exibições do ambiente do Windows PowerShell. Para obter mais informações, veja [Cmdlet Invoke-Sqlcmd](../database-engine/invoke-sqlcmd-cmdlet.md).  
  
##  <a name="ListPropMeth"></a> Listando métodos e propriedades  
 **Listando métodos e propriedades**  
  
 Para exibir os métodos e as propriedades disponíveis para objetos ou classes de objetos específicos, use o cmdlet **Get-Member** .  
  
### <a name="examples-listing-methods-and-properties"></a>Exemplos: listando métodos e propriedades  
 Este exemplo define uma variável do Windows PowerShell para a classe SMO <xref:Microsoft.SqlServer.Management.Smo.Database> e lista os métodos e as propriedades:  
  
```  
$MyDBVar = New-Object Microsoft.SqlServer.Management.SMO.Database  
$MyDBVar | Get-Member –Type Methods  
$MyDBVar | Get-Member -Type Properties  
```  
  
 Você também pode usar **Get-Member** para listar os métodos e as propriedades associadas ao nó final de um caminho do Windows PowerShell.  
  
 Este exemplo navega até o nó Bancos de Dados em um caminho SQLSERVER: e lista as propriedades da coleção:  
  
```  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
Get-Item . | Get-Member -Type Properties  
```  
  
 Este exemplo navega até o nó AdventureWorks2012 em um caminho SQLSERVER: e lista as propriedades dos objetos:  
  
```  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012  
Get-Item . | Get-Member -Type Properties  
```  
  
##  <a name="UsePropMeth"></a> Usando métodos e propriedades  
 **Usando métodos e propriedades do SMO**  
  
 Para executar trabalhos em objetos de um caminho de provedor do [!INCLUDE[ssDE](../includes/ssde-md.md)] , você pode usar métodos e propriedades do SMO.  
  
### <a name="examples-using-methods-and-properties"></a>Exemplos: usando métodos e propriedades  
 Este exemplo usa a propriedade SMO **Schema** para obter a lista de tabelas do esquema Sales em AdventureWorks2012:  
  
```  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Tables  
Get-ChildItem | where {$_.Schema -eq "Sales"}  
```  
  
 Este exemplo usa o SMO **Script** método para gerar um script que contém o `CREATE VIEW` instruções, você deve ter para recriar as exibições em AdventureWorks2012:  
  
```  
Remove-Item C:\PowerShell\CreateViews.sql  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012\Views  
foreach ($Item in Get-ChildItem) { $Item.Script() | Out-File -Filepath C:\PowerShell\CreateViews.sql -append }  
```  
  
 Este exemplo usa o método **Create** do SMO para criar um banco de dados e usa a propriedade **State** para mostrar se o banco de dados existe:  
  
```  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
$MyDBVar = New-Object Microsoft.SqlServer.Management.SMO.Database  
$MyDBVar.Parent = (Get-Item ..)  
$MyDBVar.Name = "NewDB"  
$MyDBVar.Create()  
$MyDBVar.State  
```  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [Navegar em caminhos do SQL Server PowerShell](navigate-sql-server-powershell-paths.md)   
 [Converter URNs em caminhos de provedor SQL Server](../database-engine/convert-urns-to-sql-server-provider-paths.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
