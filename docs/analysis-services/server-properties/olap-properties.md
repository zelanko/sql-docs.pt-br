---
title: Propriedades OLAP | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- AggregationPerfLog property
- DefaultPageSizeForProp property
- UseSinglePassForDimSecurityAutoExist property
- DeepCompressValue property
- CacheRowsetRows property
- Income property
- AggregationNewAlgo property
- MemoryAdjustFactor property
- DimensionLatencyAccuracy property
- InitialBonus property
- DefaultPageSizeForDataHeader property
- MaxCPUUsage property
- DistinctBuffer property
- PartitionLatencyAccuracy property
- MaxRetries property
- UseDataCacheRegistryMultiplyKey property
- ConvertDeletedToUnknown property
- DatabaseConnectionPoolMax property
- DataFileInitEnabled property
- DefaultPageSizeForHash property
- MaxRolapOrConditions property
- UseDataCacheFreeLastPageMemory property
- OLAP [Analysis Services], properties
- MapHandleAlgorithm property
- IndexBuildEnabled property
- MaxObjectsInParallel property
- IgnoreNullRolapRows property
- DimensionPropertyCacheSize property
- DefaultRefreshInterval property
- CheckDistinctRecordSortOrder property
- BufferMemoryLimit property
- EnableTableGrouping property
- ExpressNonEmptyUseEnabled property
- CopyLinkedDataCacheAndRegistry property
- UseDataSlice property
- MemoryLimitErrorEnabled property
- Enabled property
- EnableRolapOptimization property
- DatabaseConnectionPoolTimeout property
- UseDataCacheRegistryHashTable property
- AggregationsBuildEnabled property
- Tax property
- DatabaseConnectionPoolGeneralTimeout property
- DefaultPageSizeForString property
- DatabaseConnectionPoolConnectTimeout property
- MinimumBalance property
- OptimizeSchema property
- UseCalculationCacheRegistry property
- MaxTableDepth property
- DataSliceInitEnabled property
- PrefetchLowerGranularities property
- UseVBANet property
- BufferRecordLimit property
- DefaultPageSizeForIndexHeader property
- MaximumBalance property
- CalculationCacheRegistryMaxIterations property
- DefaultDrillthroughMaxRows property
- IndexBuildThreshold property
- UseDataCacheRegistry property
- MemoryAdjustConst property
- ApplyIntersect property
- IndexFileInitEnabled property
- CacheRowsetToDisk property
- DataCacheRegistryMaxIterations property
- AllowSEFiltering property
- ForceMultiPass property
- ApplySubtract property
- IndexUseEnabled property
- AggregationsUseEnabled property
- DataPlacementOptimization property
- UseMaterializedIterators property
- CacheRecordLimit property
- ROLAPDimensionProcessingEffort property
- DefaultPageSizeForIndex property
- EnableRolapDimQueryTableGrouping property
- DimensionPropertyKeyCache property
- SleepIntervalSecs property
- DefaultPageSizeForData property
- MapFormatMask property
- CalculationEvaluationPolicy property
- AggregationMemoryLimitMin property
- RecordsReportGranularity property
- MemoryLimit property
- AggregationMemoryLimitMax property
ms.assetid: 06eb0d78-96c0-42ff-b759-f4c794597c8d
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cfeaedcf34ffdafdc54c0ce88ae80ecfc6190f6f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="olap-properties"></a>Propriedades OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor OLAP listadas nas seguintes tabelas. Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** somente modo de servidor multidimensional  
  
