---
title: DBCC CHECKCONSTRAINTS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC CHECKCONSTRAINTS
- DBCC_CHECKCONSTRAINTS_TSQL
- CHECKCONSTRAINTS
- CHECKCONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC CHECKCONSTRAINTS statement
- consistency [SQL Server], constraints
- checking constraint consistency
- constraints [SQL Server], consistency checks
- integrity [SQL Server], constraints
ms.assetid: da6c9cee-6687-46e8-b504-738551f9068b
caps.latest.revision: 45
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5c5a15f6f5af19cd0e5da400dd4deb2cfa0d4cc4
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-checkconstraints-transact-sql"></a>DBCC CHECKCONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Inspeciona a integridade de uma restrição especificada ou de todas as restrições em uma tabela especificada no banco de dados atual.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC CHECKCONSTRAINTS  
[   
    (   
    table_name | table_id | constraint_name | constraint_id   
    )  
]  
    [ WITH   
    [ { ALL_CONSTRAINTS | ALL_ERRORMSGS } ]  
    [ , ] [ NO_INFOMSGS ]   
    ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name* | *table_id* | *constraint_name* | *constraint_id*  
 É a tabela ou restrição que será verificada. Quando *table_name* ou *table_id* é especificado, todas as restrições habilitadas na tabela são verificadas. Quando *constraint_name* ou *constraint_id* for especificado, somente essa restrição será verificada. Se nem um identificador de tabela ou um identificador de restrição for especificado, todas as restrições habilitadas em todas as tabelas no banco de dados atual serão verificadas.  
 Um nome de restrição identifica exclusivamente a tabela à qual ela pertence. Para obter mais informações, consulte [Database Identifiers](../../relational-databases/databases/database-identifiers.md).  
  
 com  
 Permite que opções sejam especificadas.  
  
 ALL_CONSTRAINTS  
 Verifica todas as restrições habilitadas e desabilitadas na tabela se o nome da tabela for especificado ou se todas as tabelas forem verificadas. Caso contrário, verificará somente a restrição habilitada. ALL_CONSTRAINTS não tem nenhum efeito quando um nome de restrição é especificado.  
  
 ALL_ERRORMSGS  
 Retorna todas as linhas que violam restrições na tabela verificada. O padrão inclui as primeiras 200 linhas.  
  
 NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
  
## <a name="remarks"></a>Comentários  
DBCC CHECKCONSTRAINTS constrói e executa uma consulta para todas as restrições FOREIGN KEY e CHECK de uma tabela.
  
Por exemplo, uma consulta de chave estrangeira tem o seguinte formato:
  
```sql
SELECT <columns>  
FROM <table_being_checked> LEFT JOIN <referenced_table>  
    ON <table_being_checked.fkey1> = <referenced_table.pkey1>   
    AND <table_being_checked.fkey2> = <referenced_table.pkey2>  
WHERE <table_being_checked.fkey1> IS NOT NULL   
    AND <referenced_table.pkey1> IS NULL  
    AND <table_being_checked.fkey2> IS NOT NULL  
    AND <referenced_table.pkey2> IS NULL  
```  
  
Os dados de consulta são armazenados em uma tabela temporária. Depois que todas as tabelas e restrições solicitadas forem verificadas, o conjunto de resultados será retornado.
DBCC CHECKCONSTRAINTS verifica a integridade das restrições FOREIGN KEY e CHECK, mas não verifica a integridade das estruturas de dados em disco de uma tabela. Essas verificações de estrutura de dados podem ser executadas usando [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) e [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md).
  
**Aplica-se a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] por meio de[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
Se *table_name* ou *table_id* é especificada e ela está habilitada para controle de versão do sistema, DBCC CHECKCONSTRAINTS também executa as verificações de consistência de dados temporais na tabela especificada. Quando *NO_INFOMSGS* não for especificado, esse comando retornará cada violação de consistência na saída em uma linha separada. O formato da saída será ([pkcol1], [pkcol2]...) = (\<pkcol1_value >, \<pkcol2_value >...) E \<o que há de errado com o registro da tabela temporal >.
  
|Verificar|Informações adicionais na saída se a falha na verificação|  
|-----------|-----------------------------------------------|  
|PeriodEndColumn ≥ PeriodStartColumn (atual)|[sys_end] = '{0}' e MAX(DATETIME2) = ' 9999-12-31 23:59:59.99999'|  
|PeriodEndColumn ≥ PeriodStartColumn (atual, histórico)|[sys_start] = '{0}' AND [sys_end] = '\\{1 \\}'|  
|PeriodStartColumn < current_utc_time (atual)|[sys_start] = '{0}' e SYSUTCTIME|  
|PeriodEndColumn < current_utc_time (histórico)|[sys_end] = '{0}' e SYSUTCTIME|  
|Sobreposições|(sys_start1, sys_end1), (sys_start2, sys_end2) para dois registros de sobreposição.<br /><br /> Se houver mais de 2 registros de sobreposição, saída terá várias linhas cada mostrando um par de sobreposições.|  
  
Não é possível especificar constraint_name ou constraint_id para executar verificações de consistência temporais somente.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC CHECKCONSTRAINTS retornam um conjunto de linhas com as colunas a seguir.
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|Nome da tabela|**varchar**|Nome da tabela.|  
|Constraint Name|**varchar**|Nome da restrição que é violada.|  
|Where|**varchar**|Atribuições de valor de coluna que identificam as linhas que violam a restrição.<br /><br /> O valor nesta coluna pode ser usado em uma cláusula WHERE de uma instrução SELECT que consulta as linhas que violam a restrição.|  
  
## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** ou à função de banco de dados fixa **db_owner** .
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-checking-a-table"></a>A. Verificando uma tabela  
O exemplo a seguir verifica a integridade de restrição da tabela `Table1` do banco de dados `AdventureWorks`.
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE TABLE Table1 (Col1 int, Col2 char (30));  
GO  
INSERT INTO Table1 VALUES (100, 'Hello');  
GO  
ALTER TABLE Table1 WITH NOCHECK ADD CONSTRAINT chkTab1 CHECK (Col1 > 100);  
GO  
DBCC CHECKCONSTRAINTS(Table1);  
GO  
```  
  
### <a name="b-checking-a-specific-constraint"></a>B. Verificando uma restrição específica  
O exemplo a seguir verifica a integridade da restrição `CK_ProductCostHistory_EndDate`.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC CHECKCONSTRAINTS ('Production.CK_ProductCostHistory_EndDate');  
GO  
```  
  
### <a name="c-checking-all-enabled-and-disabled-constraints-on-all-tables"></a>C. Verificando todas as restrições habilitadas e desabilitadas em todas as tabelas  
 O exemplo a seguir verifica a integridade de todas as restrições habilitadas e desabilitadas em todas as tabelas do banco de dados atual.  
  
```sql  
DBCC CHECKCONSTRAINTS WITH ALL_CONSTRAINTS;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
[DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)  
[DBCC CHECKTABLE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  

