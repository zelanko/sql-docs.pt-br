---
title: sp_estimate_data_compression_savings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 37c6a32b7970d8bfb0a44eaf407914c5de27f593
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831084"
---
# <a name="sp_estimate_data_compression_savings-transact-sql"></a>sp_estimate_data_compression_savings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o tamanho atual do objeto solicitado e faz a estimativa do tamanho do objeto para o estado de compactação solicitado. A compactação pode ser avaliada para tabelas inteiras ou partes de tabelas. Isso inclui heaps, índices clusterizados, índices não clusterizados, índices columnstore, exibições indexadas e partições de tabela e índice. Os objetos podem ser compactados usando a compactação de linha, página, columnstore ou arquivo morto columnstore. Se a tabela, o índice ou a partição já estiver compactada, será possível usar esse procedimento para estimar o tamanho da tabela, do índice ou da partição, caso ela seja descompactada.  
  
> [!NOTE]
> A compactação e a **sp_estimate_data_compression_savings** não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Para estimar o tamanho do objeto se ele usar a configuração de compactação solicitada, esse procedimento armazenado faz a amostragem do objeto de origem e carrega esses dados em uma tabela e índice equivalentes criados no tempdb. Em seguida, a tabela ou o índice criado no tempdb é compactado para a configuração solicitada e o aumento estimado da compactação é computado.  
  
 Para alterar o estado de compactação de uma tabela, índice ou partição, use as instruções [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) . Para obter informações gerais sobre a compactação, consulte [compactação de dados](../../relational-databases/data-compression/data-compression.md).  
  
> [!NOTE]  
> Se os dados existentes forem fragmentados, é possível reduzir seu tamanho sem usar compactação recriando o índice. Para índices, o fator de preenchimento será aplicado durante a recriação de um índice. Isso pode aumentar o tamanho do índice.  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_estimate_data_compression_savings   
     [ @schema_name = ] 'schema_name'    
   , [ @object_name = ] 'object_name'   
   , [ @index_id = ] index_id   
   , [ @partition_number = ] partition_number   
   , [ @data_compression = ] 'data_compression'   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @schema_name =] '*schema_name*'  
 É o nome do esquema de banco de dados que contém a tabela ou a exibição indexada. *schema_name* é **sysname**. Se *schema_name* for NULL, o esquema padrão do usuário atual será usado.  
  
 [ @object_name =] '*object_name*'  
 É o nome da tabela ou exibição indexada em que o índice está. *object_name* é **sysname**.  
  
 [ @index_id =] *index_id*  
 É a ID do índice. *index_id* é **int**e pode ser um dos seguintes valores: o número de ID de um índice, NULL ou 0 se *object_id* for um heap. Para retornar informações de todos os índices de uma tabela base ou exibição, especifique NULL. Se você especificar NULL, também deverá especificar NULL para *partition_number*.  
  
 [ @partition_number =] *partition_number*  
 É o número da partição no objeto. *partition_number* é **int**e pode ser um dos seguintes valores: o número da partição de um índice ou heap, nulo ou 1 para um índice não particionado ou heap.  
  
 Para especificar a partição, você também pode especificar a função [$Partition](../../t-sql/functions/partition-transact-sql.md) . Para retornar informações de todas as partições do objeto proprietário, especifique NULL.  
  
 [ @data_compression =] '*DATA_COMPRESSION*'  
 É o tipo de compactação a ser avaliado. *DATA_COMPRESSION* pode ser um dos seguintes valores: nenhum, linha, página, COLUMNSTORE ou COLUMNSTORE_ARCHIVE.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 O conjunto de resultados a seguir é retornado para fornecer o tamanho atual e estimado da tabela, índice ou partição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|object_name|**sysname**|Nome da tabela ou exibição indexada.|  
|schema_name|**sysname**|Esquema da tabela ou exibição indexada.|  
|index_id|**int**|ID de um índice.<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado<br /><br /> >1 = Índice não clusterizado|  
|partition_number|**int**|Número da partição. Retorna 1 para uma tabela ou índice não particionado.|  
|size_with_current_compression_setting (KB)|**bigint**|Tamanho da tabela, índice ou partição solicitada como existe atualmente.|  
|size_with_requested_compression_setting (KB)|**bigint**|Tamanho estimado da tabela, índice ou partição que usa a configuração da compactação solicitada e, se aplicável, o fator de preenchimento existente, supondo que não há nenhuma fragmentação.|  
|sample_size_with_current_compression_setting (KB)|**bigint**|Tamanho do exemplo com a definição de compactação atual. Isso inclui qualquer fragmentação.|  
|sample_size_with_requested_compression_setting (KB)|**bigint**|Tamanho do exemplo criado usando a configuração da compactação solicitada e, se aplicável, o fator de preenchimento existente e nenhuma fragmentação.|  
  
