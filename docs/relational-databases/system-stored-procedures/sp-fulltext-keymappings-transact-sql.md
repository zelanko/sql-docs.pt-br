---
title: sp_fulltext_keymappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_keymappings_TSQL
- sp_fulltext_keymappings
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], key column
- sp_fulltext_keymappings
- full-text indexes [SQL Server], troubleshooting
ms.assetid: 2818fa42-072d-4664-a2f7-7ec363b51d81
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ef8bd6cfbcc10fa0625b4925da618ab275331a32
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68124237"
---
# <a name="sp_fulltext_keymappings-transact-sql"></a>sp_fulltext_keymappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Retorna mapeamentos entre identificadores de documento (DocIds) e valores de chaves de texto completo. A coluna DocId contém valores para um inteiro **bigint** que mapeia para um valor de chave de texto completo específico em uma tabela indexada de texto completo. Os valores DocId que satisfazem uma condição de pesquisa são transmitidos do Mecanismo de Texto Completo para o Mecanismo de Banco de Dados, no qual eles são mapeados para valores de chave de texto completo da tabela base que está sendo consultada. A coluna de chave de texto completo é um índice exclusivo exigido em uma coluna da tabela.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_fulltext_keymappings { table_id | table_id, docid | table_id, NULL, key }  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *table_id*  
 É a ID do objeto da tabela indexada de texto completo. Se você especificar um *table_id*inválido, um erro será retornado. Para obter informações sobre como obter a ID de objeto de uma tabela, consulte [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md).  
  
 *identificação*  
 É o identificador de um documento interno (DocId) que corresponde ao valor da chave. Um valor *docid* inválido não retorna nenhum resultado.  
  
 *chave*  
 É o valor da chave de texto completo da tabela especificada. Um valor *key* inválido não retorna nenhum resultado. Para obter informações sobre valores de chave de texto completo, consulte [gerenciar índices de texto completo](https://msdn.microsoft.com/library/28ff17dc-172b-4ac4-853f-990b5dc02fd1).  
  
> [!IMPORTANT]  
>  Para obter informações sobre como usar um, dois ou três parâmetros, consulte "Comentários", posteriormente neste tópico.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|DocId|**bigint**|É a coluna do identificador de documento (DocId) interno que corresponde ao valor da chave.|  
|Chave|*|É o valor da chave de texto completo da tabela especificada.<br /><br /> Se nenhuma chave de texto completo existir na tabela de mapeamento, um conjunto de linhas vazio será retornado.|  
  
 <sup>*</sup>O tipo de dados da chave é o mesmo que o tipo de dados da coluna de chave de texto completo na tabela base.  
  
## <a name="permissions"></a>Permissões  
 Esta função é pública e não requer permissões especiais.  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir descreve o efeito de usar um, dois ou três parâmetros.  
  
|Esta lista de parâmetros...|Tem este resultado...|  
|--------------------------|----------------------|  
|*table_id*|Quando invocado somente com o parâmetro *table_id* , sp_fulltext_keymappings retorna todos os valores de chave de texto completo (chave) da tabela base especificada, juntamente com o docID que corresponde a cada chave. Isso inclui as chaves que estão com exclusão pendente.<br /><br /> Essa função é útil para solucionar vários problemas. É especialmente útil para ver o conteúdo do índice de texto completo quando a chave de texto completo selecionada não é do tipo de dados de números inteiros. Isso envolve a junção dos resultados de sp_fulltext_keymappings com os resultados de **Sys. dm_fts_index_keywords_by_document**. Para obter mais informações, consulte [Sys. dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md).<br /><br /> Em geral, no entanto, recomendamos que, se possível, você execute sp_fulltext_keymappings com os parâmetros que especificam uma chave de texto completo específica ou DocId. Isso é muito mais eficiente do que retornar um mapa de chaves inteiro, especialmente para uma tabela muito grande para a qual o custo de desempenho de retornar um mapa de chaves inteiro pode ser substancial.|  
|*table_id*, *DocId*|Se apenas o *table_id* e o *DocId* forem especificados, *DocId* deverá ser não nulo e especificar um docid válido na tabela especificada. Essa função é útil para isolar a chave de texto completo personalizada a partir da tabela base que corresponde ao DocId de um índice de texto completo específico.|  
|*table_id*, NULL, *chave*|Se houver três parâmetros, o segundo parâmetro deverá ser nulo e a *chave* deverá ser não nula e especificar um valor de chave de texto completo válido a partir da tabela especificada. Essa função é útil no isolamento do DocId que corresponde a uma chave de texto completo específica da tabela base.|  
  
 Um erro é retornado em qualquer uma das condições a seguir:  
  
-   Você especifica um *table_id*inválido.  
  
-   A tabela não está indexada por texto completo.  
  
-   NULL é encontrado para um parâmetro que pode ser não NULL  
  
## <a name="examples"></a>Exemplos  
  
> [!NOTE]  
>  Os exemplo desta seção usam a tabela `Production.ProductReview` do banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] . Você pode criar esse índice executando o exemplo fornecido para a `ProductReview` tabela em [criar índice de texto completo &#40;&#41;Transact-SQL ](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
### <a name="a-obtaining-all-the-key-and-docid-values"></a>A. Obtendo todos os valores de Chave e DocId  
 O exemplo a seguir usa uma instrução [declare](../../t-sql/language-elements/declare-local-variable-transact-sql.md) para criar uma variável local `@table_id` e atribuir a ID da `ProductReview` tabela como seu valor. O exemplo executa **sp_fulltext_keymappings** especificando `@table_id` para o parâmetro *table_id* .  
  
> [!NOTE]  
>  Usar **sp_fulltext_keymappings** apenas com o parâmetro *table_id* é adequado para tabelas pequenas.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id;  
GO  
  
```  
  
 Esse exemplo retorna todas as DocIds e as chaves de texto completo da tabela, da seguinte maneira:  
  
||||  
|-|-|-|  
||`docid`|`key`|  
|`1`|`1`|`1`|  
|`2`|`2`|`2`|  
|`3`|`3`|`3`|  
|`4`|`4`|`4`|  
  
### <a name="b-obtaining-the-docid-value-for-a-specific-key-value"></a>B. Obtendo o valor de DocId para um valor de Chave específico  
 O exemplo a seguir usa uma instrução DECLARE para criar uma variável local, `@table_id`, e para atribuir a ID da tabela `ProductReview` como seu valor. O exemplo executa **sp_fulltext_keymappings** especificando `@table_id` para o parâmetro *table_id* , NULL para o parâmetro *DocId* e 4 para o parâmetro de *chave* .  
  
> [!NOTE]  
>  Usando **sp_fulltext_keymappings** apenas o parâmetro *table_id* é adequado para tabelas pequenas.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @table_id int = OBJECT_ID(N'Production.ProductReview');  
EXEC sp_fulltext_keymappings @table_id, NULL, 4;  
GO  
  
```  
  
 Esse exemplo retorna os seguintes resultados.  
  
||||  
|-|-|-|  
||`docid`|`key`|  
|`4`|`4`|`4`|  
  
## <a name="see-also"></a>Consulte Também  
 [Os procedimentos armazenados de pesquisa de texto completo e de semântica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
