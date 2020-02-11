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
ms.openlocfilehash: 560b5ab5d85c7f2a69fb5062a6eacc6e5c85ee1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68053439"
---
# <a name="syssysindexes-transact-sql"></a>sys.sysindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada índice e tabela no banco de dados atual. Não há suporte a índices XML nessa exibição. Não há suporte total para tabelas e índices particionados nesta exibição; em vez disso, use a exibição de catálogo [Sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) .  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**sessão**|**int**|ID da tabela à qual o índice pertence.|  
|**Estado**|**int**|Informações de status do sistema.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**primeiro**|**binário (6)**|Ponteiro para a primeira página, ou página-raiz.<br /><br /> Não usado quando **indid** = 0.<br /><br /> NULL = o índice é particionado quando **indid** > 1.<br /><br /> NULL = a tabela é particionada quando **indid** é 0 ou 1.|  
|**indid**|**smallint**|ID do índice:<br /><br /> 0 = Heap<br /><br /> 1 = Índice clusterizado<br /><br /> >1 = índice não clusterizado|  
|**básica**|**binário (6)**|Para **indid** >= 1, **root** é o ponteiro para a página raiz.<br /><br /> Não usado quando **indid** = 0.<br /><br /> NULL = o índice é particionado quando **indid** > 1.<br /><br /> NULL = a tabela é particionada quando **indid** é 0 ou 1.|  
|**minlen**|**smallint**|Tamanho mínimo de uma linha.|  
|**keycnt**|**smallint**|Número de chaves.|  
|**GroupId**|**smallint**|ID do grupo de arquivos em que o objeto foi criado.<br /><br /> NULL = o índice é particionado quando **indid** > 1.<br /><br /> NULL = a tabela é particionada quando **indid** é 0 ou 1.|  
|**dpages**|**int**|Para **indid** = 0 ou **indid** = 1, **dpages** é a contagem de páginas de dados usada.<br /><br /> Para **indid** > 1, **dpages** é a contagem de páginas de índice usadas.<br /><br /> 0 = o índice é particionado quando **indid** > 1.<br /><br /> 0 = a tabela é particionada quando **indid** é 0 ou 1.<br /><br /> Não produzirá resultados precisos se ocorrer estouro de linha.|  
|**reservado**|**int**|Para **indid** = 0 ou **indid** = 1, **reservado** é a contagem de páginas alocadas para todos os índices e dados de tabela.<br /><br /> Para **indid** > 1, **reservado** é a contagem de páginas alocadas para o índice.<br /><br /> 0 = o índice é particionado quando **indid** > 1.<br /><br /> 0 = a tabela é particionada quando **indid** é 0 ou 1.<br /><br /> Não produzirá resultados precisos se ocorrer estouro de linha.|  
|**utiliza**|**int**|Para **indid** = 0 ou **indid** = 1, **usado** é a contagem do total de páginas usadas para todos os dados de índice e tabela.<br /><br /> Para **indid** > 1, **usado** é a contagem de páginas usadas para o índice.<br /><br /> 0 = o índice é particionado quando **indid** > 1.<br /><br /> 0 = a tabela é particionada quando **indid** é 0 ou 1.<br /><br /> Não produzirá resultados precisos se ocorrer estouro de linha.|  
|**rowcnt**|**bigint**|Contagem de linhas de nível de dados baseada em **indid** = 0 e **indid** = 1.<br /><br /> 0 = o índice é particionado quando **indid** > 1.<br /><br /> 0 = a tabela é particionada quando **indid** é 0 ou 1.|  
|**rowmodctr**|**int**|Conta o número total de linhas inseridas, excluídas ou atualizadas desde a última atualização das estatísticas da tabela.<br /><br /> 0 = o índice é particionado quando **indid** > 1.<br /><br /> 0 = a tabela é particionada quando **indid** é 0 ou 1.<br /><br /> No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e posterior, o **rowmodctr** não é totalmente compatível com as versões anteriores. Para obter mais informações, consulte Comentários.|  
|**reserved3**|**int**|Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved4**|**int**|Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xmaxlen**|**smallint**|Tamanho máximo de uma linha|  
|**maxirow**|**smallint**|Tamanho máximo de uma linha de índice não folha.<br /><br /> No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e posterior, o **maxirow** não é totalmente compatível com as versões anteriores.|  
|**OrigFillFactor**|**tinyint**|Valor do fator de preenchimento original utilizado quando o índice foi criado. Este valor não é mantido; porém, poderá ser útil se você tiver que recriar um índice e não se lembrar do fator de preenchimento que foi utilizado.|  
|**StatVersion**|**tinyint**|Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved2**|**int**|Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**FirstIAM**|**binário (6)**|NULL = O índice é particionado.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**impid**|**smallint**|Sinalizador de implementação de índice.<br /><br /> Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**lockflags**|**smallint**|Usado para restringir as granularidades de bloqueio consideradas para um índice. Por exemplo, para minimizar o custo de bloqueio, uma tabela de pesquisa que é essencialmente somente leitura pode ser configurada para realizar apenas bloqueios de nível de tabela.|  
|**pgmodctr**|**int**|Retorna 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**novas**|**varbinary (816)**|Lista de IDs das colunas que constituem a chave de índice.<br /><br /> Retorna NULL.<br /><br /> Para exibir as colunas de chave de índice, use [Sys. sysindexkeys](../../relational-databases/system-compatibility-views/sys-sysindexkeys-transact-sql.md).|  
|**name**|**sysname**|Nome do índice ou estatística. Retorna NULL quando **indid** = 0. Modifique seu aplicativo de modo a fazê-lo procurar um nome de heap NULL.|  
|**statblob**|**imagem**|Objeto binário grande (BLOB) de estatísticas.<br /><br /> Retorna NULL.|  
|**maxlen**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**rows**|**int**|Contagem de linhas de nível de dados baseada em **indid** = 0 e **indid** = 1, e o valor é repetido para **indid** >1.|  
  
