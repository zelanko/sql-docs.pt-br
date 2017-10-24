---
title: DBCC UPDATEUSAGE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATEUSAGE
- UPDATEUSAGE_TSQL
- DBCC_UPDATEUSAGE_TSQL
- DBCC UPDATEUSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- inaccurate page or row counts [SQL Server]
- space [SQL Server], usage reports
- updating space usage information
- updating row counts
- disk space [SQL Server], inaccurate counts
- counting pages
- reporting count inaccuracies
- updating page counts
- synchronization [SQL Server], inaccurate counts
- incorrect space usage reports [SQL Server]
- DBCC UPDATEUSAGE statement
- integrity [SQL Server], database objects
- counting rows
- row count accuracy [SQL Server]
- page count accuracy [SQL Server]
ms.assetid: b8752ecc-db45-4e23-aee7-13b8bc3cbae2
caps.latest.revision: 56
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0e99240896bb1192a742ad2b614080e5325acc1f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-updateusage-transact-sql"></a>DBCC UPDATEUSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Relata e corrige inexatidões de contagem de páginas e linhas nas exibições do catálogo. Essas inexatidões podem provocar relatórios de uso incorreto de espaço retornados pelo procedimento armazenado do sistema sp_spaceused.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC UPDATEUSAGE   
(   { database_name | database_id | 0 }   
    [ , { table_name | table_id | view_name | view_id }   
    [ , { index_name | index_id } ] ]   
) [ WITH [ NO_INFOMSGS ] [ , ] [ COUNT_ROWS ] ]   
```  
  
## <a name="arguments"></a>Argumentos  
*Database_Name* | *database_id* | 0  
É o nome ou a ID do banco de dados na qual serão relatadas e corrigidas as estatísticas de uso de espaço. Se 0 for especificado, será usado o banco de dados atual. Nomes de banco de dados devem estar em conformidade com as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
*table_name* | *table_id* | *view_name* | *view_id*  
É o nome ou a ID da tabela ou exibição indexada para a qual serão relatadas e corrigidas as estatísticas de uso de espaço. Os nomes de tabelas e exibições devem obedecer às regras de identificadores.  
  
*index_id* | *index_name*  
É a ID ou o nome do índice a ser usado. Se não for especificado, a instrução processará todos os índices da tabela ou a exibição especificada.  
  
com  
Permite que opções sejam especificadas.  
  
NO_INFOMSGS  
Suprime todas as mensagens informativas.  
  
COUNT_ROWS  
Especifica que a coluna de contagem de linhas seja atualizada com a contagem atual do número de linhas na tabela ou na exibição.  
  
## <a name="remarks"></a>Comentários  
DBCC UPDATEUSAGE corrige as contagens das linhas, páginas usadas, páginas reservadas, páginas de folha e páginas de dados de cada partição em uma tabela ou índice. Se não houver nenhuma inexatidão nas tabelas do sistema, DBCC UPDATEUSAGE não retornará dados. Se inexatidões forem encontradas e corrigidas, e WITH NO_INFOMSGS não for usado, DBCC UPDATEUSAGE retornará as linhas e as colunas que foram atualizadas nas tabelas do sistema.
  
O DBCC CHECKDB foi aprimorado para detectar quando as contagens de páginas ou de linhas se tornam negativas. Quando detectada, a saída do DBCC CHECKDB contém um aviso e uma recomendação para executar DBCC UPDATEUSAGE para resolver o problema.
  
## <a name="best-practices"></a>Práticas recomendadas  
Recomendamos o seguinte:
-   Não execute DBCC UPDATEUSAGE rotineiramente. Como DBCC UPDATEUSAGE pode levar algum tempo para ser executado em tabelas ou bancos de dados grandes, não deve ser usado, a não ser que você suspeite que valores incorretos estão sendo retornados por sp_spaceused.
-   Considere a execução de DBCC UPDATEUSAGE rotineiramente (por exemplo, semanalmente) somente se o banco de dados passar por modificações de DDL (Linguagem de definição de dados) frequentes, como instruções CREATE, ALTER ou DROP.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC UPDATEUSAGE retorna (os valores podem variar):
  
`DBCC execution completed. If DBCC printed error messages, contact your system administrator.`
  
## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-updating-page-or-row-counts-or-both-for-all-objects-in-the-current-database"></a>A. Atualizando as contagens de páginas ou de linhas ou de ambas para todos os objetos do banco de dados atual  
O exemplo a seguir especifica `0` para o nome do banco de dados, e `DBCC UPDATEUSAGE` relata informações sobre contagem de páginas ou de linhas atualizadas para o banco de dados atual.
  
```sql
DBCC UPDATEUSAGE (0);  
GO  
```  
  
### <a name="b-updating-page-or-row-counts-or-both-for-adventureworks-and-suppressing-informational-messages"></a>B. Atualizando contagens de páginas ou de linhas ou de ambas para o AdventureWorks e suprimindo mensagens informativas  
O exemplo a seguir especifica [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] como o nome do banco de dados e suprime todas as mensagens informativas.
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012) WITH NO_INFOMSGS;   
GO  
```  
  
### <a name="c-updating-page-or-row-counts-or-both-for-the-employee-table"></a>C. Atualizando contagens de páginas ou de linhas ou de ambas para a tabela Employee  
O exemplo a seguir relata as informações atualizadas de contagem de página ou linha para o `Employee` tabela o [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] banco de dados.
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012,'HumanResources.Employee');  
GO  
```  
  
### <a name="d-updating-page-or-row-counts-or-both-for-a-specific-index-in-a-table"></a>D. Atualizando contagens de páginas ou de linhas ou de ambas para um índice específico em uma tabela  
 O exemplo a seguir especifica `IX_Employee_ManagerID` como o nome do índice.  
  
```sql
DBCC UPDATEUSAGE (AdventureWorks2012, 'HumanResources.Employee', IX_Employee_OrganizationLevel_OrganizationNode);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_spaceused &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)  
[UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)
  
  

