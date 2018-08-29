---
title: sp_fulltext_keymappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb89beba1349b6548604764d12458d4b4fcd45b1
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43104272"
---
# <a name="spfulltextkeymappings-transact-sql"></a>sp_fulltext_keymappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  Retorna mapeamentos entre identificadores de documento (DocIds) e valores de chaves de texto completo. A coluna Doclid contém valores para um **bigint** inteiro que é mapeado para um determinado valor de chave de texto completo em uma tabela indexada de texto completo. Os valores DocId que satisfazem uma condição de pesquisa são transmitidos do Mecanismo de Texto Completo para o Mecanismo de Banco de Dados, no qual eles são mapeados para valores de chave de texto completo da tabela base que está sendo consultada. A coluna de chave de texto completo é um índice exclusivo exigido em uma coluna da tabela.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_fulltext_keymappings { table_id | table_id, docid | table_id, NULL, key }  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *table_id*  
 É a ID do objeto da tabela indexada de texto completo. Se você especificar um inválido *table_id*, um erro será retornado. Para obter informações sobre como obter a ID de objeto de uma tabela, consulte [OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md).  
  
 *docid*  
 É o identificador de um documento interno (DocId) que corresponde ao valor da chave. Um valor *docid* inválido não retorna nenhum resultado.  
  
 *key*  
 É o valor da chave de texto completo da tabela especificada. Um valor *key* inválido não retorna nenhum resultado. Para obter informações sobre valores de chave de texto completo, consulte [gerenciar índices de texto completo](http://msdn.microsoft.com/library/28ff17dc-172b-4ac4-853f-990b5dc02fd1).  
  
> [!IMPORTANT]  
>  Para obter informações sobre como usar um, dois ou três parâmetros, consulte "Comentários", posteriormente neste tópico.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|DocId|**bigint**|É a coluna do identificador de documento (DocId) interno que corresponde ao valor da chave.|  
|Chave|*|É o valor da chave de texto completo da tabela especificada.<br /><br /> Se nenhuma chave de texto completo existir na tabela de mapeamento, um conjunto de linhas vazio será retornado.|  
  
 <sup>*</sup> O tipo de dados para a chave é o mesmo como o tipo de dados da coluna de chave de texto completo na tabela base.  
  
## <a name="permissions"></a>Permissões  
 Esta função é pública e não requer permissões especiais.  
  
## <a name="remarks"></a>Remarks  
 A tabela a seguir descreve o efeito de usar um, dois ou três parâmetros.  
  
|Esta lista de parâmetros...|Tem este resultado...|  
|--------------------------|----------------------|  
|*table_id*|Quando invocado apenas com o *table_id* parâmetro, sp_fulltext_keymappings retorna todos os valores de chave de texto completo (Key) da tabela base especificada, juntamente com o DocId que corresponde a cada chave. Isso inclui as chaves que estão com exclusão pendente.<br /><br /> Essa função é útil para solucionar vários problemas. É especialmente útil para ver o conteúdo do índice de texto completo quando a chave de texto completo selecionada não é do tipo de dados de números inteiros. Isso envolve a junção de resultados de sp_fulltext_keymappings com os resultados de **DM fts_index_keywords_by_document**. Para obter mais informações, consulte [DM fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md).<br /><br /> Em geral, no entanto, recomendamos que, se possível, você execute sp_fulltext_keymappings com os parâmetros que especificam uma chave de texto completo específica ou DocId. Isso é muito mais eficiente do que retornar um mapa de chaves inteiro, especialmente para uma tabela muito grande para a qual o custo de desempenho de retornar um mapa de chaves inteiro pode ser substancial.|  
|*table_id*, *docid*|Se apenas a *table_id* e *docid* forem especificados, *docid* deve ser não NULL e especificar um DocId válido na tabela especificada. Essa função é útil para isolar a chave de texto completo personalizada a partir da tabela base que corresponde ao DocId de um índice de texto completo específico.|  
|*table_id*, NULL, *chave*|Se três parâmetros estiverem presentes, o segundo parâmetro deve ser NULL, e *chave* deve ser não NULL e especificar um valor de chave de texto completo válido da tabela especificada. Essa função é útil no isolamento do DocId que corresponde a uma chave de texto completo específica da tabela base.|  
  
 Um erro é retornado em qualquer uma das condições a seguir:  
  
-   Você especifica um inválido *table_id*.  
  
-   A tabela não está indexada por texto completo.  
  
-   NULL é encontrado para um parâmetro que pode ser não NULL  
  
## <a name="examples"></a>Exemplos  
  
> [!NOTE]  
>  Os exemplos desta seção usam a `Production.ProductReview` tabela do [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados de exemplo. Você pode criar esse índice executando o exemplo fornecido para o `ProductReview` na tabela [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md).  
  
### <a name="a-obtaining-all-the-key-and-docid-values"></a>A. Obtendo todos os valores de Chave e DocId  
 O exemplo a seguir usa uma [DECLARE](../../t-sql/language-elements/declare-local-variable-transact-sql.md) instrução para criar uma variável local, `@table_id` e atribuir a ID do `ProductReview` tabela como seu valor. O exemplo executa **sp_fulltext_keymappings** especificando `@table_id` para o *table_id* parâmetro.  
  
> [!NOTE]  
>  Usando o **sp_fulltext_keymappings** apenas com o *table_id* parâmetro é adequado para tabelas pequenas.  
  
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
 O exemplo a seguir usa uma instrução DECLARE para criar uma variável local, `@table_id`, e para atribuir a ID da tabela `ProductReview` como seu valor. O exemplo executa **sp_fulltext_keymappings** especificando `@table_id` para o *table_id* parâmetro, NULL para o *docid* parâmetro e 4 para o *chave* parâmetro.  
  
> [!NOTE]  
>  Usando o **sp_fulltext_keymappings** apenas com o *table_id* é adequado para tabelas pequenas.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de pesquisa de texto completo e pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