## <a name="remarks"></a>Comentários  
 Colunas definidas como reservadas não devem ser usadas.  
  
 As colunas **dpages**, **reservadas**e **usadas** não retornarão resultados precisos se a tabela ou o índice contiver dados na unidade de alocação de ROW_OVERFLOW. Além disso, as contagens de página para cada índice são rastreadas separadamente e não são agregadas na tabela base. Para exibir contagens de página, use as exibições de catálogo [Sys. allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) ou [Sys. partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) ou a exibição de gerenciamento dinâmico [Sys. dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) .  
  
 No SQL Server 2000 e nas versões anteriores, [!INCLUDE[ssDE](../../includes/ssde-md.md)] mantinha contadores de modificações no nível de linha. Tais contadores, agora, são mantidos no nível de coluna. Portanto, a coluna **rowmodctr** é calculada e produz resultados semelhantes aos resultados em versões anteriores, mas não são exatos.  
  
 Se você usar o valor em **rowmodctr** para determinar quando atualizar as estatísticas, considere as seguintes soluções:  
  
-   Não faça nada. O novo valor **rowmodctr** frequentemente ajudará a determinar quando atualizar as estatísticas, pois o comportamento é razoavelmente próximo aos resultados de versões anteriores.  
  
-   Usar AUTO_UPDATE_STATISTICS. Para obter mais informações, consulte [estatísticas](../../relational-databases/statistics/statistics.md).  
  
-   Usar um tempo limite para determinar quando atualizar as estatísticas. Por exemplo, toda hora, todo dia ou toda semana.  
  
-   Usar informações de nível de aplicativo para determinar quando atualizar as estatísticas. Por exemplo, toda vez que o valor máximo de uma coluna de **identidade** é alterado por mais de 10.000, ou sempre que uma operação de inserção em massa é executada.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
