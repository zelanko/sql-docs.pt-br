---
title: sys. dm_fts_index_keywords_by_property (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_fts_index_keywords_by_property
- dm_fts_index_keywords_by_property_TSQL
- sys.dm_fts_index_keywords_by_property
- sys.dm_fts_index_keywords_by_property_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], troubleshooting
- search property lists [SQL Server], viewing keywords by property
- full-text search [SQL Server], viewing keywords
- sys.dm_fts_index_keywords_by_property dynamic management view
ms.assetid: fa41e052-a79a-4194-9b1a-2885f7828500
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 82f433d18ff0940c9283f93cfa5e3f87179d31ff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078548"
---
# <a name="sysdm_fts_index_keywords_by_property-transact-sql"></a>sys.dm_fts_index_keywords_by_property (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna todo o conteúdo relacionado a propriedade no índice de texto completo de uma determinada tabela. Isso inclui todos os dados pertencentes a qualquer propriedade registrada pela lista de propriedades de pesquisa associada àquele índice de texto completo.  
  
 sys. dm_fts_index_keywords_by_property é uma função de gerenciamento dinâmico que permite que você veja quais propriedades registradas foram emitidas por IFilters no momento do índice, bem como o conteúdo exato de cada propriedade em cada documento indexado.  
  
 **Para exibir todo o conteúdo no nível de documento (incluindo conteúdo relacionado à propriedade)**  
  
