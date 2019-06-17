---
title: sp_help_fulltext_columns_cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_columns_cursor
- sp_help_fulltext_columns_cursor_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_columns_cursor
ms.assetid: 26054e76-53b7-4004-8d48-92ba3435e9d7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6d158c0703190e78209c9a9550040f9bc667b371
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65983052"
---
# <a name="sphelpfulltextcolumnscursor-transact-sql"></a>sp_help_fulltext_columns_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Usa um cursor para retornar as colunas designadas para indexação de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use o [fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) exibição do catálogo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_fulltext_columns_cursor [ @cursor_return = ] @cursor_variable OUTPUT   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @cursor_return = ] @cursor_variable OUTPUT` É a variável de saída do tipo **cursor**. O cursor resultante é rolável, dinâmico, somente leitura.  
  
`[ @table_name = ] 'table_name'` É o nome da tabela de uma ou duas partes para o qual as informações de índice de texto completo são solicitadas. *table_name* está **nvarchar(517)** , com um valor padrão de NULL. Se *table_name* for omitido, as informações de coluna de índice de texto completo são recuperadas para cada tabela indexada de texto completo.  
  
`[ @column_name = ] 'column_name'` É o nome da coluna para o qual os metadados do índice de texto completo é desejado. *column_name* está **sysname** com um valor padrão de NULL. Se *column_name* for omitido ou for NULL, as informações de coluna de texto completo serão retornadas para cada coluna indexada de texto completo de *table_name*. Se *table_name* também for omitido ou for NULL, as informações de coluna de índice de texto completo serão retornadas para cada coluna indexada de texto completo de todas as tabelas no banco de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou (1) falha  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|Proprietário da tabela. Esse é o nome do usuário de banco de dados que criou a tabela.|  
|**TABLE_ID**|**int**|Identificação da tabela.|  
|**TABLE_NAME**|**sysname**|Nome da tabela.|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|A coluna em uma tabela indexada de texto completo que é designada para indexação.|  
|**FULLTEXT_COLID**|**int**|ID da indexada de texto completo.|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|Coluna em uma tabela indexada de texto completo que especifica seu tipo de documento. Esse valor só é aplicável quando a coluna indexada de texto completo é um **varbinary (max)** ou **imagem** coluna.|  
|**FULLTEXT_BLOBTP_COLID**|**int**|ID da coluna de tipo de documento. Esse valor só é aplicável quando a coluna indexada de texto completo é um **varbinary (max)** ou **imagem** coluna.|  
|**FULLTEXT_LANGUAGE**|**sysname**|Idioma usado para a pesquisa de texto completo da coluna.|  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução usam como padrão membros da função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre as colunas que foram designadas para indexação de texto completo em todas as tabelas do banco de dados.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_columns_cursor @mycursor OUTPUT  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END;  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>Consulte também  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
