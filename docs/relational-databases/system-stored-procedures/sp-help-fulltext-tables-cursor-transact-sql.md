---
title: sp_help_fulltext_tables_cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables_cursor
- sp_help_fulltext_tables_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables_cursor
ms.assetid: 155791eb-8832-4596-8487-7fc70dfba5b9
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e4218f6a105f81997c37202421feb689cd3a074
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68055004"
---
# <a name="sp_help_fulltext_tables_cursor-transact-sql"></a>sp_help_fulltext_tables_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Usa um cursor ao retornar uma lista de tabelas que são registradas para indexação de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use a nova exibição de catálogo **Sys. fulltext_indexes** . Para obter mais informações, consulte [Sys. fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_fulltext_tables_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @cursor_return = ] @cursor_variable OUTPUT`É a variável de saída do tipo **cursor**. O cursor é somente leitura, rolável e dinâmico.  
  
`[ @fulltext_catalog_name = ] 'fulltext_catalog_name'`É o nome do catálogo de texto completo. *fulltext_catalog_name* é **sysname**, com um padrão de NULL. Se *fulltext_catalog_name* for omitido ou for NULL, todas as tabelas indexadas de texto completo associadas ao banco de dados serão retornadas. Se *fulltext_catalog_name* for especificado, mas *table_name* for omitido ou for NULL, as informações de índice de texto completo serão recuperadas para cada tabela indexada de texto completo associada a esse catálogo. Se *fulltext_catalog_name* e *table_name* forem especificados, uma linha será retornada se *table_name* estiver associado a *fulltext_catalog_name*; caso contrário, um erro será gerado.  
  
`[ @table_name = ] 'table_name'`É o nome da tabela de uma ou duas partes para a qual os metadados de texto completo são solicitados. *table_name* é **nvarchar (517)**, com um valor padrão de NULL. Se apenas *table_name* for especificado, somente a linha relevante para *table_name* será retornada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou (1) falha  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
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
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_tables_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END;  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>Consulte Também  
 [INDEXproperty &#40;&#41;Transact-SQL](../../t-sql/functions/indexproperty-transact-sql.md)   
 [&#41;OBJECTPROPERTY &#40;Transact-SQL](../../t-sql/functions/objectproperty-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_fulltext_table](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_fulltext_tables](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
