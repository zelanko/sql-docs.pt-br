---
title: sys.dm_fts_index_keywords (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_fts_index_keywords
- sys.dm_fts_index_keywords
- sys.dm_fts_index_keywords_TSQL
- dm_fts_index_keywords_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_index_keywords dynamic management function
- full-text search [SQL Server], viewing keywords
- troubleshooting [SQL Server], full-text search
ms.assetid: fce7b2a1-7e74-4769-86a8-c77c7628decd
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fffcfdc4a7db8fafbe58b0abd914ce611edf3732
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34464342"
---
# <a name="sysdmftsindexkeywords-transact-sql"></a>sys.dm_fts_index_keywords (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre o conteúdo de um índice de texto completo da tabela especificada.  
  
 **sys.DM fts_index_keywords** é uma função de gerenciamento dinâmico.  
  
> [!NOTE]  
>  Para exibir informações de índice de texto completo de nível inferior, use o [sys.DM fts_index_keywords_by_document](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md) a função de gerenciamento dinâmico no nível do documento.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.dm_fts_index_keywords( DB_ID('database_name'), OBJECT_ID('table_name') )  
```  
  
## <a name="arguments"></a>Argumentos  
 db_id('*database_name*')  
 Uma chamada para o [db_id](../../t-sql/functions/db-id-transact-sql.md) função. Essa função aceita um nome de banco de dados e retorna a ID de banco de dados, que **sys.DM fts_index_keywords** usa para localizar o banco de dados especificado. Se *database_name* for omitido, a ID de banco de dados atual será retornada.  
  
 object_id ('*table_name*')  
 Uma chamada para o [object_id ()](../../t-sql/functions/object-id-transact-sql.md) função. Essa função aceita um nome de tabela e retorna a ID da tabela que contém o índice de texto completo a ser inspecionado.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**keyword**|**nvarchar(4000)**|A representação hexadecimal da palavra-chave armazenada dentro do índice de texto completo.<br /><br /> Observação: OxFF representa o caractere especial que indica o final de um arquivo ou conjunto de dados.|  
|**display_term**|**nvarchar(4000)**|O formato legível da palavra-chave. Esse formato é derivado do formato hexadecimal.<br /><br /> Observação: O **display_term** valor de OxFF é "END OF FILE".|  
|**column_id**|**Int**|A ID da coluna a partir da qual a palavra-chave atual foi indexada com texto completo.|  
|**document_count**|**Int**|Número de documentos ou linhas que contém o termo atual.|  
  
## <a name="remarks"></a>Remarks  
 As informações retornadas por **sys.DM fts_index_keywords** é útil para descobrir o seguinte, entre outras coisas:  
  
-   Se uma palavra-chave faz parte do índice de texto completo.  
  
-   Quantos documentos ou linhas contêm uma determinada palavra-chave.  
  
-   A palavra-chave mais comum no índice de texto completo:  
  
    -   **document_count** de cada *keyword_value* em comparação com o total **document_count**, a contagem de documentos de 0xFF.  
  
    -   Normalmente, palavras-chave comuns são apropriadas para declarar como palavras irrelevantes.  
  
> [!NOTE]  
>  O **document_count** retornado por **sys.DM fts_index_keywords** pode ser menos preciso para um documento específico que a contagem retornada por **sys.DM fts_index_keywords_by_document** ou um **contém** consulta. Estima-se que a imprecisão em potencial seja inferior a 1%. Essa imprecisão pode ocorrer porque um **document_id** pode ser contado duas vezes quando ele se prolonga por mais de uma linha no fragmento de índice, ou quando ele aparece mais de uma vez na mesma linha. Para obter uma contagem mais precisa de um documento específico, use **sys.DM fts_index_keywords_by_document** ou um **contém** consulta.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-displaying-high-level-full-text-index-content"></a>A. Exibindo conteúdo de índice de texto completo de alto nível  
 O exemplo a seguir exibe informações sobre o conteúdo de alto nível do índice de texto completo na tabela `HumanResources.JobCandidate`.  
  
```  
SELECT * FROM sys.dm_fts_index_keywords(db_id('AdventureWorks2012'), object_id('HumanResources.JobCandidate'))  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Pesquisa de texto completo e funções e exibições de gerenciamento dinâmico de pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [Pesquisa de texto completo](../../relational-databases/search/full-text-search.md)   
 [sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)  
  
  
