---
description: semantickeyphrasetable (Transact-SQL)
title: semantickeyphrasetable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- semantickeyphrasetable
- semantickeyphrasetable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- semantickeyphrasetable function
ms.assetid: d33b973a-2724-4d4b-aaf7-67675929c392
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8026760d93132e3a18b51145bc1802e416bc0934
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464778"
---
# <a name="semantickeyphrasetable-transact-sql"></a>semantickeyphrasetable (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma tabela com zero, uma ou mais linhas para essas frases-chave associadas às colunas especificadas da tabela especificada.  
  
 Essa função de conjunto de linhas pode ser referenciada na cláusula FROM de uma instrução SELECT como se fosse um nome de tabela comum.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
SEMANTICKEYPHRASETABLE  
    (  
    table,  
    { column | (column_list) | * }  
     [ , source_key ]  
    )  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> Argumentos  
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
  
 A chave é convertida implicitamente no tipo da chave exclusiva de texto completo na tabela de origem sempre que possível. A chave pode ser especificaca como uma constante ou variável, mas não pode ser uma expressão ou o resultado de uma subconsulta escalar. Se a source-key for omitida, os resultados serão retornados para todas as linhas.  
  
## <a name="table-returned"></a>Tabela retornada  
 A tabela a seguir descreve as informações sobre as frases-chave que podem ser retornadas por essa função de conjunto de linhas.  
  
|Column_name|Type|Descrição|  
|------------------|----------|-----------------|  
|**column_id**|**int**|ID da coluna da qual a frase de chave atual foi extraída e indexada.<br /><br /> Consulte as funções COL_NAME e COLUMNPROPERTY para obter detalhes sobre como recuperar o nome da coluna do column_id e vice-versa.|  
|**document_key**|**\***<br /><br /> Essa chave corresponde ao tipo da chave exclusiva na tabela de origem.|O valor da chave exclusiva do documento ou linha a partir da qual a frase-chave atual foi indexada.|  
|**keyphrase**|**NVARCHAR**|A frase-chave localizada na coluna identificada por column_id e associada ao documento especificado por document_key.|  
|**placar**|**FOTO**|Um valor relativo para essa frase-chave em sua relação com todas as outras frases-chave no mesmo documento na coluna indexada.<br /><br /> O valor é um valor decimal fracionário no intervalo de [0,0, 1,0] onde uma pontuação mais alta representa peso mais alto e 1,0 é a pontuação perfeita.|  
  
## <a name="general-remarks"></a>Comentários gerais  
 Para obter mais informações, consulte [Localizar frases-chave em documentos com pesquisa semântica](../../relational-databases/search/find-key-phrases-in-documents-with-semantic-search.md).  
  
## <a name="metadata"></a>Metadados  
 Para obter informações e o status da extração e população da palavra-chave semântica, consulte as seguintes exibições de gerenciamento dinâmico:  
  
-   [sys.dm_db_fts_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-fts-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Exige permissões SELECT na tabela base na qual os índices de texto completo e semânticos foram criados.  
  
## <a name="examples"></a>Exemplos  
  
###  <a name="example-1-find-the-top-key-phrases-in-a-specific-document"></a><a name="HowToTopPhrases"></a> Exemplo 1: localizar as principais frases-chave em um documento específico  
 O exemplo a seguir recupera as 10 principais frases-chave do documento especificado pela variável @DocumentId na coluna Document da tabela Production.Document do banco de dados de exemplo AdventureWorks. A variável @DocumentId representa um valor da coluna de chave do índice de texto completo. A função **SEMANTICKEYPHRASETABLE** recupera esses resultados com eficácia usando uma busca de índice em vez de um exame de tabela. Este exemplo assume que a coluna está configurada para indexação de texto completo e semântica.  
  
```sql  
SELECT TOP(10) KEYP_TBL.keyphrase  
FROM SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document,  
    @DocumentId  
    ) AS KEYP_TBL  
ORDER BY KEYP_TBL.score DESC;  
  
```  
  
###  <a name="example-2-find-the-top-documents-that-contain-a-specific-key-phrase"></a><a name="HowToTopDocuments"></a> Exemplo 2: localizar os principais documentos que contêm uma frase-chave específica  
 O exemplo a seguir recupera os 25 principais documentos que contêm a frase-chave "Bracket" da coluna Document da tabela Production.Document do banco de dados de exemplo AdventureWorks. Este exemplo assume que a coluna está configurada para indexação de texto completo e semântica.  
  
```sql  
SELECT TOP (25) DOC_TBL.DocumentID, DOC_TBL.DocumentSummary  
FROM Production.Document AS DOC_TBL  
    INNER JOIN SEMANTICKEYPHRASETABLE  
    (  
    Production.Document,  
    Document  
    ) AS KEYP_TBL  
ON DOC_TBL.DocumentID = KEYP_TBL.document_key  
WHERE KEYP_TBL.keyphrase = 'Bracket'  
ORDER BY KEYP_TBL.Score DESC;  
  
```  
  
  
