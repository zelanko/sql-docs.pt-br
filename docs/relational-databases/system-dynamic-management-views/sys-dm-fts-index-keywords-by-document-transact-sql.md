---
title: sys.dm_fts_index_keywords_by_document (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_fts_index_keywords_by_document_TSQL
- dm_fts_index_keywords_by_document_TSQL
- sys.dm_fts_index_keywords_by_document
- dm_fts_index_keywords_by_document
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- sys.dm_fts_index_keywords_by_document dynamic management function
- full-text search [SQL Server], viewing keywords
ms.assetid: 793b978b-c8a1-428c-90c2-a3e49d81b5c9
author: pmasl
ms.author: pelopes
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ed1ebf610eafe5c882b2e19ed70129e0cac432fb
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65944371"
---
# <a name="sysdmftsindexkeywordsbydocument-transact-sql"></a>sys.dm_fts_index_keywords_by_document (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Retorna informações sobre o conteúdo no nível de documento de um índice de texto completo associado à tabela especificada.  
  
 sys.dm_fts_index_keywords_by_document é uma função de gerenciamento dinâmico.  
  
 **Para exibir informações de nível mais altos índice de texto completo**  
  
-   [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
 **Para exibir informações sobre o conteúdo de nível de propriedade relacionados a uma propriedade de documento**  
  
-   [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.dm_fts_index_keywords_by_document  
(   
    DB_ID('database_name'),     OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>Argumentos  
 db_id('*database_name*')  
 Uma chamada para o [db_id ()](../../t-sql/functions/db-id-transact-sql.md) função. Essa função aceita um nome de banco de dados e retorna a ID do banco de dados, que sys.dm_fts_index_keywords_by_document usa para localizar o banco de dados especificado. Se *database_name* for omitido, a ID de banco de dados atual será retornada.  
  
 object_id('*table_name*')  
 Uma chamada para o [object_id ()](../../t-sql/functions/object-id-transact-sql.md) função. Essa função aceita um nome de tabela e retorna a ID da tabela que contém o índice de texto completo a ser inspecionado.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|coluna|Data type|Descrição|  
|------------|---------------|-----------------|  
|palavra-chave|**nvarchar(4000)**|A representação hexadecimal da palavra-chave armazenada no índice de texto completo.<br /><br /> Observação: OxFF representa o caractere especial que indica o final de um arquivo ou conjunto de dados.|  
|display_term|**nvarchar(4000)**|O formato legível da palavra-chave. Esse formato é derivado do formato interno, que é armazenado no índice de texto completo.<br /><br /> Observação: OxFF representa o caractere especial que indica o final de um arquivo ou conjunto de dados.|  
|column_id|**int**|A ID da coluna a partir da qual a palavra-chave atual foi indexada com texto completo.|  
|document_id|**int**|A ID do documento ou linha a partir da qual o termo atual foi indexado com texto completo. Essa ID corresponde ao valor da chave de texto completo desse documento ou linha.|  
|occurrence_count|**int**|Número de ocorrências da palavra-chave atual no documento ou linha que é indicada por **document_id**. Quando '*search_property_name*' for especificado, occurrence_count exibe apenas o número de ocorrências da palavra-chave atual na propriedade de pesquisa especificada dentro do documento ou linha.|  
  
## <a name="remarks"></a>Comentários  
 Entre outras coisas, as informações retornadas por sys.dm_fts_index_keywords_by_document são úteis para localizar:  
  
-   O número total de palavras-chave que um índice de texto completo contém.  
  
-   Se uma palavra-chave faz parte de um determinado documento ou linha.  
  
-   Quantas vezes uma palavra-chave aparece no índice de texto completo inteiro; ou seja:  
  
     ([SUM](../../t-sql/functions/sum-transact-sql.md)(**occurrence_count**) WHERE **keyword**=*keyword_value* )  
  
-   Quantas vezes uma palavra-chave aparece em um determinado documento ou linha.  
  
-   Quantas palavras-chave um determinado documento ou linha contém.  
  
 Além disso, é possível usar as informações fornecidas por sys.dm_fts_index_keywords_by_document para recuperar todas as palavras-chave que pertencem a um determinado documento ou linha.  
  
 Quando a coluna de chave de texto completo é um tipo de dados inteiro, conforme recomendado, o document_id é mapeado diretamente no valor da chave de texto completo da tabela base.  
  
 Por outro lado, quando a coluna de chave de texto completo usa um tipo de dados não inteiro, o document_id não representa a chave de texto completo da tabela base. Nesse caso, para identificar a linha na tabela base que é retornada por dm_fts_index_keywords_by_document, você precisa unir essa exibição com os resultados retornados por [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md). Antes de uni-los, é necessário armazenar a saída do procedimento armazenado em uma tabela temporária. Em seguida, você poderá unir a coluna document_id de dm_fts_index_keywords_by_document à coluna DocId que é retornada por esse procedimento armazenado. Observe que um **timestamp** coluna não pode receber valores em tempo de inserção, porque eles são gerados automaticamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, o **timestamp** coluna deve ser convertida em **varbinary (8)** colunas. O exemplo a seguir mostra estas etapas. Neste exemplo, *table_id* é a ID da tabela *database_name* é o nome do banco de dados, e *table_name* é o nome da sua tabela.  
  
```  
USE database_name;  
GO  
CREATE TABLE #MyTempTable   
   (  
      docid INT PRIMARY KEY ,  
      [key] INT NOT NULL  
   );  
DECLARE @db_id int = db_id(N'database_name');  
DECLARE @table_id int = OBJECT_ID(N'table_name');  
INSERT INTO #MyTempTable EXEC sp_fulltext_keymappings @table_id;  
SELECT * FROM sys.dm_fts_index_keywords_by_document   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>Permissões  
 Requer permissões SELECT nas colunas abrangidas pelo índice de texto completo e permissões CREATE FULLTEXT CATALOG.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-full-text-index-content-at-the-document-level"></a>A. Exibindo o conteúdo do índice de texto completo no nível do documento  
 O exemplo a seguir exibe o conteúdo do índice de texto completo no nível do documento na tabela `HumanResources.JobCandidate` do banco de dados de exemplo `AdventureWorks2012`.  
  
> [!NOTE]  
>  Você pode criar esse índice executando o exemplo fornecido para o `HumanResources.JobCandidate` na tabela [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
```  
SELECT * FROM sys.dm_fts_index_keywords_by_document(db_id('AdventureWorks'),   
object_id('HumanResources.JobCandidate'));  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Pesquisa de texto completo e funções e exibições de gerenciamento dinâmico de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)   
 [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [sys.dm_fts_index_keywords_by_property &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-property-transact-sql.md)   
 [sp_fulltext_keymappings &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [Melhorar o desempenho de índices de texto completo](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)  
  
  
