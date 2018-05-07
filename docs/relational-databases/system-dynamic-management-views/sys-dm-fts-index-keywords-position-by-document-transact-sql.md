---
title: sys.dm_fts_index_keywords_position_by_document (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document_TSQL
- dm_fts_index_keywords_position_by_document
- sys.dm_fts_index_keywords_position_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords_position_by_document dynamic management view
ms.assetid: 0d70184f-baa2-411b-a32d-a4c5af890edd
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 76d7a58ba785964f240cccb6d68cdff897cd6a77
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmftsindexkeywordspositionbydocument-transact-sql"></a>sys.dm_fts_index_keywords_position_by_document (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna informações de posição de palavra-chave em documentos indexados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>Argumentos  
 db_id('*database_name*')  
 Uma chamada para o [db_id](../../t-sql/functions/db-id-transact-sql.md) função. Essa função aceita um nome de banco de dados e retorna a ID de banco de dados, que sys.DM fts_index_keywords_position_by_document usa para localizar o banco de dados especificado.  
  
 object_id ('*table_name*')  
 Uma chamada para o [object_id ()](../../t-sql/functions/object-id-transact-sql.md) função. Essa função aceita um nome de tabela e retorna a ID da tabela que contém o índice de texto completo a ser inspecionado.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Coluna|Data type|Description|  
|------------|---------------|-----------------|  
|palavra-chave|**varbinary(128)**|Cadeia de caracteres binária que representa a palavra-chave.|  
|display_term|**nvarchar(4000)**|O formato legível da palavra-chave. Esse formato é derivado do formato interno, que é armazenado no índice de texto completo.|  
|column_id|**Int**|A ID da coluna a partir da qual a palavra-chave atual foi indexada com texto completo.|  
|document_id|**bigint**|A ID do documento ou linha a partir da qual o termo atual foi indexado com texto completo. Essa ID corresponde ao valor da chave de texto completo desse documento ou linha.|  
|position|**Int**|A posição da palavra-chave no documento.|  
  
## <a name="remarks"></a>Remarks  
 Use a DMV para identificar o local das palavras indexadas em documentos indexados. Essa DMV pode ser usada para solucionar problemas ao **sys.DM fts_index_keywords_by_document** indica as palavras são no índice de texto completo, mas quando você executa uma consulta usando as palavras, o documento não é retornado.  
  
## <a name="permissions"></a>Permissões  
 Requer permissões SELECT nas colunas abrangidas pelo índice de texto completo e permissões CREATE FULLTEXT CATALOG.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna as palavras-chave do índice de texto completo a `Production.Document` analítico o `AdventureWorks` banco de dados de exemplo.  
  
```  
USE AdventureWorks2012;  
GO   
  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
);   
GO  
```  
  
 Você pode adicionar um predicado em de outras columns_id como a seguinte consulta de exemplo, para isolar ainda mais os locais.  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
)  
WHERE document_id = 7 AND display_term = 'performance';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Pesquisa de texto completo](../../relational-databases/search/full-text-search.md)   
 [Melhorar o desempenho de índices de texto completo](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [Pesquisa de texto completo e funções de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-functions/full-text-search-and-semantic-search-functions-transact-sql.md)   
 [Pesquisa de texto completo e funções e exibições de gerenciamento dinâmico de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Procedimentos armazenados de pesquisa de texto completo e pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
