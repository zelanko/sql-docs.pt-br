---
title: Navegar em caminhos do PowerShell SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: d68aca48-d161-45ed-9f4f-14122ed30218
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce1e3a2088214c222cd2c2e84fc333f4993b7a6b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72797806"
---
# <a name="navigate-sql-server-powershell-paths"></a>Navegar em caminhos do SQL Server PowerShell
  O provedor do [!INCLUDE[ssDE](../includes/ssde-md.md)] PowerShell expõe o conjunto de objetos em uma instância do SQL Server em uma estrutura semelhante a um caminho de arquivo. Você pode usar cmdlets do Windows PowerShell para navegar até o caminho do provedor e criar unidades personalizadas para encurtar o caminho que você tem que digitar.  
  
## <a name="before-you-begin"></a>Antes de começar  
 O Windows PowerShell implementa cmdlets para navegar na estrutura do caminho que representa a hierarquia de objetos por um provedor do PowerShell. Ao navegar até um nó do caminho, você pode usar outros cmdlets para executar operações básicas no objeto atual. Como os cmdlets são usados com frequência, eles têm aliases pequenos e canônicos. Também existe um conjunto de aliases que mapeia os cmdlets para comandos semelhantes do prompt de comando e outro conjunto para comandos shell do UNIX.  
  
 O provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] implementa um subconjunto de cmdlets do provedor, mostrados na tabela a seguir:  
  
|cmdlet|Alias canônico|Alias de cmd|Alias de shell do UNIX|Descrição|  
|------------|---------------------|---------------|----------------------|-----------------|  
|**Get-Location**|**gl**|**pwd**|**pwd**|Obtém o nó atual.|  
|`Set-Location`|**SL**|**cd, chdir**|**cd, chdir**|Altera o nó atual.|  
|**Get-ChildItem**|**gci**|**dir**|**ls**|Lista os objetos armazenados no nó atual.|  
|**Get-Item**|**gi**|||Retorna as propriedades do item atual.|  
|**Renomear-item**|**rni**|**RN**|**ren**|Renomeia um objeto.|  
|**Remover item**|**ri**|**del, rd**|**rm, rmdir**|Remove um objeto.|  
  
> [!IMPORTANT]  
>  Alguns identificadores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (nomes de objeto) contêm caracteres não suportados pelos nomes de caminho do Windows PowerShell. Para obter mais informações sobre como usar os nomes que contêm esses caracteres, consulte [SQL Server Identifiers in PowerShell](sql-server-identifiers-in-powershell.md).  
  
### <a name="sql-server-information-returned-by-get-childitem"></a>Informações do SQL Server retornadas por Get-ChildItem  
 A informações retornadas por **Get-ChildItem** (ou seus aliases **dir** e **ls** ) dependem de seu local em um caminho SQLSERVER:.  
  
|Local do caminho|Resultados de Get-ChildItem|  
|-------------------|----------------------------|  
|SQLSERVER:\SQL|Retorna o nome do computador local. Se você usou o SMO ou o WMI para se conectar às instâncias do [!INCLUDE[ssDE](../includes/ssde-md.md)] em outros computadores, esses computadores também estarão listados.|  
|SqlServer: \ SQL\\*ComputerName*|A lista de instâncias do [!INCLUDE[ssDE](../includes/ssde-md.md)] no computador.|  
|SqlServer: \ SQL\\*ComputerName*\\*InstanceName*|A lista de tipos de objeto de nível superior na instância, como Pontos de Extremidade, Certificados e Bancos de Dados.|  
|Nó da classe de objeto, como Bancos de Dados|A lista de objetos desse tipo, como a lista de bancos de dados: master, model, AdventureWorks20008R2.|  
|Nó do nome de objeto, como AdventureWorks2012|A lista de tipos de objeto contida no objeto. Por exemplo, um banco de dados poderia listar tipos de objeto, como tabelas e exibições.|  
  
 Por padrão, **Get-ChildItem** não lista nenhum objeto de sistema. Use o parâmetro *Force* para ver objetos de sistema, como os objetos no esquema **sys** .  
  
