---
title: sys. dm_fts_index_keywords_position_by_document (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: feaf2a222df364a41e51969a2c95a978f2d0a289
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67900951"
---
# <a name="sysdm_fts_index_keywords_position_by_document-transact-sql"></a>sys. dm_fts_index_keywords_position_by_document (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna informações de posição de palavra-chave nos documentos indexados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>Argumentos  
 db_id ('*database_name*')  
 Uma chamada para a função [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md) . Essa função aceita um nome de banco de dados e retorna a ID do banco de dados, que sys. dm_fts_index_keywords_position_by_document usa para localizar o banco de dados especificado.  
  
 object_id ('*table_name*')  
 Uma chamada para a função [object_id ()](../../t-sql/functions/object-id-transact-sql.md) . Essa função aceita um nome de tabela e retorna a ID da tabela que contém o índice de texto completo a ser inspecionado.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Coluna|Tipo de dados|Descrição|  
|------------|---------------|-----------------|  
|palavra-chave|**varbinary(128)**|Cadeia de caracteres binária que representa a palavra-chave.|  
|display_term|**nvarchar(4000)**|O formato legível da palavra-chave. Esse formato é derivado do formato interno, que é armazenado no índice de texto completo.|  
|column_id|**int**|A ID da coluna a partir da qual a palavra-chave atual foi indexada com texto completo.|  
|document_id|**bigint**|A ID do documento ou linha a partir da qual o termo atual foi indexado com texto completo. Essa ID corresponde ao valor da chave de texto completo desse documento ou linha.|  
|position|**int**|A posição da palavra-chave no documento.|  
  
## <a name="remarks"></a>Comentários  
 Use o DMV para identificar a localização de palavras indexadas em documentos indexados. Essa DMV pode ser usada para solucionar problemas quando **Sys. dm_fts_index_keywords_by_document** indica que as palavras estão no índice de texto completo, mas quando você executa uma consulta usando essas palavras, o documento não é retornado.  
  
## <a name="permissions"></a>Permissões  
 Requer permissões SELECT nas colunas abrangidas pelo índice de texto completo e permissões CREATE FULLTEXT CATALOG.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna palavras-chave do índice de texto completo da `Production.Document` tabela do banco de `AdventureWorks` dados de exemplo.  
  
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
  
 Você pode adicionar um predicado no outro columns_id como na consulta de exemplo a seguir, para isolar ainda mais os locais.  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_position_by_document  
(   
    DB_ID('AdventureWorks2012'),  
    OBJECT_ID('AdventureWorks2012.Production.Document')   
)  
WHERE document_id = 7 AND display_term = 'performance';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)   
 [Melhorar o desempenho de índices de texto completo](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [As funções pesquisa de texto completo e pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-functions/full-text-search-and-semantic-search-functions-transact-sql.md)   
 [Exibições e funções de gerenciamento dinâmico de pesquisa de texto completo e de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Os procedimentos armazenados de pesquisa de texto completo e de semântica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [Pesquisar Propriedades do documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
