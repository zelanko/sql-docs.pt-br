---
title: Como o Repositório de Consultas coleta dados | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, data collection
ms.assetid: 8d5eec36-0013-480a-9c11-183e162e4c8e
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f60ded18e88d57c5a2975b567fa246923ece7ebe
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71974357"
---
# <a name="how-query-store-collects-data"></a>Como o Repositório de Consultas coleta dados
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

O Repositório de Consultas do SQL Server funciona como um gravador de dados de voo, constantemente coletando informações de compilação e runtime relacionadas a consultas e planos. Dados relacionados a consultas são mantidos nas tabelas internas e apresentados aos usuários por meio de um conjunto de exibições.
  
## <a name="views"></a>Exibições 
 O diagrama a seguir mostra os modos de exibição do Repositório de Consultas e suas relações lógicas, com informações de tempo de compilação, apresentadas como entidades azuis:
  
 ![Exibições do processo do Repositório de Consultas](../../relational-databases/performance/media/query-store-process-2views.png "query-store-process-2views")  
**Descrições da exibição**  
  
|Visualizar|Descrição|  
|----------|-----------------|  
|**sys.query_store_query_text**|Apresenta os textos de consulta exclusivos executados no banco de dados. Comentários e espaços antes e depois o texto da consulta são ignorados. Comentários e espaços dentro do texto não são ignorados. Cada instrução no lote gera uma entrada de texto de consulta separada.|  
|**sys.query_context_settings**|Apresenta as combinações exclusivas do plano que afetam as configurações em que as consultas são executadas. O mesmo texto de consulta, executado com configurações diferentes que afetam um plano, produz uma entrada de consulta separada no Repositório de Consultas porque `context_settings_id` faz parte da chave de consulta.|  
|**sys.query_store_query**|Entradas de consulta que são controladas e forçadas separadamente no Repositório de Consultas. Um único texto de consulta poderá gerar várias entradas de consulta se elas forem executadas em configurações de contextos diferentes ou se forem executadas fora versus dentro de diferentes módulos do [!INCLUDE[tsql](../../includes/tsql-md.md)], como procedimentos armazenados e gatilhos.|  
|**sys.query_store_plan**|Apresenta estimativa de plano para a consulta com as estatísticas de tempo de compilação. O plano armazenado é equivalente ao que você obtém usando o `SET SHOWPLAN_XML ON`.|  
|**sys.query_store_runtime_stats_interval**|O Repositório de Consultas divide o tempo em janelas de tempo geradas automaticamente (intervalos) e armazena estatísticas agregadas no intervalo para cada plano executado. O tamanho do intervalo é controlado pela opção de configuração **Intervalo de Coleta de Estatísticas** (em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) ou `INTERVAL_LENGTH_MINUTES` usando [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).|  
|**sys.query_store_runtime_stats**|Estatísticas agregadas de tempo de execução para planos executados. Todas as métricas capturadas são expressas na forma de quatro funções estatísticas: Média, Mínimo, Máximo e Desvio Padrão.|  
  
 Para obter mais informações sobre modos de exibição do Repositório de Consultas, confira a seção "Exibições, funções e procedimentos relacionados" de [Monitorando o desempenho com o repositório de consultas](monitoring-performance-by-using-the-query-store.md). 
  
## <a name="query-processing"></a>Processamento de consulta
 O Repositório de Consultas interage com o pipeline de processamento de consulta nos seguintes pontos-chave:
  
1.  Quando uma consulta é compilada pela primeira vez, o texto de consulta e o plano inicial são enviados ao Repositório de Consultas.
  
2.  Quando uma consulta é recompilada, o plano é atualizado no Repositório de Consultas. Se for criado um novo plano, o Repositório de Consultas adicionará a nova entrada de plano para a consulta, mantendo as anteriores juntos com as respectivas estatísticas de execução.
  
3.  Após a execução da consulta, as estatísticas de runtime são enviadas para o Repositório de Consultas. O Repositório de Consultas mantém estatísticas agregadas precisas para cada plano que foi executado dentro do intervalo ativo no momento. 
  
4.  Durante a compilação e a verificação das fases de recompilação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] determina se há um plano no Repositório de Consultas que deve ser aplicado para a consulta em execução no momento. Se houver um plano forçado e o plano no cache de procedimento for diferente do plano forçado, a consulta será recompilada. Isso seria efetivamente da mesma maneira como se DICA DO PLANO fosse aplicada a essa consulta. Esse processo acontece de forma transparente para o usuário. 
  
 O diagrama a seguir ilustra os pontos de integração explicados nas etapas anteriores:
  
 ![Processo do Repositório de Consultas](../../relational-databases/performance/media/query-store-process-2processor.png "query-store-process-2processor") 

## <a name="remarks"></a>Comentários
 Para minimizar a sobrecarga de E/S, novos dados são capturados na memória. As operações de gravação são enfileiradas e liberadas para o disco posteriormente. As informações de plano e de consulta, mostradas como Repositório de Planos no diagrama a seguir, são liberadas com latência mínima. As estatísticas de runtime, mostradas como Estatísticas de Runtime, são mantidas na memória por um período definido com a opção `DATA_FLUSH_INTERVAL_SECONDS` da instrução `SET QUERY_STORE`. Você pode usar a caixa de diálogo [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] do Repositório de Consultas para inserir um valor para o **Intervalo de Liberação de Dados (Minutos)** , que é convertido internamente em segundos. 
  
 ![Plano do processo do Repositório de Consultas](../../relational-databases/performance/media/query-store-process-3.png "query-store-process-3plan") 
  
 Se o sistema falhar ou ocorrer um desligamento durante o uso do [sinalizador de rastreamento 7745](../../relational-databases/performance/best-practice-with-the-query-store.md#Recovery), o Repositório de Consultas poderá perder os dados de runtime que foram coletados, mas ainda não foram mantidos, até uma janela de tempo definida com `DATA_FLUSH_INTERVAL_SECONDS`. Recomendamos o valor padrão de 900 segundos (15 minutos) como um equilíbrio entre desempenho de captura de consulta e a disponibilidade de dados.
 
 > [!IMPORTANT] 
 > O limite de **Tamanho Máx. (MB)** não é imposto estritamente. O tamanho do armazenamento é verificado somente quando o Repositório de Consultas grava dados no disco. Esse intervalo é definido pelo valor de **Intervalo de Liberação de Dados**. Se Repositório de Consultas tiver violado o limite de tamanho máximo entre as verificações de tamanho de armazenamento, ele fará a transição para o modo somente leitura. Se o **Modo de Limpeza Baseado em Tamanho** estiver habilitado, o mecanismo de limpeza para impor o limite de tamanho máximo também será disparado.
 
 > [!NOTE]
 > Se o sistema estiver enfrentando pressão de memória, as estatísticas de tempo de execução poderão ser liberadas para o disco antes do que foi definido com `DATA_FLUSH_INTERVAL_SECONDS`.
 
 Durante a leitura do Repositório de Consultas, os dados na memória e no disco são unificados de maneira transparente. 
 
 Se uma sessão for encerrada ou o aplicativo cliente for reiniciado ou falhar, as estatísticas de consulta não serão gravadas. 
  
 ![Informações do plano de processo do Repositório de Consultas](../../relational-databases/performance/media/query-store-process-4planinfo.png "query-store-process-4planinfo")    

## <a name="see-also"></a>Confira também
 [Monitorando o desempenho com o Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [Melhor prática com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md)  
 [Exibições de catálogo do repositório de consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md) 
  
  
