---
title: semanticsimilaritytable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- semanticsimilaritytable
- semanticsimilaritytable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritytable function
ms.assetid: b49d40ab-7552-438b-ad67-6237dcccb75b
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8b6b4b36580c35aead16780f4ada0f461dd58754
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33232791"
---
# <a name="semanticsimilaritytable-transact-sql"></a>semanticsimilaritytable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma tabela de zero, uma ou mais linhas para documentos cujo conteúdo nas colunas especificadas é semanticamente similar a um documento especificado.  
  
 Essa função de conjunto de linhas pode ser referenciada na cláusula FROM de uma instrução SELECT como um nome de tabela normal.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
SEMANTICSIMILARITYTABLE  
    (  
    table,  
    { column | (column_list) | * },  
    source_key  
    )  
```  
  
##  <a name="Arguments"></a> Argumentos  
 **table**  
 É o nome de uma tabela que tem indexação de texto completo e semântica habilitada.  
  
 Esse nome pode ser um nome de uma a quatro partes, mas um nome de servidor remoto não é permitido.  
  
 **column**  
 Nome da coluna indexada para a qual os resultados devem ser retornados. A coluna deve ter indexação semântica habilitada.  
  
 **column_list**  
 Indica várias colunas, separadas por uma vírgula e incluídas entre parênteses. Todas as colunas devem ter indexação semântica habilitada.  
  
 **\***  
 Indica que todas as colunas que têm indexação semântica habilitada estão incluídas.  
  
 **source_key**  
 Chave exclusiva da linha para solicitar resultados de uma linha específica.  
  
 A chave é implicitamente convertida para o tipo da chave exclusiva de texto completo na tabela de origem sempre que possível. A chave pode ser especificaca como uma constante ou variável, mas não pode ser uma expressão ou o resultado de uma subconsulta escalar.  
  
## <a name="table-returned"></a>Tabela retornada  
 A tabela a seguir descreve as informações sobre documentos semelhantes ou relacionados retornados por esta função de conjunto de linhas.  
  
 Documentos correspondidos serão retornados por coluna se os resultados forem solicitados de mais de uma coluna.  
  
|Column_name|Tipo|Description|  
|------------------|----------|-----------------|  
|**source_column_id**|**Int**|ID da coluna da qual um documento de origem foi usado para localizar documentos semelhantes.<br /><br /> Consulte as funções COL_NAME e COLUMNPROPERTY para obter detalhes sobre como recuperar o nome da coluna do column_id e vice-versa.|  
|**matched_column_id**|**Int**|ID da coluna da qual um documento similar foi localizado.<br /><br /> Consulte as funções COL_NAME e COLUMNPROPERTY para obter detalhes sobre como recuperar o nome da coluna do column_id e vice-versa.|  
|**matched_document_key**|**\***<br /><br /> Essa chave corresponde ao tipo da chave exclusiva na tabela de origem.|Valor da chave exclusiva da extração de texto completo e semântica do documento ou linha que foi localizada como similar ao documento especificado na consulta.|  
|**score**|**REAL**|Um valor relativo da similaridade deste documento em sua relação com todos os outros documentos similares.<br /><br /> O valor é um valor decimal fracionário no intervalo de [0,0, 1,0] onde uma pontuação mais alta representa uma correspondência mais próxima e 1,0 é uma pontuação perfeita.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Para obter mais informações, consulte [localizar documentos semelhantes e relacionados com a pesquisa semântica](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md).  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Não é possível consultar documentos similares em colunas. O **SEMANTICSIMILARITYTABLE** função recupera documentos similares apenas da mesma coluna como coluna de origem, que é identificada pelo **source_key** argumento.  
  
## <a name="metadata"></a>Metadados  
 Para obter informações e o status da extração e população de similaridade semântica, consulte as exibições de gerenciamento dinâmico a seguir:  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Exige permissões SELECT na tabela base na qual os índices de texto completo e semânticos foram criados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recuperar os 10 principais candidatos que são semelhantes a um candidato especificado da tabela HumanResources.JobCandidate no banco de dados de exemplo AdventureWorks2012.  
  
```scr  
SELECT TOP(10) KEY_TBL.matched_document_key AS Candidate_ID  
FROMSEMANTICSIMILARITYTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume,  
    @CandidateID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