## <a name="memory"></a>Memória  
 **DefaultPageSizeForData**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForDataHeader**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForIndex**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForIndexHeader**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForString**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForHash**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultPageSizeForProp**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="lazyprocessing"></a>LazyProcessing  
 **Enabled**  
 Uma propriedade booliana que especifica se o processamento de agregação lento está habilitado.  
  
 **SleepIntervalSecs**  
 Uma propriedade de inteiro de 32 bits assinada que define o intervalo, em segundos, em que o servidor verifica se há tarefas de processamento lento pendentes.  
  
 **MaxCPUUsage**  
 Uma propriedade de número de ponto flutuante de precisão dupla de 64 bits assinada que define o uso máximo da CPU para processamento lento, expresso como uma porcentagem. O servidor monitora o uso médio de CPU com base em instantâneos. É comportamento normal pela CPU para controlar os picos desse limite.  
  
 O valor padrão dessa propriedade é 0,5, indicando que no máximo 50% da CPU será dedicado ao processamento lento.  
  
 **MaxObjectsInParallel**  
 Uma propriedade de inteiro de 32 bits assinada, que especifica o número máximo de partições e que podem ser processadas lentamente em paralelo.  
  
 **MaxRetries**  
 Uma propriedade de inteiro de 32 bits assinada que define o número de novas tentativas no caso do processamento lento falhar antes que ocorra um erro.  
  
