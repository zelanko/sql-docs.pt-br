---
title: sp_help_fulltext_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables
- sp_help_fulltext_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables
ms.assetid: 86e24a5f-a869-43f6-b83e-c52b7b01b5ff
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 73189dfb75f9a9debca373d09cc55b09aece7be3
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760062"
---
# <a name="sp_help_fulltext_tables-transact-sql"></a>sp_help_fulltext_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma lista de tabelas que estão registradas para indexação de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use a exibição de catálogo **Sys. fulltext_indexes** em vez disso. Para obter mais informações, consulte [Sys. fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_fulltext_tables [ [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'`É o nome do catálogo de texto completo. *fulltext_catalog_name* é **sysname**, com um padrão de NULL. Se *fulltext_catalog_name* for omitido ou for NULL, todas as tabelas indexadas de texto completo associadas ao banco de dados serão retornadas. Se *fulltext_catalog_name* for especificado, mas *table_name* for omitido ou for NULL, as informações de índice de texto completo serão recuperadas para cada tabela indexada de texto completo associada a esse catálogo. Se *fulltext_catalog_name* e *table_name* forem especificados, uma linha será retornada se *table_name* estiver associado a *fulltext_catalog_name*; caso contrário, um erro será gerado.  
  
`[ @table_name = ] 'table_name'`É o nome da tabela de uma ou duas partes para a qual os metadados de texto completo são solicitados. *table_name* é **nvarchar (517)**, com um valor padrão de NULL. Se apenas *table_name* for especificado, somente a linha relevante para *table_name* será retornada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou (1) falha  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|Proprietário da tabela. Esse é o nome do usuário de banco de dados que criou a tabela.|  
|**TABLE_NAME**|**sysname**|Nome da tabela.|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|Índice que impõe a restrição UNIQUE na coluna designada como a coluna de chave exclusiva.|  
|**FULLTEXT_KEY_COLID**|**int**|ID de coluna do índice exclusivo identificado por FULLTEXT_KEY_NAME.|  
|**FULLTEXT_INDEX_ACTIVE**|**int**|Especifica se as colunas marcadas para indexação de texto completo nessa tabela são elegíveis para consultas:<br /><br /> 0 = Inativo<br /><br /> 1 = Ativo|  
|**FULLTEXT_CATALOG_NAME**|**sysname**|Catálogo de texto completo no qual os dados de índice de texto completo residem.|  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução usam como padrão membros da função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna os nomes das tabelas indexadas de texto completo associadas ao catálogo de texto completo `Cat_Desc`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_help_fulltext_tables 'Cat_Desc';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [INDEXproperty &#40;&#41;Transact-SQL](../../t-sql/functions/indexproperty-transact-sql.md)   
 [&#41;OBJECTPROPERTY &#40;Transact-SQL](../../t-sql/functions/objectproperty-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_fulltext_table](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_fulltext_tables_cursor](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
