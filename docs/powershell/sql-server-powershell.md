---
title: SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 08/04/2016
ms.prod: sql-non-specified
ms.prod_service: powershell
ms.service: ''
ms.component: powershell
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: d9dc11888ffd63ad97031e666d4e63893dc2db3e
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

**[Instalar o SQL Server PowerShell](download-sql-server-ps-module.md)**

> [!NOTE]
> Há dois módulos do SQL Server PowerShell; **SqlServer** e **SQLPS**. O módulo **SQLPS** está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está sendo atualizado. O módulo do PowerShell mais atualizado é o módulo do **SqlServer**. O módulo do **SqlServer** contém versões atualizadas dos cmdlets no **SQLPS** e também inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL.  
> As versões anteriores do módulo do **SqlServer** *foram* incluídas no SQL Server Management Studio (SSMS), mas apenas nas versões 16.x do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões posteriores, o módulo do **SqlServer** deve ser instalado da Galeria do PowerShell.
> Para instalar o módulo do **SqlServer**, consulte [Instalar o SQL Server PowerShell](download-sql-server-ps-module.md).

**Por que o módulo foi alterado de SQLPS para SqlServer?**

Para enviar atualizações do SQL PowerShell, tivemos que alterar a identidade do módulo do SQL PowerShell, bem como o wrapper conhecido como *SQLPS.exe*. Devido a essa alteração, agora existem dois módulos do PowerShell do SQL, o módulo do **SqlServer** e o módulo do **SQLPS**.  

**Atualize seus scripts do PowerShell se eles importarem o módulo do SQLPS.**

Se você tiver qualquer script do PowerShell que executa `Import-Module -Name SQLPS` e desejar aproveitar a nova funcionalidade do provedor e os novos cmdlets, você deverá alterá-los para `Import-Module -Name SqlServer`. O novo módulo é instalado na pasta `%ProgramFiles%\WindowsPowerShell\Modules\SqlServer`. Portanto, você não precisa atualizar a variável $env:PSModulePath. Se você tiver scripts que usam uma versão de terceiros ou comunitária de um módulo chamado **SqlServer**, use o parâmetro de prefixo para evitar colisões de nome. Não há nenhuma alteração no módulo usado pelo SQL Server Agent. 

  
## <a name="sql-server-powershell-components"></a>Componentes do SQL Server PowerShell  
O módulo do **SqlServer** carrega dois snap-ins do Windows PowerShell:  
  
-   Um provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , que ativa um mecanismo de navegação simples semelhante aos caminhos de sistema de arquivos. É possível criar caminhos semelhantes aos caminhos de sistema de arquivos, onde a unidade é associada ao modelo de objeto de gerenciamento do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e os nós baseiam-se nas classes de modelo do objeto. Você pode usar os comandos conhecidos, como **cd** e **dir** , para navegar pelos caminhos de maneira semelhante à forma como navega pelas pastas em uma janela do prompt de comando. Também pode usar outros comandos, como **ren** ou **del**, para executar ações nos nós no caminho.  
  
-   Um conjunto de cmdlets que dão suporte a ações, como a execução de um script **sqlcmd** que contém instruções [!INCLUDE[tsql](../includes/tsql-md.md)] ou XQuery.  
  
  
## <a name="sql-server-versions"></a>Versões do SQL Server  
Os cmdlets do SQL PowerShell podem ser usados para gerenciar instâncias do Banco de Dados SQL do Azure, SQL Data Warehouse do Azure e todos os [produtos compatíveis com SQL Server](https://support.microsoft.com/lifecycle/search/1044).  


## <a name="sql-server-identifiers-that-contain-characters-not-supported-in-powershell-paths"></a>Os identificadores do SQL Server que contêm caracteres sem suporte em caminhos do PowerShell  
 
Os cmdlets **Encode-Sqlname** e **Decode-Sqlname** ajudam a especificar identificadores do SQL Server que contêm caracteres sem suporte em caminhos do PowerShell. Para obter mais informações, consulte [SQL Server Identifiers in PowerShell](sql-server-identifiers-in-powershell.md).  
  
Use o cmdlet **Convert-UrnToPath** para converter um nome de recurso exclusivo de um objeto do [!INCLUDE[ssDE](../includes/ssde-md.md)] para um caminho do provedor do SQL Server PowerShell. Para obter mais informações, consulte [Convert URNs to SQL Server Provider Paths](https://docs.microsoft.com/powershell/module/sqlserver/Convert-UrnToPath).  
  
## <a name="query-expressions-and-unique-resource-names"></a>Expressões de consultas e URNs (Unique Resource Names)  

As expressões de consulta são cadeias de caracteres que usam sintaxe similar à do XPath para especificar um conjunto de critérios que enumera um ou mais objetos em uma hierarquia de modelo de objetos. Um URN (Unique Resource Name) é um tipo específico de cadeia de caracteres de expressão de consulta que identifica exclusivamente um único objeto. Para obter mais informações, consulte [Query Expressions and Uniform Resource Names](query-expressions-and-uniform-resource-names.md).       


## <a name="cmdlet-reference"></a>Referência de cmdlet
* [Cmdlets do SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)
* [Cmdlets do SQLPS](https://docs.microsoft.com/powershell/module/sqlps)