## <a name="processplan"></a>ProcessPlan  
 **CacheRowsetRows**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CacheRowsetToDisk**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DistinctBuffer**  
 Uma propriedade de inteiro de 32 bits assinada que define o tamanho de um buffer interno usado para contagens distintas. Aumente esse valor para acelerar o processamento de contagem distinto pelo uso da memória.  
  
 **EnableRolapDimQueryTableGrouping**  
 Uma propriedade booliana que especifica se o agrupamento da tabela está habilitado para dimensões ROLAP. Se True, ao consultar as dimensões ROLAP em tempo de execução, as tabelas de dimensões ROLAP inteiras serão consultadas uma vez, diferentemente das consultas separadas para cada atributo.  
  
 **EnableTableGrouping**  
 Uma propriedade booliana que especifica se o agrupamento da tabela está habilitado. Se True, ao processar as dimensões, as tabelas de dimensões inteiras serão consultadas uma vez, diferentemente das consultas separadas para cada atributo.  
  
 **ForceMultiPass**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxTableDepth**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryAdjustConst**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryAdjustFactor**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MemoryLimit**  
 Uma propriedade de número de ponto flutuante da precisão dupla de 64 bits assinada que define a quantidade máxima de memória para processamento, expressa como uma porcentagem da memória física.  
  
 O valor padrão dessa propriedade é 65, indicando que no máximo 65% da memória física será dedicada ao processamento de cubo e dimensão.  
  
 **MemoryLimitErrorEnabled**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **OptimizeSchema**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="proactivecaching"></a>ProactiveCaching  
 **DefaultRefreshInterval**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DimensionLatencyAccuracy**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **PartitionLatencyAccuracy**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="process"></a>Processar  
 **AggregationMemoryLimitMax**  
 Uma propriedade de número de ponto flutuante da precisão dupla de 64 bits assinada que define a quantidade máxima de memória que pode ser dedicada para processamento de agregação, expressa como uma porcentagem da memória física.  
  
 O valor padrão dessa propriedade é 80, indicando que 80% da memória física poderá ser dedicada ao processamento de agregação.  
  
 **AggregationMemoryLimitMin**  
 Uma propriedade de número de ponto flutuante da precisão dupla de 64 bits assinada que define a quantidade mínima de memória que pode ser dedicada para processamento de agregação, expressa como uma porcentagem da memória física. Um valor maior pode acelerar o processamento da agregação pelo uso da memória.  
  
 O valor padrão dessa propriedade é 10, indicando que no mínimo 10% da memória física será dedicada ao processamento da agregação.  
  
 **AggregationNewAlgo**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **AggregationPerfLog2**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **AggregationsBuildEnabled**  
 Uma propriedade booliana que especifica se a criação da agregação está habilitada. Esse é um mecanismo para avaliar a criação da agregação sem alterar o projeto da agregação.  
  
 **BufferMemoryLimit**  
 Uma propriedade de número de ponto flutuante de precisão dupla de 64 bits assinada que define o limite de memória do buffer de processamento, expresso como uma porcentagem da memória física.  
  
 O valor padrão dessa propriedade é 60, indicando que até 60% da memória física pode ser usada para a memória de buffer.  
  
 **BufferRecordLimit**  
 Uma propriedade de inteiro de 32 bits assinada que define o número de registros que podem ser colocados em buffer durante o processamento.  
  
 O valor padrão para essa propriedade é 1048576 (registros).  
  
 **CacheRecordLimit**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CheckDistinctRecordSortOrder**  
 Uma propriedade booliana que define se a ordem de classificação para os resultados de uma consulta de contagem distinta é significativa ao processar partições. True indica que a ordem de classificação não é significativa e deve ser “verificada” pelo servidor. Ao processar partições com medida de contagem distinta, a consulta é enviada para SQL com a classificação. Defina como false para acelerar o processamento.  
  
 O valor padrão dessa propriedade é True, indicando que a ordem de classificação não é significativa e deve ser verificada.  
  
 **DatabaseConnectionPoolConnectTimeout**  
 Uma propriedade de inteiro de 32 bits assinada que especifica o tempo limite em segundos ao abrir uma nova conexão.  
  
 **DatabaseConnectionPoolGeneralTimeout**  
 Uma propriedade de inteiro de 32 bits assinada que especifica o tempo limite em segundos da conexão do banco de dados para uso com as conexões OLEDB externas.  
  
 **DatabaseConnectionPoolMax**  
 Uma propriedade de inteiro de 32 bits assinada que especifica o número máximo de conexões de banco de dados agrupadas.  
  
 O valor padrão dessa propriedade é 50 (conexões).  
  
 **DatabaseConnectionPoolTimeout**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataFileInitEnabled**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataPlacementOptimization**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataSliceInitEnabled**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DeepCompressValue**  
 Uma propriedade booliana aplicada a medidas com tipo de dados duplo que especifica se os números podem ser compactados, causando perda na precisão numérica. Um valor False indica que não há nenhuma compactação ou perda de precisão.  
  
 O valor padrão para essa propriedade é True, que indica que a compactação está habilitada e a precisão será perdida.  
  
 **DimensionPropertyKeyCache**  
 Uma propriedade booliana que especifica se as chaves da propriedade de dimensão são colocadas em cache. Deve ser definida como True se as chaves não forem exclusivas.  
  
 **IndexBuildEnabled**  
 Uma propriedade booliana que especifica se os índices são criados no processamento. Essa propriedade é para fins de avaliação de desempenho e de informação.  
  
 **IndexBuildThreshold**  
 Uma propriedade de inteiro de 32 bits assinada que especifica o limite de contagem de linhas abaixo do qual os índices não serão criados para partições.  
  
 O valor padrão para essa propriedade é 4096 (linhas).  
  
 **IndexFileInitEnabled**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MapFormatMask**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **RecordsReportGranularity**  
 Uma propriedade de inteiro de 32 bits assinada que especifica com que frequência o servidor registra os eventos de Rastreamento durante o processamento em linhas.  
  
 O valor padrão para essa propriedade é 1000, o que indica que um evento de Rastreamento é registrado uma vez a cada 1000 linhas.  
  
 **ROLAPDimensionProcessingEffort**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="query"></a>Consulta  
 **AggregationsUseEnabled**  
 Uma propriedade booliana que define se as agregações armazenadas são usadas em tempo de execução. Essa propriedade permite que as agregações sejam desabilitadas sem alterar o projeto da agregação ou o reprocessamento, para fins de avaliação de desempenho e de informação.  
  
 O valor padrão para essa propriedade é True, indicando que as agregações estão habilitadas.  
  
 **AllowSEFiltering**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationCacheRegistryMaxIterations**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationEvaluationPolicy**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ConvertDeletedToUnknown**  
 Uma propriedade booliana que especifica se membros excluídos da dimensão são convertidos em um membro Desconhecido.  
  
 **CopyLinkedDataCacheAndRegistry**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCacheRegistryMaxIterations**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DefaultDrillthroughMaxRows**  
 Uma propriedade de inteiro de 32 bits assinada que especifica o número máximo de linhas que retornarão de uma consulta em profundidade.  
  
 O valor padrão para essa propriedade é 10000 (linhas).  
  
 **DimensionPropertyCacheSize**  
 Uma propriedade de inteiro de 32 bits assinada que especifica a quantidade de memória (em bytes) usada para membros de dimensão de cache usados em uma consulta.  
  
 O padrão é 4.000.000 bytes (ou 4 MB) por hierarquia de atributo, por consulta ativa. O valor padrão fornece um tamanho de cache bem balanceado para soluções que têm hierarquias típicas. No entanto, as dimensões com um número muito grande de membros (em milhões) ou de hierarquias profundas serão melhor executadas se você aumentar esse valor.  
  
 Implicações de aumentar o tamanho do cache:  
  