-   [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
 **Para exibir informações de alto nível sobre um índice de texto completo**  
  
-   [sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)  
  
> [!NOTE]  
>  Para obter informações sobre listas de propriedades de pesquisa, consulte [Pesquisar Propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.dm_fts_index_keywords_by_property  
(   
    DB_ID('database_name'),   
OBJECT_ID('table_name')   
)  
```  
  
## <a name="arguments"></a>Argumentos  
 db_id ('*database_name*')  
 Uma chamada para a função [DB_ID ()](../../t-sql/functions/db-id-transact-sql.md) . Essa função aceita um nome de banco de dados e retorna a ID do banco de dados, que sys. dm_fts_index_keywords_by_property usa para localizar o banco de dados especificado. Se *database_name* for omitido, a ID de banco de dados atual será retornada.  
  
 object_id ('*table_name*')  
 Uma chamada para a função [object_id ()](../../t-sql/functions/object-id-transact-sql.md) . Essa função aceita um nome de tabela e retorna a ID da tabela que contém o índice de texto completo a ser inspecionado.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Coluna|Tipo de dados|DESCRIÇÃO|  
|------------|---------------|-----------------|  
|palavra-chave|**nvarchar(4000)**|A representação hexadecimal da palavra-chave armazenada no índice de texto completo.<br /><br /> Observação: OxFF representa o caractere especial que indica o final de um arquivo ou conjunto de um DataSet.|  
|display_term|**nvarchar(4000)**|O formato legível da palavra-chave. Esse formato é derivado do formato interno, que é armazenado no índice de texto completo.<br /><br /> Observação: OxFF representa o caractere especial que indica o final de um arquivo ou conjunto de um DataSet.|  
|column_id|**int**|A ID da coluna a partir da qual a palavra-chave atual foi indexada com texto completo.|  
|document_id|**int**|A ID do documento ou linha a partir da qual o termo atual foi indexado com texto completo. Essa ID corresponde ao valor da chave de texto completo desse documento ou linha.|  
|property_id|**int**|A ID de propriedade interna da propriedade de pesquisa no índice de texto completo da tabela que você especificou no parâmetro OBJECT_ID ('*table_name*').<br /><br /> Quando uma determinada propriedade é adicionada a uma lista de propriedades de pesquisa, o Mecanismo de Texto Completo registra a propriedade e atribui a ela uma ID de propriedade interna que é específica dessa lista de propriedades. A ID de propriedade interna, que é um inteiro, é exclusiva de uma determinada lista de propriedades de pesquisa. Se uma determinada propriedade for registrada para várias listas de propriedades de pesquisa, uma ID de propriedade interna diferente poderá ser atribuída para cada lista de propriedades de pesquisa.<br /><br /> Observação: a ID de propriedade interna é distinta do identificador inteiro de propriedade que é especificado ao adicionar a propriedade à lista de propriedades de pesquisa. Para obter mais informações, veja [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md).<br /><br /> Para exibir a associação entre property_id e o nome da propriedade:<br />                    [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)|  
  
## <a name="remarks"></a>Comentários  
 Essa exibição de gerenciamento dinâmico pode responder a perguntas como estas:  
  
-   Que conteúdo é armazenado em uma determinada propriedade para um determinado DocID?  
  
-   Quão comum é uma determinada propriedade entre os documentos indexados?  
  
-   Quais documentos contêm de fato uma determinada propriedade? Isso será útil se a consulta em uma determinada propriedade de pesquisa não retornar um documento que você esperava encontrar.  
  
 Quando a coluna de chave de texto completo é um tipo de dados inteiro, conforme recomendado, o document_id é mapeado diretamente no valor da chave de texto completo da tabela base.  
  
 Por outro lado, quando a coluna de chave de texto completo usa um tipo de dados não inteiro, o document_id não representa a chave de texto completo da tabela base. Nesse caso, para identificar a linha na tabela base retornada por dm_fts_index_keywords_by_property, você precisa adicionar essa exibição com os resultados retornados por [sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md). Antes de uni-los, é necessário armazenar a saída do procedimento armazenado em uma tabela temporária. Em seguida, você pode unir a coluna document_id de dm_fts_index_keywords_by_property com a coluna DocId retornada por esse procedimento armazenado. Observe que uma coluna **timestamp** não pode receber valores em tempo de inserção, porque eles são gerados automaticamente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]pelo. Portanto, a coluna **timestamp** deve ser convertida em colunas **varbinary (8)** . O exemplo a seguir mostra estas etapas. Neste exemplo, *table_id* é a ID da sua tabela, *database_name* é o nome do seu banco de dados e *table_name* é o nome da sua tabela.  
  
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
SELECT * FROM sys.dm_fts_index_keywords_by_property   
   ( @db_id, @table_id ) kbd  
   INNER JOIN #MyTempTable tt ON tt.[docid]=kbd.document_id;  
GO  
  
```  
  
## <a name="permissions"></a>Permissões  
 Requer permissões SELECT nas colunas abrangidas pelo índice de texto completo e permissões CREATE FULLTEXT CATALOG.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retornar palavras-chave da propriedade `Author` no índice de texto completo da tabela `Production.Document` do banco de dados de amostra `AdventureWorks`. O exemplo usa o alias `KWBPOP` para a tabela retornada por **Sys. dm_fts_index_keywords_by_property**. O exemplo usa junções internas para combinar colunas de [Sys. registered_search_properties](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md) e [Sys. fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md).  
  
```  
-- Once the full-text index is configured to support property searching  
-- on the Author property, return any keywords indexed for this property.  
USE AdventureWorks2012;  
GO   
SELECT KWBPOP.* FROM   
   sys.dm_fts_index_keywords_by_property( DB_ID(),   
   object_id('Production.Document') ) AS KWBPOP  
   INNER JOIN  
      sys.registered_search_properties AS RSP ON(   
         (KWBPOP.property_id = RSP.property_id)   
         AND (RSP.property_name = 'Author') )  
   INNER JOIN  
      sys.fulltext_indexes AS FTI ON(   
         (FTI.[object_id] = object_id('Production.Document'))   
         AND (RSP.property_list_id = FTI.property_list_id) );  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Pesquisa de texto completo](../../relational-databases/search/full-text-search.md)   
 [Melhorar o desempenho de índices de texto completo](../../relational-databases/search/improve-the-performance-of-full-text-indexes.md)   
 [&#41;&#40;Transact-SQL de sp_fulltext_keymappings](../../relational-databases/system-stored-procedures/sp-fulltext-keymappings-transact-sql.md)   
 [sys. dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)   
 [sys. dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)   
 [sys.registered_search_properties &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-properties-transact-sql.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql.md)   
 [Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
  
