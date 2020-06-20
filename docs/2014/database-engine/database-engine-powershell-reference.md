---
title: Referência do Mecanismo de Banco de Dados com o PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3c379a43-c497-47dd-8e7d-2b015c068bb7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5412b8a96f79f0c33206c794090916732ef016a8
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934457"
---
# <a name="database-engine-powershell-reference"></a>Referência do Mecanismo de Banco de Dados com o PowerShell
  O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] inclui um conjunto de cmdlets de Windows PowerShell 2.0 para executar ações comuns no [!INCLUDE[ssDE](../includes/ssde-md.md)]. Além disso, expressões de consulta e URNs podem ser convertidos em caminhos do SQL Server PowerShell ou usados para especificar um ou mais objetos no [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
## <a name="database-engine-cmdlets"></a>Cmdlets do Mecanismo de Banco de Dados  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] inclui cmdlets relativamente poucos para o [!INCLUDE[ssDE](../includes/ssde-md.md)]. A maioria dos scripts do PowerShell que funciona com o [!INCLUDE[ssDE](../includes/ssde-md.md)] usa o provedor do SQL Server PowerShell e os modelos de objeto de gerenciamento. Para obter mais informações, consulte [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md).  
  
 Para saber como obter ajuda sobre o cmdlets do SQL Server em um ambiente do Windows PowerShell, consulte [Get Help SQL Server PowerShell](../powershell/sql-server-powershell.md).  
  
### <a name="in-this-section"></a>Nesta seção  
 Esta seção contém informações sobre esses cmdlets.  
  
|Descrição|Cmdlet|  
|-----------------|------------|  
|Executa scripts Transact-SQL e XQuery, como scripts que podem ser executados usando o utilitário `sqlcmd`.|[cmdlet Invoke-Sqlcmd](../../2014/database-engine/invoke-sqlcmd-cmdlet.md)|  
|Avalia se um objeto do Mecanismo de Banco de Dados obedece a uma política gerenciamento baseado em políticas.|[cmdlet Invoke-PolicyEvaluation](../../2014/database-engine/invoke-policyevaluation-cmdlet.md)|  
  
### <a name="information-about-other-cmdlets"></a>Informações sobre outros cmdlets  
 Os cmdlets `Encode-Sqlname` e `Decode-Sqlname` ajudam a especificar identificadores do SQL Server que contêm caracteres sem suporte em caminhos do PowerShell. Para obter mais informações, consulte [SQL Server Identifiers in PowerShell](../powershell/sql-server-identifiers-in-powershell.md).  
  
 Use o cmdlet `Convert-UrnToPath` para converter um nome de recurso exclusivo de um objeto do [!INCLUDE[ssDE](../includes/ssde-md.md)] para um caminho do provedor do SQL Server PowerShell. Para obter mais informações, consulte [Convert URNs to SQL Server Provider Paths](../../2014/database-engine/convert-urns-to-sql-server-provider-paths.md).  
  
## <a name="query-expressions-and-unique-resource-names"></a>Expressões de consultas e URNs (Unique Resource Names)  
 As expressões de consulta são cadeias de caracteres que usam sintaxe similar à do XPath para especificar um conjunto de critérios que enumera um ou mais objetos em uma hierarquia de modelo de objetos. Um URN (Unique Resource Name) é um tipo específico de cadeia de caracteres de expressão de consulta que identifica exclusivamente um único objeto. Para obter mais informações, consulte [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