### <a name="custom-drives"></a>Unidades personalizadas  
 O Windows PowerShell permite que os usuários definam unidades virtuais que são conhecidas como unidades PowerShell. Elas mapeiam os nós iniciais de uma instrução de caminho. Em geral, elas são usadas para encurtar caminhos que são digitados com frequência. SQLSERVER: os caminhos podem se tornar longos, ocupando muito espaço na janela do Windows PowerShell e exigindo muita digitação. Se você vai trabalhar muito em um nó de caminho específico, é possível definir uma unidade personalizada do Windows PowerShell mapeada para esse nó.  
  
## <a name="use-powershell-cmdlet-aliases"></a>Usar aliases de cmdlet do PowerShell  
 **Usar um alias de cmdlet**  
  
-   Em vez de digitar um nome de cmdlet completo, digite um alias mais curto ou um que mapeia para um prompt de comando familiar.  
  
### <a name="alias-example-powershell"></a>Exemplo de alias (PowerShell)  
 Por exemplo, você pode usar um dos conjuntos de cmdlets ou aliases a seguir para recuperar uma listagem das instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] disponíveis navegando para a pasta SQLSERVER:\SQL e solicitando a lista de itens filho da pasta:  
  
```powershell
## Shows using the full cmdet name.  
Set-Location SQLSERVER:\SQL  
Get-ChildItem  
  
## Shows using canonical aliases.  
sl SQLSERVER:\SQL  
gci  
  
## Shows using command prompt aliases.  
cd SQLSERVER:\SQL  
dir  
  
## Shows using Unix shell aliases.  
cd SQLSERVER:\SQL  
ls  
```  
  
## <a name="use-get-childitem"></a>Usar Get-ChildItem  

### <a name="return-information-by-using-get-childitem"></a>Retornar informações usando Get-Childitem
  
1.  Navegue até o nó para o qual você deseja uma lista de childrem  
  
2.  Execute Get-Childitem para obter a lista.  
  
### <a name="get-childitem-example-powershell"></a>Exemplo de Get-ChildItem (PowerShell)  
 Estes exemplos ilustram as informações retornadas por Get-Childitem para nós diferentes em um caminho de provedor do SQL Server.  
  
```powershell
## Return the current computer and any computer  
## to which you have made a SQL or WMI connection.  
Set-Location SQLSERVER:\SQL  
Get-ChildItem  
  
## List the instances of the Database Engine on the local computer.  
Set-Location SQLSERVER:\SQL\localhost  
Get-ChildItem  
  
## Lists the categories of objects available in the  
## default instance on the local computer.  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT  
Get-ChildItem  
  
## Lists the databases from the local default instance.  
## The force parameter is used to include the system databases.  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
Get-ChildItem -force  
```  
  
## <a name="create-a-custom-drive"></a>Criar uma unidade personalizada  

### <a name="create-and-use-a-custom-drive"></a>Criar e usar uma unidade personalizada
  
1.  Use `New-PSDrive` para definir uma unidade personalizada. Use o parâmetro `Root` para especificar o caminho que é representado pelo nome de unidade personalizada.  
  
2.  Referencie o nome de unidade personalizada em cmdlets de navegação do caminho como `Set-Location`.  
  
### <a name="custom-drive-example-powershell"></a>Exemplo de unidade personalizada (PowerShell)  
 Este exemplo cria uma unidade virtual chamada AWDB que é mapeada para o nó de uma cópia implantada do banco de dados de exemplo AdventureWorks2012. A unidade virtual é usada para navegar até uma tabela no banco de dados.  
  
```powershell
## Create a new virtual drive.  
New-PSDrive -Name AWDB -Root SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012  
  
## Use AWDB: to navigate to a specific table.  
Set-Location AWDB:\Tables\Purchasing.Vendor  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Provedor de SQL Server PowerShell](sql-server-powershell-provider.md)   
 [Trabalhar com caminhos de SQL Server PowerShell](work-with-sql-server-powershell-paths.md)   
 [Converter URNs em caminhos de provedor SQL Server](../database-engine/convert-urns-to-sql-server-provider-paths.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
