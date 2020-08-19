---
description: sp_indexoption (Transact-SQL)
title: sp_indexoption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_indexoption
- sp_indexoption_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_indexoption
ms.assetid: 75f836be-d322-4a53-a45d-25bee6b42a52
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 509d58a28f768fe774c813a8235ae4c0d9cd718a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88469224"
---
# <a name="sp_indexoption-transact-sql"></a>sp_indexoption (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Define os valores da opção de bloqueio para índices clusterizados e não clusterizados definidos pelo usuário ou tabelas sem índice clusterizado.  
  
 O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] faz automaticamente escolhas de bloqueio no nível de página, linha ou tabela. Você não precisa definir essas opções manualmente. **sp_indexoption** é fornecido para usuários especialistas que sabem com certeza que um determinado tipo de bloqueio é sempre apropriado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] Em vez disso, use [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_indexoption [ @IndexNamePattern = ] 'table_or_index_name'   
    , [ @OptionName = ] 'option_name'   
    , [ @OptionValue = ] 'value'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @IndexNamePattern = ] 'table_or_index_name'` É o nome qualificado ou não qualificado de uma tabela ou índice definido pelo usuário. *table_or_index_name* é **nvarchar (1035)**, sem padrão. As aspas são necessárias somente se um nome de índice ou tabela qualificado for especificado. Se um nome de tabela totalmente qualificado, incluindo um nome de banco de dados, for fornecido, o nome de banco de dados deve ser o nome do banco de dados atual. Se um nome de tabela for especificado sem-índice, o valor de opção especificado será definido para todos os índices nessa tabela e para a própria tabela se não houver um índice clusterizado.  
  
`[ @OptionName = ] 'option_name'` É um nome de opção de índice. *option_name* é **varchar (35)**, sem padrão. *option_name* pode ter um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**AllowRowLocks**|No caso de TRUE, são permitidos bloqueios de linha ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados. No caso de FALSE, não são usados bloqueios de linha. O padrão é TRUE.|  
|**AllowPageLocks**|No caso de TRUE, são permitidos bloqueios de página ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados. No caso de FALSE, não são usados bloqueios de página. O padrão é TRUE.|  
|**DisAllowRowLocks**|No caso de TRUE, não são usados bloqueios de linha. No caso de FALSE, são permitidos bloqueios de linha ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados.|  
|**DisAllowPageLocks**|No caso de TRUE, não são usados bloqueios de página. No caso de FALSE, são permitidos bloqueios de página ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados.|  
  
`[ @OptionValue = ] 'value'` Especifica se a configuração de *option_name* está habilitada (true, on, Yes ou 1) ou Disabled (false, off, no ou 0). o *valor* é **varchar (12)**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou superior a 0 (falha)  
  
## <a name="remarks"></a>Comentários  
 Não é oferecido suporte a índices XML. Se um índice XML for especificado, ou um nome de tabela for especificado sem nome de índice e a tabela tiver um índice XML, haverá falha na instrução. Para definir essas opções, use [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) em vez disso.  
  
 Para exibir as propriedades de bloqueio de linha e de página atuais, use [INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md) ou a exibição de catálogo [Sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) .  
  
-   Os bloqueios em nível de linha, página e tabela são permitidos ao acessar o índice quando **AllowRowLocks** = true ou **DisallowRowLocks** = false e **AllowPageLocks** = true ou **DisallowPageLocks** = false. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] escolhe o bloqueio apropriado e pode escalar o bloqueio de uma linha ou página para um bloqueio de tabela.  
  
 Somente um bloqueio em nível de tabela é permitido ao acessar o índice quando **AllowRowLocks** = false ou **DisallowRowLocks** = true e **AllowPageLocks** = false ou **DisallowPageLocks** = true.  
  
 Se um nome de tabela for especificado sem-índice, as configurações serão aplicadas a todos os índices nessa tabela. Quando a tabela subjacente não tiver índice clusterizado (ou seja, é um heap), as configurações serão aplicadas da seguinte forma:  
  
-   Quando **AllowRowLocks** ou **DisallowRowLocks** são definidos como true ou false, a configuração é aplicada ao heap e a quaisquer índices não clusterizados associados.  
  
-   Quando a opção **AllowPageLocks** é definida como true ou **DisallowPageLocks** é definida como false, a configuração é aplicada ao heap e a quaisquer índices não clusterizados associados.  
  
-   Quando a opção **AllowPageLocks** é definida como false ou **DisallowPageLocks** é definido como true, a configuração é totalmente aplicada aos índices não clusterizados. Ou seja, nenhum bloqueio de página é permitido nos índices não clusterizados. No heap, somente os bloqueios compartilhados (S, shared), de atualização (U, update) e exclusivos (X, exclusive) de página não são permitidos. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] ainda pode adquirir um bloqueio de página intencional (IS, IU ou IX) para fins internos.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão ALTER na tabela.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-an-option-on-a-specific-index"></a>a. Definindo uma opção em um índice específico  
 O exemplo a seguir não permite bloqueios de página no `IX_Customer_TerritoryID` índice na `Customer` tabela.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_indexoption N'Sales.Customer.IX_Customer_TerritoryID',  
    N'disallowpagelocks', TRUE;  
```  
  
### <a name="b-setting-an-option-on-all-indexes-on-a-table"></a>B. Definindo uma opção em todos os índices de uma tabela  
 O exemplo a seguir não permite bloqueios de linha em todos os índices associados com a tabela `Product`. A exibição do catálogo `sys.indexes` é consultada antes e depois da execução do procedimento `sp_indexoption` para mostrar os resultados da instrução.  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
-- Set the disallowrowlocks option on the Product table.   
EXEC sp_indexoption N'Production.Product',  
    N'disallowrowlocks', TRUE;  
GO  
--Verify the row and page lock options for all indexes on the table.  
SELECT name, type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE object_id = OBJECT_ID(N'Production.Product');  
GO  
```  
  
### <a name="c-setting-an-option-on-a-table-with-no-clustered-index"></a>C. Definindo uma opção em uma tabela sem índice clusterizado  
 O exemplo a seguir não permite bloqueios de página em uma tabela sem índice clusterizado (um heap). A `sys.indexes` exibição do catálogo é consultada antes e depois que o `sp_indexoption` procedimento é executado para mostrar os resultados da instrução.  
  
```sql  
USE AdventureWorks2012;  
GO  
--Display the current row and page lock options of the table.   
SELECT OBJECT_NAME (object_id) AS [Table], type_desc, allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
-- Set the disallowpagelocks option on the table.   
EXEC sp_indexoption DatabaseLog,  
    N'disallowpagelocks', TRUE;  
GO  
--Verify the row and page lock settings of the table.  
SELECT OBJECT_NAME (object_id) AS [Table], allow_row_locks, allow_page_locks   
FROM sys.indexes  
WHERE OBJECT_NAME (object_id) = N'DatabaseLog';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