-   O custo da utilização de memória aumenta quando você permite que mais memória seja usada pelo cache de dimensão. O uso real depende da execução da consulta. Nem todas as consultas usarão o máximo permitido.  
  
     Observe que a memória usada por esses caches é considerada não reduzível e será incluída para explicar o **TotalMemoryLimit**.  
  
-   Afeta todos os bancos de dados do servidor. **DimensionPropertyCachesize** é uma propriedade para todo o servidor. Alterar essa propriedade afeta todos os bancos de dados em execução na instância atual.  
  
 Abordagem para calcular os requisitos de cache de dimensão:  
  
1.  Comece aumentando o tamanho bastante para determinar se é vantagem aumentar o tamanho do cache de dimensão. Por exemplo, talvez você queira dobrar o valor padrão como uma etapa inicial.  
  
2.  Se uma melhoria de desempenho é evidente, reduza incrementalmente o valor até que você alcance um equilíbrio entre o bom desempenho e a utilização de memória.  
  
 **ExpressNonEmptyUseEnabled**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **IgnoreNullRolapRows**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **IndexUseEnabled**  
 Uma propriedade booliana que define se os índices são usados em tempo de execução. Essa propriedade é para fins de avaliação de desempenho e de informações.  
  
 **MapHandleAlgorithm**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **MaxRolapOrConditions**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseCalculationCacheRegistry**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataCacheFreeLastPageMemory**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataCacheRegistry**  
 Uma propriedade booliana que especifica se o registro em cache de dados deve ser habilitado, onde os resultados da consulta são armazenados em cache (mesmo se os resultados não forem calculados).  
  
 **UseDataCacheRegistryHashTable**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataCacheRegistryMultiplyKey**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseDataSlice**  
 Uma propriedade booliana, que define se frações de dados de partição devem ser usadas em tempo de execução para a otimização da consulta. Essa propriedade é para fins de avaliação de desempenho e de informação.  
  
 **UseMaterializedIterators**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseSinglePassForDimSecurityAutoExist**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **UseVBANet**  
 Uma propriedade booliana que define se deve ser usada a assembly VBA .net para funções definidas pelo usuário.  
  
 **CalculationPrefetchLocality\ ApplyIntersect**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationPrefetchLocality\ ApplySubtract**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **CalculationPrefetchLocality\ PrefetchLowerGranularities**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\  CachedPageAlloc\ Income**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\  CachedPageAlloc\ InitialBonus**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\  CachedPageAlloc\ MaximumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\  CachedPageAlloc\ MinimumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\  CachedPageAlloc\ Tax**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\ Income**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\ InitialBonus**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\ MaximumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\ MinimumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\CellStore\ Tax**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\ MemoryModel \ Income**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\ MemoryModel \ InitialBonus**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\ MemoryModel \ MaximumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\ MemoryModel \ MinimumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataCache\ MemoryModel\ Tax**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="jobs"></a>Trabalhos  
 **ProcessAggregation\ MemoryModel\ Income**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ MemoryModel\ InitialBonus**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ MemoryModel\ MaximumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ MemoryModel\ MinimumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ MemoryModel\ Tax**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessPartition\ Income**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessPartition \ InitialBonus**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessPartition \ MaximumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessPartition \ MinimumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessPartition \ Tax**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessProperty\ Income**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessProperty\ InitialBonus**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessProperty\ MaximumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessProperty\ MinimumBalance**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ProcessAggregation\ ProcessProperty\ Tax**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do servidor no Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
