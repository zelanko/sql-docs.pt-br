---
title: sp_indexoption (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_indexoption
- sp_indexoption_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_indexoption
ms.assetid: 75f836be-d322-4a53-a45d-25bee6b42a52
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8b5b63c7f76695853ab216aee1aaab63a3139cc2
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="spindexoption-transact-sql"></a>sp_indexoption (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define os valores da opção de bloqueio para índices clusterizados e não clusterizados definidos pelo usuário ou tabelas sem índice clusterizado.  
  
 O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] faz automaticamente escolhas de bloqueio no nível de página, linha ou tabela. Você não precisa definir essas opções manualmente. **sp_indexoption** é fornecido para usuários especialistas que sabem com certeza que um determinado tipo de bloqueio sempre é apropriado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)]Em vez disso, use [ALTER INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-index-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_indexoption [ @IndexNamePattern = ] 'table_or_index_name'   
    , [ @OptionName = ] 'option_name'   
    , [ @OptionValue = ] 'value'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@IndexNamePattern=**] **'***table_or_index_name***'**  
 É o nome qualificado ou não qualificado de uma tabela ou índice definido pelo usuário. *table_or_index_name* é **nvarchar(1035)**, sem padrão. As aspas são necessárias somente se um nome de índice ou tabela qualificado for especificado. Se um nome de tabela totalmente qualificado, incluindo um nome de banco de dados, for fornecido, o nome de banco de dados deve ser o nome do banco de dados atual. Se um nome de tabela for especificado sem-índice, o valor de opção especificado será definido para todos os índices nessa tabela e para a própria tabela se não houver um índice clusterizado.  
  
 [  **@OptionName =**] **'***option_name***'**  
 É um nome de opção de índice. *option_name* é **varchar (35)**, sem padrão. *option_name* pode ter um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**AllowRowLocks**|No caso de TRUE, são permitidos bloqueios de linha ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados. No caso de FALSE, não são usados bloqueios de linha. O padrão é TRUE.|  
|**AllowPageLocks**|No caso de TRUE, são permitidos bloqueios de página ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados. No caso de FALSE, não são usados bloqueios de página. O padrão é TRUE.|  
|**DisAllowRowLocks**|No caso de TRUE, não são usados bloqueios de linha. No caso de FALSE, são permitidos bloqueios de linha ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de linha são usados.|  
|**DisAllowPageLocks**|No caso de TRUE, não são usados bloqueios de página. No caso de FALSE, são permitidos bloqueios de página ao acessar o índice. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina quando os bloqueios de página são usados.|  
  
 [  **@OptionValue =**] **'***valor***'**  
 Especifica se o *option_name* configuração estiver habilitada (TRUE, ON, Sim ou 1) ou desabilitado (FALSE, OFF, não ou 0). *valor* é **varchar(12)**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou superior a 0 (falha)  
  
## <a name="remarks"></a>Remarks  
 Não é oferecido suporte a índices XML. Se um índice XML for especificado, ou um nome de tabela for especificado sem nome de índice e a tabela tiver um índice XML, haverá falha na instrução. Para definir essas opções, use [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) em vez disso.  
  
 Para exibir a linha atual e a página de propriedades de bloqueio, use [INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md) ou [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) exibição do catálogo.  
  
-   Linha, página e bloqueios de nível de tabela são permitidos ao acessar o índice quando **AllowRowLocks** = TRUE ou **DisAllowRowLocks** = FALSE, e **AllowPageLocks** = TRUE ou  **DisAllowPageLocks** = FALSE. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] escolhe o bloqueio apropriado e pode escalar o bloqueio de uma linha ou página para um bloqueio de tabela.  
  
 Somente um bloqueio de nível de tabela é permitido ao acessar o índice quando **AllowRowLocks** = FALSE ou **DisAllowRowLocks** = TRUE e **AllowPageLocks** = FALSE ou  **DisAllowPageLocks** = TRUE.  
  
 Se um nome de tabela for especificado sem-índice, as configurações serão aplicadas a todos os índices nessa tabela. Quando a tabela subjacente não tiver índice clusterizado (ou seja, é um heap), as configurações serão aplicadas da seguinte forma:  
  
-   Quando **AllowRowLocks** ou **DisAllowRowLocks** estiver definido como TRUE ou FALSE, a configuração é aplicada ao heap e quaisquer índices não clusterizados associados.  
  
-   Quando **AllowPageLocks** opção é definida como TRUE ou **DisAllowPageLocks** é definido como FALSE, a configuração é aplicada ao heap e quaisquer índices não clusterizados associados.  
  
-   Quando **AllowPageLocks** opção for definida como FALSE ou **DisAllowPageLocks** é definida como TRUE, a configuração será totalmente aplicada os índices não clusterizados. Ou seja, nenhum bloqueio de página é permitido nos índices não clusterizados. No heap, somente os bloqueios compartilhados (S, shared), de atualização (U, update) e exclusivos (X, exclusive) de página não são permitidos. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] ainda pode adquirir um bloqueio de página intencional (IS, IU ou IX) para fins internos.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão ALTER na tabela.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-setting-an-option-on-a-specific-index"></a>A. Definindo uma opção em um índice específico  
 O exemplo a seguir não permite bloqueios de página sobre o `IX_Customer_TerritoryID` índice no `Customer` tabela.  
  
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
 O exemplo a seguir não permite bloqueios de página em uma tabela sem índice clusterizado (um heap). O `sys.indexes` exibição do catálogo é consultada antes e após o `sp_indexoption` procedimento é executado para mostrar os resultados da instrução.  
  
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
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
