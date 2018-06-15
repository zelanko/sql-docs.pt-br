---
title: sp_help_fulltext_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_tables
- sp_help_fulltext_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_tables
ms.assetid: 86e24a5f-a869-43f6-b83e-c52b7b01b5ff
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 855a9a5bde98703909a01b44721c5972c1eefff2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33252190"
---
# <a name="sphelpfulltexttables-transact-sql"></a>sp_help_fulltext_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de tabelas que estão registradas para indexação de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use **fulltext_indexes** exibição do catálogo. Para obter mais informações, consulte [fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_fulltext_tables [ [ @fulltext_catalog_name = ] 'fulltext_catalog_name' ]   
     [ , [ @table_name = ] 'table_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@fulltext_catalog_name=**] **'***fulltext_catalog_name***'**  
 É o nome do catálogo de texto completo. *fulltext_catalog_name* é **sysname**, com um padrão NULL. Se *fulltext_catalog_name* for omitido ou for NULL, todas as tabelas indexadas de texto completo associadas com o banco de dados são retornadas. Se *fulltext_catalog_name* for especificado, mas *table_name* for omitido ou for NULL, as informações de índice de texto completo são recuperadas para cada tabela indexada de texto completo associada a este catálogo. Se ambos os *fulltext_catalog_name* e *table_name* for especificado, uma linha é retornada se *table_name* associado *fulltext_catalog_name*; Caso contrário, ocorrerá um erro.  
  
 [  **@table_name=**] **'***table_name***'**  
 É o nome de uma ou duas partes da tabela para a qual são solicitados metadados de texto completo. *table_name* é **nvarchar (517)**, com um valor padrão de NULL. Se apenas *table_name* for especificado, apenas as linhas relevantes para *table_name* é retornado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou (1) falha  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|Proprietário da tabela. Esse é o nome do usuário de banco de dados que criou a tabela.|  
|**TABLE_NAME**|**sysname**|Nome da tabela.|  
|**FULLTEXT_KEY_INDEX_NAME**|**sysname**|Índice que impõe a restrição UNIQUE na coluna designada como a coluna de chave exclusiva.|  
|**FULLTEXT_KEY_COLID**|**Int**|ID de coluna do índice exclusivo identificado por FULLTEXT_KEY_NAME.|  
|**FULLTEXT_INDEX_ACTIVE**|**Int**|Especifica se as colunas marcadas para indexação de texto completo nessa tabela são elegíveis para consultas:<br /><br /> 0 = Inativo<br /><br /> 1 = Ativo|  
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
  
## <a name="see-also"></a>Consulte também  
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_fulltext_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-table-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
