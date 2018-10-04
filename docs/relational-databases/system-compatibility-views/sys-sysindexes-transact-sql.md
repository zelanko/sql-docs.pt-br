---
title: sys. sysindexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysindexes
- sysindexes_TSQL
- sys.sysindexes
- sys.sysindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysindexes system table
- sys.sysindexes compatibility view
ms.assetid: f483d89c-35c4-4a08-8f8b-737fd80d13f5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0c33336f1e58dadb8781072afc1d4f694a402e01
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709164"
---
# <a name="syssysindexes-transact-sql"></a>sys.sysindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada índice e tabela no banco de dados atual. Não há suporte a índices XML nessa exibição. Tabelas e índices particionados não têm suporte total no modo de exibição; Use o [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) exibição do catálogo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|ID da tabela à qual o índice pertence.|  
|**status**|**int**|Informações de status do sistema.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**first**|**binary(6)**|Ponteiro para a primeira página, ou página-raiz.<br /><br /> Não utilizado quando **indid** = 0.<br /><br /> NULL = o índice é particionado quando **indid** > 1.<br /><br /> NULL = a tabela é particionada quando **indid** for 0 ou 1.|  
|**indid**|**smallint**|ID do índice:<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado<br /><br /> >1 = Índice não clusterizado|  
|**root**|**binary(6)**|Para **indid** > = 1, **raiz** é o ponteiro para a página de raiz.<br /><br /> Não utilizado quando **indid** = 0.<br /><br /> NULL = o índice é particionado quando **indid** > 1.<br /><br /> NULL = a tabela é particionada quando **indid** for 0 ou 1.|  
|**minlen**|**smallint**|Tamanho mínimo de uma linha.|  
|**keycnt**|**smallint**|Número de chaves.|  
|**groupid**|**smallint**|ID do grupo de arquivos em que o objeto foi criado.<br /><br /> NULL = o índice é particionado quando **indid** > 1.<br /><br /> NULL = a tabela é particionada quando **indid** for 0 ou 1.|  
|**dpages**|**int**|Para **indid** = 0 ou **indid** = 1, **dpages** é a contagem de páginas de dados usado.<br /><br /> Para **indid** > 1, **dpages** é a contagem de páginas de índice usado.<br /><br /> 0 = o índice é particionado quando **indid** > 1.<br /><br /> 0 = a tabela é particionada quando **indid** for 0 ou 1.<br /><br /> Não produzirá resultados precisos se ocorrer estouro de linha.|  
|**reserved**|**int**|Para **indid** = 0 ou **indid** = 1, **reservado** é a contagem de páginas alocadas para todos os índices e dados da tabela.<br /><br /> Para **indid** > 1, **reservado** é a contagem de páginas alocadas para o índice.<br /><br /> 0 = o índice é particionado quando **indid** > 1.<br /><br /> 0 = a tabela é particionada quando **indid** for 0 ou 1.<br /><br /> Não produzirá resultados precisos se ocorrer estouro de linha.|  
|**usado**|**int**|Para **indid** = 0 ou **indid** = 1, **usado** é a contagem do total de páginas usadas para todos os dados de índice e tabela.<br /><br /> Para **indid** > 1, **usado** é a contagem de páginas usadas para o índice.<br /><br /> 0 = o índice é particionado quando **indid** > 1.<br /><br /> 0 = a tabela é particionada quando **indid** for 0 ou 1.<br /><br /> Não produzirá resultados precisos se ocorrer estouro de linha.|  
|**rowcnt**|**bigint**|Contagem de linhas de nível de dados com base em **indid** = 0 e **indid** = 1.<br /><br /> 0 = o índice é particionado quando **indid** > 1.<br /><br /> 0 = a tabela é particionada quando **indid** for 0 ou 1.|  
|**rowmodctr**|**int**|Conta o número total de linhas inseridas, excluídas ou atualizadas desde a última atualização das estatísticas da tabela.<br /><br /> 0 = o índice é particionado quando **indid** > 1.<br /><br /> 0 = a tabela é particionada quando **indid** for 0 ou 1.<br /><br /> Na [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, **rowmodctr** não é totalmente compatível com versões anteriores. Para obter mais informações, consulte Comentários.|  
|**reserved3**|**int**|Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved4**|**int**|Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xmaxlen**|**smallint**|Tamanho máximo de uma linha|  
|**maxirow**|**smallint**|Tamanho máximo de uma linha de índice não folha.<br /><br /> Na [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores, **maxirow** não é totalmente compatível com versões anteriores.|  
|**OrigFillFactor**|**tinyint**|Valor do fator de preenchimento original utilizado quando o índice foi criado. Este valor não é mantido; porém, poderá ser útil se você tiver que recriar um índice e não se lembrar do fator de preenchimento que foi utilizado.|  
|**StatVersion**|**tinyint**|Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved2**|**int**|Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**FirstIAM**|**binary(6)**|NULL = O índice é particionado.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**impid**|**smallint**|Sinalizador de implementação de índice.<br /><br /> Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**lockflags**|**smallint**|Usado para restringir as granularidades de bloqueio consideradas para um índice. Por exemplo, para minimizar o custo de bloqueio, uma tabela de pesquisa que é essencialmente somente leitura pode ser configurada para realizar apenas bloqueios de nível de tabela.|  
|**pgmodctr**|**int**|Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Chaves**|**varbinary(816)**|Lista de IDs das colunas que constituem a chave de índice.<br /><br /> Retorna NULL.<br /><br /> Para exibir as colunas de chave de índice, use [sysindexkeys](../../relational-databases/system-compatibility-views/sys-sysindexkeys-transact-sql.md).|  
|**name**|**sysname**|Nome do índice ou estatística. Retorna NULL quando **indid** = 0. Modifique seu aplicativo de modo a fazê-lo procurar um nome de heap NULL.|  
|**statblob**|**image**|Objeto binário grande (BLOB) de estatísticas.<br /><br /> Retorna NULL.|  
|**MaxLen**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**rows**|**int**|Contagem de linhas de nível de dados com base em **indid** = 0 e **indid** = 1, e o valor é repetido para **indid** > 1.|  
  
## <a name="remarks"></a>Comentários  
 Colunas definidas como reservadas não devem ser usadas.  
  
 As colunas **dpages**, **reservado**, e **usado** não retornará resultados precisos se a tabela ou índice contém dados na unidade de alocação ROW_OVERFLOW. Além disso, as contagens de página para cada índice são rastreadas separadamente e não são agregadas na tabela base. Para exibir as contagens de página, use o [sys. allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) ou [sys. Partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) exibições do catálogo, ou o [DM db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) exibição de gerenciamento dinâmico.  
  
 No SQL Server 2000 e nas versões anteriores, [!INCLUDE[ssDE](../../includes/ssde-md.md)] mantinha contadores de modificações no nível de linha. Tais contadores, agora, são mantidos no nível de coluna. Portanto, o **rowmodctr** coluna é calculada e produz resultados que são semelhantes aos resultados nas versões anteriores, mas não são exatos.  
  
 Se você usar o valor em **rowmodctr** para determinar quando atualizar estatísticas, considere as seguintes soluções:  
  
-   Não fazer nada. O novo **rowmodctr** valor frequentemente o ajudam a determinar quando atualizar estatísticas, como o comportamento é razoavelmente próximo dos resultados das versões anteriores.  
  
-   Usar AUTO_UPDATE_STATISTICS. Para obter mais informações, consulte [estatísticas](../../relational-databases/statistics/statistics.md).  
  
-   Usar um tempo limite para determinar quando atualizar as estatísticas. Por exemplo, toda hora, todo dia ou toda semana.  
  
-   Usar informações de nível de aplicativo para determinar quando atualizar as estatísticas. Por exemplo, sempre que o valor máximo de um **identidade** coluna é alterado por mais de 10.000 ou toda vez que uma inserção em massa operação é executada.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