## <a name="remarks"></a>Comentários  
 Use `sp_estimate_data_compression_savings` para estimar a economia que pode ocorrer quando você habilita uma tabela ou partição para a compactação de linha, página, columnstore ou arquivo morto columnstore. Por exemplo, se o tamanho médio da linha puder ser reduzido em 40%, o tamanho do objeto poderá ser potencialmente reduzido em 40%. Um aumento de espaço poderá não ser obtido porque isso depende do fator de preenchimento e do tamanho da linha. Por exemplo, se você tiver uma linha com 8.000 bytes de comprimento e reduzir seu tamanho em 40%, ainda poderá ajustar apenas uma linha em uma página de dados. Não há nenhum aumento.  
  
 Se os resultados da execução de `sp_estimate_data_compression_savings` indicarem que a tabela aumentará, isso significa que muitas linhas da tabela usam quase toda a precisão dos tipos de dados e que a adição da pequena sobrecarga necessária para o formato compactado será maior do que o aumento obtido da compactação. Nessa caso raro, não habilite a compactação.  
  
 Se uma tabela estiver habilitada para compactação, use `sp_estimate_data_compression_savings` para estimar o tamanho médio da linha se a tabela não for compactada.  
  
 Um bloqueio (IS) é adquirido na tabela durante essa operação. Se um bloqueio (IS) não puder ser obtido, o procedimento será bloqueado. A tabela é verificada no nível de isolamento confirmado de leitura.  
  
 Se a configuração da compactação solicitada for igual à configuração da compactação atual, o procedimento armazenado retornará o tamanho estimado sem nenhuma fragmentação de dados e usando o fator de preenchimento existente.  
  
 Se a ID da partição ou índice não existir, nenhum resultado será retornado.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `SELECT` na tabela.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 Antes do SQL Server 2019, esse procedimento não se aplica a índices columnstore e, portanto, não aceitou os parâmetros de compactação de dados COLUMNSTORE e COLUMNSTORE_ARCHIVE.  A partir do SQL Server 2019, os índices columnstore podem ser usados como um objeto de origem para estimativa e como um tipo de compactação solicitado.

 > [!IMPORTANT]
 > Quando os [metadados de tempdb com otimização de memória](../databases/tempdb-database.md#memory-optimized-tempdb-metadata) estão habilitados no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] , não há suporte para a criação de índices columnstore em tabelas temporárias. Devido a essa limitação, não há suporte para sp_estimate_data_compression_savings com os parâmetros COLUMNSTORE e COLUMNSTORE_ARCHIVE de compactação de dados quando os metadados de TempDB com otimização de memória estão habilitados.

## <a name="considerations-for-columnstore-indexes"></a>Considerações para Índices Columnstore
 A partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] , `sp_estimate_compression_savings` o dá suporte à estimativa de compactação de arquivo columnstore e columnstore. Ao contrário da compactação de página e linha, a aplicação da compactação columnstore a um objeto requer a criação de um novo índice columnstore. Por esse motivo, ao usar as opções COLUMNSTORE e COLUMNSTORE_ARCHIVE deste procedimento, o tipo do objeto de origem fornecido ao procedimento determina o tipo de índice COLUMNSTORE usado para a estimativa de tamanho compactado. A tabela a seguir ilustra os objetos de referência usados para estimar a economia de compactação para cada tipo de objeto de origem quando o @data_compression parâmetro é definido como COLUMNSTORE ou COLUMNSTORE_ARCHIVE.

 |Objeto de origem|Objeto de referência|
 |-----------------|---------------|
 |Pilha|Índice columnstore clusterizado|
 |Índice clusterizado|Índice columnstore clusterizado|
 |Índice não clusterizado|Índice columnstore não clusterizado (incluindo as colunas de chave e todas as colunas incluídas do índice não clusterizado fornecido, bem como a coluna de partição da tabela, se houver)|
 |índice columnstore não clusterizado|Índice columnstore não clusterizado (incluindo as mesmas colunas que o índice columnstore não clusterizado fornecido)|
 |Índice columnstore clusterizado|Índice columnstore clusterizado|

> [!NOTE]  
> Ao estimar a compactação de columnstore de um objeto de origem do repositório de linhas (índice clusterizado, índice não clusterizado ou heap), se houver alguma coluna no objeto de origem que tenha um tipo de dados sem suporte em um índice columnstore, sp_estimate_compression_savings falhará com um erro.

 Da mesma forma, quando o `@data_compression` parâmetro é definido como `NONE` , `ROW` , ou `PAGE` e o objeto de origem é um índice columnstore, a tabela a seguir descreve os objetos de referência usados.

 |Objeto de origem|Objeto de referência|
 |-----------------|---------------|
 |Índice columnstore clusterizado|Pilha|
 |índice columnstore não clusterizado|Índice não clusterizado (incluindo as colunas contidas no índice columnstore não clusterizado como colunas de chave, e a coluna de partição da tabela, se houver, como uma coluna incluída)|

> [!NOTE]  
> Ao estimar a compactação do rowgroup (nenhum, linha ou página) de um objeto de origem columnstore, verifique se o índice de origem não contém mais de 32 colunas, pois esse é o limite com suporte em um índice de rowgroup (não clusterizado).
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir faz uma estimativa do tamanho da tabela `Production.WorkOrderRouting` quando compactada por meio da compactação `ROW`.  
  
```sql  
USE AdventureWorks2016;  
GO  
EXEC sp_estimate_data_compression_savings 'Production', 'WorkOrderRouting', NULL, NULL, 'ROW' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys. partitions &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Implementação da compactação Unicode](../../relational-databases/data-compression/unicode-compression-implementation.md)  
  
  
