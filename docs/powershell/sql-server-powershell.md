---
title: SQL Server PowerShell
description: Saiba mais sobre os dois módulos SQL Server PowerShell, SqlServer e SQLPS, que incluem provedores e cmdlets do PowerShell.
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 89b70725-bbe7-4ffe-a27d-2a40005a97e7
author: markingmyname
ms.author: maghan
ms.reviewer: matteot
ms.custom: ''
ms.date: 06/11/2020
ms.openlocfilehash: 968bcd1560fd4fd24dddfaf45cfe606518235b60
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081885"
---
# <a name="sql-server-powershell"></a>SQL Server PowerShell

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

**[Instalar o SQL Server PowerShell](download-sql-server-ps-module.md)**

Há dois módulos do SQL Server PowerShell; **[SqlServer](https://docs.microsoft.com/powershell/module/sqlserver)** e **[SQLPS](https://docs.microsoft.com/powershell/module/sqlps)** .

O módulo **SqlServer** é o módulo atual do PowerShell a ser usado.

O módulo **SQLPS** está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está mais sendo atualizado.

O módulo do **SqlServer** contém versões atualizadas dos cmdlets no **SQLPS** e inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL.

As versões anteriores do módulo **SqlServer** *foram* incluídas no [SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md), mas apenas nas versões 16.x do SSMS.

Para usar o PowerShell com o SSMS 17.0 e posteriores, instale o módulo **SqlServer** da [Galeria do PowerShell](https://www.powershellgallery.com/packages/SqlServer).

Você também pode usar o [PowerShell com o Azure Data Studio](../azure-data-studio/extensions/powershell-extension.md).

**Por que o módulo foi alterado de SQLPS para SqlServer?**

Para enviar atualizações do SQL PowerShell, precisamos alterar a identidade do módulo do SQL PowerShell e o wrapper conhecido como *SQLPS.exe*. Devido a essa alteração, agora existem dois módulos do PowerShell do SQL, o módulo do **SqlServer** e o módulo do **SQLPS**.  

**Atualize seus scripts do PowerShell se você importar o módulo SQLPS.**

Se você tiver qualquer script do PowerShell que executa `Import-Module -Name SQLPS` e desejar aproveitar a nova funcionalidade do provedor e os novos cmdlets, você deverá alterá-los para `Import-Module -Name SqlServer`. O novo módulo é instalado na pasta `%ProgramFiles%\WindowsPowerShell\Modules\SqlServer`. Portanto, você não precisa atualizar a variável $env:PSModulePath. Se você tiver scripts que usam uma versão de terceiros ou comunitária de um módulo chamado **SqlServer**, use o parâmetro de prefixo para evitar colisões de nome.

Recomendamos iniciar o script com *Import-Module SQLServer* para evitar problemas lado a lado caso o módulo SQLPS esteja instalado no mesmo computador.

Esta seção se aplica aos scripts executados no PowerShell e não ao SQL Agent. O novo módulo pode ser usado com etapas de trabalho do SQL Agent por meio de [#NOSQLPS](#sql-server-agent).

## <a name="sql-server-powershell-components"></a>Componentes do SQL Server PowerShell

O módulo **SqlServer** é fornecido com:

- [Provedores do PowerShell](/powershell/module/microsoft.powershell.core/about/about_providers), que habilita um mecanismo de navegação simples semelhante aos caminhos do sistema de arquivos. Crie caminhos semelhantes aos caminhos do sistema de arquivos, nos quais a unidade é associada ao modelo de objeto de gerenciamento do SQL Server e os nós se baseiam nas classes de modelo do objeto. Você pode usar os comandos conhecidos, como **cd** e **dir** , para navegar pelos caminhos de maneira semelhante à forma como navega pelas pastas em uma janela do prompt de comando. Também pode usar outros comandos, como **ren** ou **del**, para executar ações nos nós no caminho.

- Um conjunto de cmdlets que dá suporte a ações, como a execução de um script **sqlcmd** que contém instruções Transact-SQL ou XQuery.  

- Os cmdlets e o provedor do AS, que antes eram instalados separadamente.

## <a name="sql-server-versions"></a>Versões do SQL Server

Os cmdlets do SQL PowerShell podem ser usados para gerenciar instâncias do Banco de Dados SQL do Azure, do Azure Synapse Analytics e de todos os [produtos compatíveis com SQL Server](https://support.microsoft.com/lifecycle/search/1044).

## <a name="sql-server-identifiers-that-contain-characters-not-supported-in-powershell-paths"></a>Os identificadores do SQL Server que contêm caracteres sem suporte em caminhos do PowerShell

Os cmdlets **Encode-Sqlname** e **Decode-Sqlname** ajudam a especificar identificadores do SQL Server que contêm caracteres sem suporte em caminhos do PowerShell. Para obter mais informações, consulte [SQL Server Identifiers in PowerShell](sql-server-identifiers-in-powershell.md).

Use o cmdlet **Convert-UrnToPath** para converter um nome de recurso exclusivo de um objeto do Mecanismo de Banco de Dados para um caminho do provedor do SQL Server PowerShell. Para obter mais informações, consulte [Convert URNs to SQL Server Provider Paths](/powershell/module/sqlserver/Convert-UrnToPath).
  
## <a name="query-expressions-and-unique-resource-names"></a>Expressões de consultas e URNs (Unique Resource Names)  

As expressões de consulta são cadeias de caracteres que usam uma sintaxe similar à do XPath para especificar um conjunto de critérios que enumera um ou mais objetos em uma hierarquia de modelo de objetos. Um URN (Unique Resource Name) é um tipo específico de cadeia de caracteres de expressão de consulta que identifica exclusivamente um único objeto. Para obter mais informações, consulte [Query Expressions and Uniform Resource Names](query-expressions-and-uniform-resource-names.md).

## <a name="sql-server-agent"></a>SQL Server Agent

Não há nenhuma alteração no módulo usado pelo SQL Server Agent. Portanto, os trabalhos do SQL Server Agent, que têm etapas de trabalho do tipo PowerShell, usam o módulo SQLPS. Para obter mais informações, confira [Como executar o PowerShell com o SQL Server Agent](run-windows-powershell-steps-in-sql-server-agent.md). No entanto, do SQL Server 2019 em diante, é possível desabilitar o SQLPS. Para fazer isso, na primeira linha de uma etapa de trabalho do tipo PowerShell, você pode adicionar `#NOSQLPS`, o que impede o SQL Agent de carregar automaticamente o módulo SQLPS. Quando você faz isso, o trabalho do SQL Agent executa a versão do PowerShell instalada no computador e você pode usar qualquer outro módulo do PowerShell desejado.

Se você quiser usar o módulo **SqlServer** na etapa de trabalho do SQL Agent, coloque esse código nas duas primeiras linhas do script.

```powershell
#NOSQLPS
Import-Module -Name SqlServer
```

## <a name="cmdlet-reference"></a>Referência de cmdlet

- [Cmdlets do SqlServer](/powershell/module/sqlserver)
- [Cmdlets do SQLPS](/powershell/module/sqlps)

## <a name="next-steps"></a>Próximas etapas

- [Baixar o módulo do PowerShell do SQL Server](download-sql-server-ps-module.md)
- [Cmdlets do SQL Server PowerShell](/powershell/module/sqlserver)
- [Usar o PowerShell com o Azure Data Studio](../azure-data-studio/extensions/powershell-extension.md)
