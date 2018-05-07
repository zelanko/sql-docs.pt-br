---
title: sp_estimate_data_compression_savings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_estimate_data_compression_savings_TSQL
- sp_estimate_data_compression_savings
dev_langs:
- TSQL
helpviewer_keywords:
- compression [SQL Server], estimating
- sp_estimate_data_compression_savings
ms.assetid: 6f6c7150-e788-45e0-9d08-d6c2f4a33729
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 25798372f2b949446b746164665dbfe6752443d7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spestimatedatacompressionsavings-transact-sql"></a>sp_estimate_data_compression_savings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o tamanho atual do objeto solicitado e faz a estimativa do tamanho do objeto para o estado de compactação solicitado. A compactação pode ser avaliada para tabelas inteiras ou partes de tabelas. Isso inclui heaps, índices clusterizados, índices não clusterizados, exibições indexadas e partições de tabelas e índices. Os objetos podem ser compactados usando a compactação de linha ou de página. Se a tabela, o índice ou a partição já estiver compactada, será possível usar esse procedimento para estimar o tamanho da tabela, do índice ou da partição, caso ela seja descompactada.  
  
> [!NOTE]  
>  Compactação e **sp_estimate_data_compression_savings** não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Para estimar o tamanho do objeto se ele usar a configuração de compactação solicitada, esse procedimento armazenado faz a amostragem do objeto de origem e carrega esses dados em uma tabela e índice equivalentes criados no tempdb. Em seguida, a tabela ou o índice criado no tempdb é compactado para a configuração solicitada e o aumento estimado da compactação é computado.  
  
 Para alterar o estado de compactação de uma tabela, índice ou partição, use o [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) instruções. Para obter informações gerais sobre compactação, consulte [compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
> [!NOTE]  
>  Se os dados existentes forem fragmentados, é possível reduzir seu tamanho sem usar compactação recriando o índice. Para índices, o fator de preenchimento será aplicado durante a recriação de um índice. Isso pode aumentar o tamanho do índice.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_estimate_data_compression_savings   
     [ @schema_name = ] 'schema_name'    
   , [ @object_name = ] 'object_name'   
   , [@index_id = ] index_id   
   , [@partition_number = ] partition_number   
   , [@data_compression = ] 'data_compression'   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @schema_name=] '*schema_name*'  
 É o nome do esquema de banco de dados que contém a tabela ou a exibição indexada. *schema_name* é **sysname**. Se *schema_name* for NULL, será usado o esquema padrão do usuário atual.  
  
 [ @object_name=] '*object_name*'  
 É o nome da tabela ou exibição indexada em que o índice está. *object_name* é **sysname**.  
  
 [ @index_id=] '*index_id*'  
 É a ID do índice. *index_id* é **int**, e pode ser um dos seguintes valores: o número de identificação de um índice, NULL ou 0 se *object_id* for um heap. Para retornar informações de todos os índices de uma tabela base ou exibição, especifique NULL. Se você especificar NULL, você também deverá especificar NULL para *número_da_partição*.  
  
 [ @partition_number=] '*número_da_partição*'  
 É o número da partição no objeto. *número_da_partição* é **int**, e pode ser um dos seguintes valores: o número de partição de um índice ou heap, NULL ou 1 para um heap ou índice não particionado.  
  
 Para especificar a partição, você também pode especificar o [$partition](../../t-sql/functions/partition-transact-sql.md) função. Para retornar informações de todas as partições do objeto proprietário, especifique NULL.  
  
 [ @data_compression=] '*data_compression*'  
 É o tipo de compactação a ser avaliado. *data_compression* pode ser um dos seguintes valores: NONE, linha ou página.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O conjunto de resultados a seguir é retornado para fornecer o tamanho atual e estimado da tabela, índice ou partição.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|object_name|**sysname**|Nome da tabela ou exibição indexada.|  
|schema_name|**sysname**|Esquema da tabela ou exibição indexada.|  
|index_id|**Int**|ID de um índice.<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado<br /><br /> > 1 = Índice não clusterizado|  
|partition_number|**Int**|Número da partição. Retorna 1 para uma tabela ou índice não particionado.|  
|size_with_current_compression_setting (KB)|**bigint**|Tamanho da tabela, índice ou partição solicitada como existe atualmente.|  
|size_with_requested_compression_setting (KB)|**bigint**|Tamanho estimado da tabela, índice ou partição que usa a configuração da compactação solicitada e, se aplicável, o fator de preenchimento existente, supondo que não há nenhuma fragmentação.|  
|sample_size_with_current_compression_setting (KB)|**bigint**|Tamanho do exemplo com a definição de compactação atual. Isso inclui qualquer fragmentação.|  
|sample_size_with_requested_compression_setting (KB)|**bigint**|Tamanho do exemplo criado usando a configuração da compactação solicitada e, se aplicável, o fator de preenchimento existente e nenhuma fragmentação.|  
  
## <a name="remarks"></a>Remarks  
 Use sp_estimate_data_compression_savings para estimar o aumento que pode ocorrer quando uma tabela ou partição é habilitada para compactação de linha ou de página. Por exemplo, se o tamanho médio da linha puder ser reduzido em 40%, o tamanho do objeto poderá ser potencialmente reduzido em 40%. Um aumento de espaço poderá não ser obtido porque isso depende do fator de preenchimento e do tamanho da linha. Por exemplo, se você tiver uma linha de 8000 bytes de comprimento e reduzir seu tamanho em 40%, ainda poderá ajustar apenas uma linha em uma página de dados. Não há nenhum aumento.  
  
 Se os resultados da execução de sp_estimate_data_compression_savings indicarem que a tabela crescerá, isso significará que muitas linhas da tabela usam quase toda a precisão dos tipos de dados e que a adição da pequena sobrecarga necessária para o formato compactado será maior do que o aumento obtido da compactação. Nessa caso raro, não habilite a compactação.  
  
 Se uma tabela estiver habilitada para compactação, use sp_estimate_data_compression_savings para estimar o tamanho médio da linha se a tabela não estiver compactada.  
  
 Um bloqueio (IS) é adquirido na tabela durante essa operação. Se um bloqueio (IS) não puder ser obtido, o procedimento será bloqueado. A tabela é verificada no nível de isolamento confirmado de leitura.  
  
 Se a configuração da compactação solicitada for igual à configuração da compactação atual, o procedimento armazenado retornará o tamanho estimado sem nenhuma fragmentação de dados e usando o fator de preenchimento existente.  
  
 Se a ID da partição ou índice não existir, nenhum resultado será retornado.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT na tabela.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Este procedimento não se aplica às tabelas columnstore e, portanto, não aceita os parâmetros de compactação de dados COLUMNSTORE e COLUMNSTORE_ARCHIVE.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir faz uma estimativa do tamanho da tabela `Production.WorkOrderRouting` quando compactada por meio da compactação `ROW`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimate_data_compression_savings 'Production', 'WorkOrderRouting', NULL, NULL, 'ROW' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Implementação da compactação Unicode](../../relational-databases/data-compression/unicode-compression-implementation.md)  
  
  
