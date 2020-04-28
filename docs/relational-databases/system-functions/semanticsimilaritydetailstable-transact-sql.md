---
title: semanticsimilaritydetailstable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semanticsimilaritydetailstable
- semanticsimilaritydetailstable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semanticsimilaritydetailstable function
ms.assetid: 038d751a-fca5-4b4c-9129-cba741a4e173
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 34473e6eb173a0aabc5c2067e50aeeec27ce5636
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68067744"
---
# <a name="semanticsimilaritydetailstable-transact-sql"></a>semanticsimilaritydetailstable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna uma tabela de zero, uma ou mais linhas de frases-chave comuns entre dois documentos (um documento de origem e um documento correspondido) cujo conteúdo é semanticamente similar.  
  
 Essa função de conjunto de linhas pode ser referenciada na cláusula FROM de uma instrução SELECT 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
SEMANTICSIMILARITYDETAILSTABLE  
    (  
    table,  
    source_column,  
    source_key,  
    matched_column,  
    matched_key  
    )  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>Argumentos  
 **table**  
 É o nome de uma tabela que tem indexação de texto completo e semântica habilitada.  
  
 Esse nome pode ser um nome de uma a quatro partes, mas um nome de servidor remoto não é permitido.  
  
 **source_column**  
 Nome da coluna na linha de origem que contém o conteúdo a ser comparado para semelhança.  
  
 **source_key**  
 A chave exclusiva que representa a linha do documento original.  
  
 Essa chave é convertida implicitamente no tipo de chave exclusiva de texto completo na tabela de origem sempre que possível. A chave pode ser especificaca como uma constante ou variável, mas não pode ser uma expressão ou o resultado de uma subconsulta escalar. Se uma chave inválida for especificada, nenhuma linha será retornada.  
  
 **matched_column**  
 Nome da coluna na linha correspondente que contém o conteúdo a ser comparado para semelhança.  
  
 **matched_key**  
 A chave exclusiva que representa a linha do documento correspondente.  
  
 Essa chave é convertida implicitamente no tipo de chave exclusiva de texto completo na tabela de origem sempre que possível. A chave pode ser especificaca como uma constante ou variável, mas não pode ser uma expressão ou o resultado de uma subconsulta escalar.  
  
## <a name="table-returned"></a>Tabela retornada  
 A tabela a seguir descreve as informações sobre as frases-chave que podem ser retornadas por essa função de conjunto de linhas.  
  
|Column_name|Type|Descrição|  
|------------------|----------|-----------------|  
|**keyphrase**|**NVARCHAR**|A frase chave que contribui com a semelhança entre o documento original e o documento correspondente.|  
|**placar**|**real**|Um valor relativo para essa frase-chave em sua relação com todas as outras frases-chave que são semelhantes entre os 2 documentos.<br /><br /> O valor é um valor decimal fracionário no intervalo de [0,0, 1,0] onde uma pontuação mais alta representa peso mais alto e 1,0 é a pontuação perfeita.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Para obter mais informações, consulte [localizar documentos semelhantes e relacionados com pesquisa semântica](../../relational-databases/search/find-similar-and-related-documents-with-semantic-search.md).  
  
## <a name="metadata"></a>Metadados  
 Para obter informações e o status da extração e população de similaridade semântica, consulte as exibições de gerenciamento dinâmico a seguir:  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Exige permissões SELECT na tabela base na qual os índices de texto completo e semânticos foram criados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera as 5 frases-chave que tinham a pontuação de similaridade mais alta entre os candidatos especificados na tabela **HumanResources. JobCandidate** do banco de dados de exemplo AdventureWorks2012. As @CandidateId variáveis @MatchedID e representam valores da coluna de chave do índice de texto completo.  
  
```sql  
SELECT TOP(5) KEY_TBL.keyphrase, KEY_TBL.score  
FROMSEMANTICSIMILARITYDETAILSTABLE  
    (  
    HumanResources.JobCandidate,  
    Resume, @CandidateID,  
    Resume, @MatchedID  
    ) AS KEY_TBL  
ORDER BY KEY_TBL.score DESC;  
  
```  
  
  
