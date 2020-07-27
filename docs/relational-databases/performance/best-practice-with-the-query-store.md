---
title: Melhores práticas com o Repositório de Consultas | Microsoft Docs
description: Conheça as melhores práticas para usar o Repositório de Consultas do SQL Server com sua carga de trabalho, como usar o SQL Server Management Studio e a Análise de Desempenho de Consultas mais recentes.
ms.custom: ''
ms.date: 03/04/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: carlrab
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Query Store, best practices
ms.assetid: 5b13b5ac-1e4c-45e7-bda7-ebebe2784551
author: pmasl
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||= azure-sqldw-latest||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 39c563da1d79492b36cdd13a29ef5ebf4401bed6
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457724"
---
# <a name="best-practices-with-query-store"></a>Melhores prática com o Repositório de Consultas

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

Este artigo descreve as melhores práticas para usar o Repositório de Consultas do SQL Server com sua carga de trabalho.

## <a name="use-the-latest-ssmanstudiofull"></a><a name="SSMS"></a> Use a versão mais recente do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]

O [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] tem um conjunto de interfaces do usuário projetadas para configurar o Repositório de Consultas e para consumir os dados sobre sua carga de trabalho coletados. Baixe a versão mais recente do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] [aqui](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Para ver uma descrição rápida sobre como usar o Repositório de Consultas em cenários de solução de problemas, confira os blogs do [Repositório de Consultas do @Azure](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

## <a name="use-query-performance-insight-in-azure-sql-database"></a><a name="Insight"></a> Usar a Análise de Desempenho de Consultas no banco de dados SQL do Azure

Caso execute o Repositório de Consultas no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], você poderá usar a [Análise de Desempenho de Consultas](https://docs.microsoft.com/azure/sql-database/sql-database-query-performance) para analisar o consumo de recursos ao longo do tempo. Embora você possa usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e o [Azure Data Studio](../../azure-data-studio/what-is.md) para obter o consumo de recursos detalhado de todas as suas consultas, como CPU, memória e E/S, a Análise de Desempenho de Consultas fornece uma maneira rápida e eficiente para determinar seu impacto sobre o consumo de DTU geral do banco de dados. Para obter mais informações, consulte [Análise de Desempenho de Consultas do Banco de Dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-query-performance/).

Esta seção descreve os padrões de configuração ideais que são projetados para garantir a operação confiável do Repositório de Consultas, bem como recursos dependentes. A configuração padrão é otimizada para coleta de dados contínua, ou seja, tempo mínimo gasto nos estados OFF/READ_ONLY. Para obter mais informações sobre todas as opções de Repositório de Consultas disponíveis, confira [Opções do ALTER DATABASE SET (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md#query-store).

| Configuração | Descrição | Padrão | Comentário |
| --- | --- | --- | --- |
| MAX_STORAGE_SIZE_MB |Especifica o limite para o espaço de dados que o Repositório de Consultas ocupará no banco de dados do cliente |100 |Imposto para novos bancos de dados |
| INTERVAL_LENGTH_MINUTES |Define o tamanho da janela de tempo durante o qual as estatísticas de runtime coletadas para planos de consulta são agregadas e persistidas. Cada plano de consulta ativa tem no máximo uma linha por um período de tempo definido com esta configuração |60 |Imposto para novos bancos de dados |
| STALE_QUERY_THRESHOLD_DAYS |Política de limpeza com base em tempo que controla o período de retenção de estatísticas de runtime persistidas e consultas inativas |30 |Imposto para novos bancos de dados e bancos de dados padrão anteriores (367) |
| SIZE_BASED_CLEANUP_MODE |Especifica se a limpeza automática de dados ocorrerá quando o tamanho dos dados do Repositório de Consultas aproximar-se do limite |AUTO |Imposto para todos os bancos de dados |
| QUERY_CAPTURE_MODE |Especifica se todas as consultas ou apenas um subconjunto de consultas será controlado |AUTO |Imposto para todos os bancos de dados |
| FLUSH_INTERVAL_SECONDS |Especifica o período máximo durante o qual as estatísticas de runtime coletadas são mantidas na memória antes de liberar para disco |900 |Imposto para novos bancos de dados |
| | | | |

> [!IMPORTANT]
> Esses padrões serão aplicados automaticamente na fase final de ativação do Repositório de Consultas em todos os [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Depois de habilitado, o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] não alterará os valores de configuração definidos pelos clientes, a menos que eles afetem negativamente a carga de trabalho primária ou as operações confiáveis do Repositório de Consultas.

> [!NOTE]  
> O Repositório de Consultas não pode ser desabilitado no banco de dados individual do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e no Pool Elástico. Executar `ALTER DATABASE [database] SET QUERY_STORE = OFF` retornará o aviso `'QUERY_STORE=OFF' is not supported in this version of SQL Server.`. 

Se você quiser manter suas configurações personalizadas, use [ALTER DATABASE com opções de Repositório de Consultas](../../t-sql/statements/alter-database-transact-sql-set-options.md#query-store) para reverter a configuração ao estado anterior. Confira [Práticas recomendadas com o Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md) para saber como escolher os parâmetros de configuração ideais.

## <a name="use-query-store-with-elastic-pool-databases"></a>Usar o Repositório de Consultas com os bancos de dados de Pool Elástico

Você pode usar o Repositório de Consultas em todos os bancos de dados sem problemas, mesmo em pools densamente compactados. Todos os problemas relacionados ao uso excessivo de recursos, que podem ter ocorrido quando o Repositório de Consultas foi habilitado para o grande número de bancos de dados nos pools elásticos, foram resolvidos.

## <a name="keep-query-store-adjusted-to-your-workload"></a><a name="Configure"></a> Mantenha o Repositório de Consultas ajustado à sua carga de trabalho

Configure o Repositório de Consultas com base na sua carga de trabalho e nos requisitos para solução de problemas de desempenho.
Os parâmetros padrão são bons o bastante para iniciar, mas você deve monitorar o comportamento do Repositório de Consultas ao longo do tempo e ajustar sua configuração adequadamente.

 ![Propriedades do Repositório de Consultas](../../relational-databases/performance/media/query-store-properties.png "query-store-properties")

 Aqui estão as diretrizes a seguir para definir valores de parâmetro:

**Tamanho máximo (MB)** : Especifica o limite do espaço de dados que o Repositório de Consultas consome no banco de dados. Essa é a configuração mais importante, que afeta diretamente o modo de operação do Repositório de Consultas.

Conforme o Repositório de Consultas coleta consultas, planos de execução e estatísticas, seu tamanho no banco de dados cresce até esse limite ser atingido. Quando isso acontece, o Repositório de Consultas automaticamente altera o modo de operação para somente leitura e para de coletar novos dados, o que significa que a análise de desempenho não é mais precisa.

O valor padrão em [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] é de 100 MB. Esse tamanho poderá não ser suficiente se sua carga de trabalho gerar um grande número de consultas e planos diferentes ou se você quiser manter o histórico de consulta por um período de tempo maior. No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e versões posteriores, o valor padrão é de 1 GB. Controle o uso de espaço atual e aumente o valor do **Tamanho Máximo (MB)** para impedir que o Repositório de Consultas passe para o modo somente leitura.

> [!IMPORTANT]
> O limite de **Tamanho Máx. (MB)** não é imposto estritamente. O tamanho do armazenamento é verificado somente quando o Repositório de Consultas grava dados no disco. Esse intervalo é definido pela opção **Intervalo de Liberação de Dados (Minutos)** . Se Repositório de Consultas tiver violado o limite de tamanho máximo entre as verificações de tamanho de armazenamento, ele fará a transição para o modo somente leitura. Se o **Modo de Limpeza Baseado em Tamanho** estiver habilitado, o mecanismo de limpeza para impor o limite de tamanho máximo também será disparado.

Use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou execute o script a seguir para obter as informações mais recentes sobre o tamanho do Repositório de Consultas:

```sql
USE [QueryStoreDB];
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
 max_storage_size_mb, readonly_reason
FROM sys.database_query_store_options;
```

O script a seguir define um novo valor para **Tamanho Máximo (MB)** :

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);
```

 **Intervalo de Limpeza de Dados (Minutos)** : define a frequência de manutenção das estatísticas de runtime coletadas no disco. É expresso em minutos na GUI (interface gráfica do usuário), mas em [!INCLUDE[tsql](../../includes/tsql-md.md)] é expresso em segundos. O padrão é 900 segundos, que são 15 minutos na interface gráfica do usuário. Considere usar um valor mais alto se a carga de trabalho não gerar um grande número de planos e consultas diferentes ou se você puder aguardar mais tempo para manter os dados antes do desligamento de um banco de dados.

> [!NOTE]
> O uso do sinalizador de rastreamento 7745 impede que os dados do Repositório de Consultas sejam gravados em disco em caso de um failover ou comando de desligamento. Para obter mais informações, confira a seção [Usar sinalizadores de rastreamento em servidores críticos](#Recovery).

Use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)] para definir um valor diferente para o **Intervalo de Liberação de Dados**:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (DATA_FLUSH_INTERVAL_SECONDS = 900);
```

**Intervalo de Coleta de Estatísticas**: define o nível de granularidade para a estatística de runtime coletada, expressa em minutos. O padrão é de 60 minutos. Considere usar um valor menor se você precisar de granularidade mais fina ou menos tempo para detectar e atenuar problemas. Lembre-se de que o valor afeta diretamente o tamanho dos dados do Repositório de Consultas. Use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)] para definir um valor diferente para o **Intervalo de Coleta de Estatísticas**:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (INTERVAL_LENGTH_MINUTES = 60);
```

**Limite de Consulta Obsoleta (Dias):** política de limpeza baseada em tempo que controla o período de retenção de estatísticas de runtime persistidas e de consultas inativas, expressa em dias. Por padrão, o Repositório de Consultas está configurado para manter os dados por 30 dias, o que pode ser longo demais para seu cenário.

Evite manter dados históricos que você não planeja usar. Essa prática reduz as alterações ao status somente leitura. O tamanho dos dados do Repositório de Consultas e o tempo para detectar e reduzir o problema serão mais previsíveis. Use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou o script a seguir para configurar a política de limpeza com base em tempo:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 90));
```

**Modo de limpeza com base em tamanho**: especifica se ocorre uma limpeza automática dos dados quando o tamanho dos dados do Repositório de Consultas se aproxima do limite. Ative a limpeza com base no tamanho para que o repositório de consultas seja sempre executado no modo de leitura-gravação e colete sempre os dados mais recentes.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);
```

**Modo de captura do Repositório de Consultas**: especifica a política de captura de consulta do Repositório de Consultas.

- **Tudo**: Captura todas as consultas. Essa é a opção padrão em [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].
- **Auto**: consultas infrequentes e consultas com duração de compilação e execução insignificantes são ignoradas. Os limites para a duração da execução de contagem, da compilação e do runtime são determinados internamente. No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e versões posteriores, essa é a opção padrão.
- **Nenhum**: o Repositório de Consultas para de capturar novas consultas.
- **Personalizado**: permite controle adicional e o ajuste fino da política de coleta de dados. As novas configurações personalizadas definem o que acontece durante o limite de tempo da política de captura interna. Esse é um limite de tempo durante o qual as condições configuráveis são avaliadas e, se alguma for verdadeira, a consulta será qualificada para captura pelo Repositório de Consultas.

> [!IMPORTANT]
> Cursores, consultas dentro de procedimentos armazenados e consultas compiladas nativamente sempre são capturados quando o Modo de Captura do Repositório de Consultas está definido como **Tudo**, **Automático** ou **Personalizado**. Para capturar consultas compiladas nativamente, habilite a coleta de estatísticas por consulta usando [sys.sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).

 O script a seguir define QUERY_CAPTURE_MODE como AUTO:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);
```

### <a name="examples"></a>Exemplos

O exemplo a seguir define QUERY_CAPTURE_MODE como AUTO e define as outras opções recomendadas em [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60
    );
```

O exemplo a seguir define QUERY_CAPTURE_MODE como AUTO e define as outras opções recomendadas em [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] para incluir estatísticas de espera:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      QUERY_CAPTURE_MODE = AUTO,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
    );
```

O exemplo a seguir define QUERY_CAPTURE_MODE como AUTO e define outras opções recomendadas no [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e, *opcionalmente*, define a política de captura CUSTOM com os respectivos padrões, em vez do novo modo de captura AUTO padrão:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE = ON
    (
      OPERATION_MODE = READ_WRITE,
      CLEANUP_POLICY = ( STALE_QUERY_THRESHOLD_DAYS = 90 ),
      DATA_FLUSH_INTERVAL_SECONDS = 900,
      MAX_STORAGE_SIZE_MB = 1000,
      INTERVAL_LENGTH_MINUTES = 60,
      SIZE_BASED_CLEANUP_MODE = AUTO,
      MAX_PLANS_PER_QUERY = 200,
      WAIT_STATS_CAPTURE_MODE = ON,
      QUERY_CAPTURE_MODE = CUSTOM,
      QUERY_CAPTURE_POLICY = (
        STALE_CAPTURE_POLICY_THRESHOLD = 24 HOURS,
        EXECUTION_COUNT = 30,
        TOTAL_COMPILE_CPU_TIME_MS = 1000,
        TOTAL_EXECUTION_CPU_TIME_MS = 100
      )
    );
```

## <a name="start-with-query-performance-troubleshooting"></a>Começar a solução de problemas de desempenho de consulta

O fluxo de trabalho para solucionar problemas com o Repositório de Consultas é simples, como mostra o diagrama a seguir:

![Solução de problemas do Repositório de Consultas](../../relational-databases/performance/media/query-store-troubleshooting.png "query-store-troubleshooting")

Habilite o Repositório de Consultas usando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] conforme descrito na seção anterior ou execute a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir:

```sql
ALTER DATABASE [DatabaseOne] SET QUERY_STORE = ON;
```

Leva algum tempo até o Repositório de Consultas coletar o conjunto de dados que representa com precisão a sua carga de trabalho. Geralmente, um dia é suficiente até mesmo para cargas de trabalho muito complexas. No entanto, você pode começar a explorar os dados e identificar as consultas que exigem atenção imediatamente após a habilitação do recurso. Acesse a subpasta do Repositório de Consultas sob o nó do banco de dados no Pesquisador de Objetos de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para abrir modos de exibição de solução de problemas para cenários específicos.

[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] Os modos de exibição do Repositório de Consultas operam com o conjunto de métricas de execução, cada uma expressa em qualquer uma das seguintes funções de estatística:

|Versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Métrica de execução|Função estatística|
|----------------------|----------------------|------------------------|
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Tempo de CPU, Duração, Contagem de execução, Leituras lógicas, Gravações lógicas, Consumo de memória, Leituras físicas, Tempo de CLR, DOP (grau de paralelismo) e Contagem de linhas|Média, Máximo, Mínimo, Desvio Padrão, Total|
|[!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]|Tempo de CPU, Duração, Contagem de execução, Leituras lógicas, Gravações lógicas, Consumo de memória, Leituras físicas, Tempo de CLR, Grau de paralelismo, Contagem de linhas, Memória de log, Memória TempDB e Tempos de espera|Média, Máximo, Mínimo, Desvio Padrão, Total|

O gráfico a seguir mostra como localizar os modos de exibição do Repositório de Consultas:

![Exibições do Repositório de Consultas](../../relational-databases/performance/media/objectexplorerquerystore_sql17.png "Exibições do Repositório de Consultas")

A tabela a seguir explica quando usar cada um dos modos de exibição do Repositório de Consultas:

|Exibição do SQL Server Management Studio|Cenário|
|---------------|--------------|
|**Consultas Regredidas**|Identifique as consultas para as quais as métricas de execução regrediram recentemente (por exemplo, mudaram para pior). <br />Use esta exibição para correlacionar os problemas de desempenho observados em seu aplicativo com as consultas reais que precisam ser corrigidas ou melhoradas.|
|**Consumo geral de recursos**|Analise o consumo de recursos total do banco de dados para qualquer uma das métricas de execução.<br />Use esta exibição para identificar padrões de recurso (diariamente em vez de cargas de trabalho noturnas) e otimizar o consumo geral do seu banco de dados.|
|**Consultas com o maior consumo de recursos**|Escolha uma métrica de execução de seu interesse e identifique as consultas que tinham os valores mais extremos em um intervalo de tempo fornecido. <br />Use esse modo de exibição para concentrar sua atenção nas consultas mais relevantes, as que apresentam o maior impacto no consumo de recursos do banco de dados.|
|**Consultas com planos forçados**|Listas de planos forçados anteriormente usando o Repositório de Consultas. <br />Use esta exibição para acessar rapidamente todos os planos forçados no momento.|
|**Consultas com alta variação**|Analise consultas com alta variação de execução relacionadas a qualquer dimensão disponível, como Duração, Tempo de CPU, E/S e Uso de memória no intervalo de tempo desejado.<br />Use esta exibição para identificar consultas com desempenho amplamente variável que possam afetar a experiência do usuário em seus aplicativos.|
|**Estatísticas de Espera da Consulta**|Analise as categorias de espera que são mais ativas em um banco de dados e quais consultas mais contribuem para a categoria de espera selecionada.<br />Use esta exibição para analisar as estatísticas de espera e identifique as consultas que podem estar afetando a experiência do usuário em seus aplicativos.<br /><br />Aplica-se a: Começando com [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v18.0 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].|
|**Consultas rastreadas**|Acompanhe a execução das consultas mais importantes em tempo real. Normalmente, você usa este modo de exibição quando você tem consultas com planos forçados e você deseja certificar-se de que o desempenho de consultas é estável.|

> [!TIP]
> Para obter uma descrição detalhada de como usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para identificar as consultas com maior consumo de recursos e corrigir as que regrediram devido à alteração de uma opção de plano, confira os blogs de [Repositório de Consultas do @Azure](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).

Ao identificar uma consulta com desempenho abaixo do ideal, sua ação dependerá da natureza do problema.

- Se a consulta foi executada com vários planos e o último plano é consideravelmente pior que o anterior, é possível usar o mecanismo de imposição de plano para forçá-lo. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tenta forçar o plano no otimizador. Se a imposição do plano falhar, um XEvent será acionado e o otimizador será instruído a otimizar normalmente.

  ![Forçar plano do Repositório de Consultas](../../relational-databases/performance/media/query-store-force-plan.png "query-store-force-plan")

  > [!NOTE]
  > O gráfico anterior pode conter formas diferentes para planos de consulta específicos, com os seguintes significados para cada status possível:<br />
  >
  > |Forma|Significado|
  > |-------------------|-------------|
  > |Circle|Consulta concluída, o que significa que uma execução regular foi concluída com êxito.|
  > |Square|Cancelada, o que significa uma execução anulada iniciada pelo cliente.|
  > |Triangle|Falha, o que significa que uma exceção anulou a execução.|
  >
  > Além disso, o tamanho da forma reflete a contagem de execução da consulta dentro do intervalo de tempo especificado. O tamanho aumenta com um número maior de execuções.

- Você pode concluir falta um índice na consulta para a execução ideal. Essas informações são expostas no plano de execução de consulta. Crie o índice ausente e verifique o desempenho da consulta usando o Repositório de Consultas.

   ![Mostrar plano do Repositório de Consultas](../../relational-databases/performance/media/query-store-show-plan.png "query-store-show-plan")

Se você executar sua carga de trabalho em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], inscreva-se no Index Advisor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] para receber automaticamente as recomendações de índice.

- Em alguns casos, você poderá aplicar a recompilação de estatística se perceber uma diferença significativa entre o número de linhas estimado e o real no plano de execução.
- Reescreva consultas problemáticas, por exemplo, para aproveitar a parametrização de consulta ou para implementar uma lógica melhor.

## <a name="verify-that-query-store-collects-query-data-continuously"></a><a name="Verify"></a> Verifique se Repositório de Consultas coleta dados de consulta continuamente

O Repositório de Consultas pode alterar o modo de operação silenciosamente. Monitore regularmente o estado do Repositório de Consultas para garantir que o repositório de consultas esteja operando e agir para evitar falhas devido a causas previsíveis. Execute a consulta a seguir para determinar o modo de operação e exibir os parâmetros mais relevantes:

```sql
USE [QueryStoreDB];
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
    max_storage_size_mb, readonly_reason, interval_length_minutes,
    stale_query_threshold_days, size_based_cleanup_mode_desc,
    query_capture_mode_desc
FROM sys.database_query_store_options;
```

A diferença entre `actual_state_desc` e `desired_state_desc` indica que uma alteração do modo de operação ocorreu automaticamente. A alteração mais comum é a alternância silenciosa do Repositório de Consultas para o modo somente leitura. Em circunstâncias raras, o Repositório de Consultas pode terminar no estado de ERRO devido a erros internos.

Quando o estado real for somente leitura, use a coluna **readonly_reason** para determinar a causa raiz. Normalmente, você descobre que o Repositório de Consultas realizou a transição para o modo somente leitura porque a cota de tamanho foi excedida. Nesse caso, **readonly_reason** é definido como 65536. Para outras razões, veja [sys.database_query_store_options &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md).

Considere as etapas a seguir para realizar a transição do Repositório de Consultas para o modo de leitura-gravação e ativar a coleta de dados:

- Aumente o tamanho máximo de armazenamento usando a opção **MAX_STORAGE_SIZE_MB** de **ALTER DATABASE**.
- Limpe os dados do Repositório de Consultas usando a instrução a seguir:

  ```sql
  ALTER DATABASE [QueryStoreDB] SET QUERY_STORE CLEAR;
  ```

Você pode aplicar uma destas etapas ou ambas executando a seguinte instrução, que altera explicitamente o modo de operação para leitura-gravação:

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);
```

Execute as etapas a seguir para ser proativo:

- Você pode evitar alterações silenciosas do modo de operação aplicando as práticas recomendadas. O tamanho do Repositório de Consultas deve estar sempre abaixo do valor máximo permitido para reduzir drasticamente a chance de ocorrer transição para o modo somente leitura. Ative a política com base no tamanho conforme descrito na seção [Configurar Repositório de Consultas](#Configure) para que o Repositório de Consultas limpe automaticamente os dados quando o tamanho se aproximar do limite.
- Para assegurar que os dados mais recentes sejam mantidos, configure a política com base em tempo para remover informações obsoletas regularmente.
- Por fim, considere definir o **Modo de Captura do Repositório de Consultas** como **Auto**, pois ele remove as consultas que costumam ser menos relevantes para sua carga de trabalho.

### <a name="error-state"></a>Estado de ERRO

Para recuperar o Repositório de Consultas, tente definir explicitamente o modo de leitura-gravação e verifique o estado real novamente.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
    max_storage_size_mb, readonly_reason, interval_length_minutes,
    stale_query_threshold_days, size_based_cleanup_mode_desc,
    query_capture_mode_desc
FROM sys.database_query_store_options;
```

Se o problema persistir, isso indicará que os dados do Repositório de Consultas mantidos no disco estão corrompidos.

No [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] e versões posteriores, é possível recuperar o Repositório de Consultas executando o procedimento armazenado **sp_query_store_consistency_check** no banco de dados afetado. O Repositório de Consultas deve ser desabilitado antes da tentativa de executar a operação de recuperação. Para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], limpe os dados do Repositório de Consultas conforme mostrado.

Se a recuperação falhar, tente limpar o Repositório de Consultas antes de configurar o modo de leitura/gravação.

```sql
ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE CLEAR;
GO

ALTER DATABASE [QueryStoreDB]
SET QUERY_STORE (OPERATION_MODE = READ_WRITE);
GO

SELECT actual_state_desc, desired_state_desc, current_storage_size_mb,
    max_storage_size_mb, readonly_reason, interval_length_minutes,
    stale_query_threshold_days, size_based_cleanup_mode_desc,
    query_capture_mode_desc
FROM sys.database_query_store_options;
```

## <a name="set-the-optimal-query-store-capture-mode"></a>Definir o Modo de Captura do Repositório de Consultas ideal

Mantenha os dados mais relevantes no Repositório de Consultas. A tabela a seguir descreve os cenários típicos para cada Modo de Captura do Repositório de Consultas:

|Modo de captura do Repositório de Consultas|Cenário|
|------------------------|--------------|
|**Todos**|Analise sua carga de trabalho plenamente quanto a todas as formas das consultas, suas frequências de execução e outras estatísticas.<br /><br /> Identifique novas consultas na carga de trabalho.<br /><br /> Detecte se consultas ad hoc são usadas para identificar oportunidades de parametrização automática ou pelo usuário.<br /><br />Observação: Esse é o modo de captura padrão no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e no [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)].|
|**Auto**|Concentre a atenção em consultas relevantes e acionáveis. Um exemplo são as consultas executadas regularmente ou que consomem muitos recursos.<br /><br />Observação: No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e versões posteriores, esse é o modo de captura padrão.|
|**Nenhuma**|Você já capturou o conjunto de consultas que deseja monitorar no runtime e deseja eliminar as distrações que outras consultas podem causar.<br /><br /> Nenhuma é adequada para ambientes de teste e parâmetros de avaliação.<br /><br /> Nenhuma também é adequado para fornecedores de software que entregam o Repositório de Consultas configurado para monitorar a sua carga de trabalho do aplicativo.<br /><br /> Nenhuma deve ser usada com cuidado, pois você poderá perder a oportunidade de acompanhar e otimizar novas consultas importantes. Evite usar Nenhuma, a menos que tenha um cenário específico que precise desse modo.|
|**Custom**|O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] introduz um modo de captura Personalizado sob o comando `ALTER DATABASE SET QUERY_STORE`. Quando habilitadas, as configurações adicionais do Repositório de Consultas ficam disponíveis em uma nova configuração de política de captura do Repositório de Consultas para ajustar a coleta de dados em um servidor específico.<br /><br />As novas configurações personalizadas definem o que acontece durante o limite de tempo da política de captura interna. Esse é um limite de tempo durante o qual as condições configuráveis são avaliadas e, se alguma for verdadeira, a consulta será qualificada para captura pelo Repositório de Consultas. Para obter mais informações, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).|

> [!NOTE]
> Cursores, consultas dentro de procedimentos armazenados e consultas compiladas nativamente sempre são capturados quando o Modo de Captura do Repositório de Consultas está definido como **Tudo**, **Automático** ou **Personalizado**. Para capturar consultas compiladas nativamente, habilite a coleta de estatísticas por consulta usando [sys.sp_xtp_control_query_exec_stats](../../relational-databases/system-stored-procedures/sys-sp-xtp-control-query-exec-stats-transact-sql.md).

## <a name="keep-the-most-relevant-data-in-query-store"></a>Manter os dados mais relevantes no Repositório de Consultas

Configure o Repositório de Consultas para conter somente os dados relevantes para que ele seja executado continuamente e proporcione uma ótima experiência de solução de problemas com impacto mínimo sobre sua carga de trabalho normal.
A tabela a seguir fornece as práticas recomendadas:

|Melhor prática|Configuração|
|-------------------|-------------|
|Limite dados históricos retidos.|Configure a política com base em tempo para ativar a limpeza automática.|
|Por filtragem, desconsidere consultas não relevantes.|Configure o **Modo de Captura do Repositório de Consultas** como **Auto**.|
|Exclua consultas menos relevantes ao atingir o tamanho máximo.|Ative a política de limpeza com base em tamanho.|

## <a name="avoid-using-non-parameterized-queries"></a><a name="Parameterize"></a> Evite usar consultas não parametrizadas

Não é recomendável usar consultas não parametrizadas quando isso não é necessário. Um exemplo é no caso da análise ad hoc. Planos em cache não podem ser reutilizados, o que força o Otimizador de Consulta a compilar consultas para cada texto da consulta exclusivo. Para saber mais, confira [Diretrizes para uso da parametrização forçada](../../relational-databases/query-processing-architecture-guide.md#ForcedParamGuide).

Além disso, o Repositório de Consultas pode rapidamente exceder a cota de tamanho devido a um número potencialmente grande de textos da consulta diferentes e, assim, um grande número de planos de execução diferentes com forma semelhante. Como resultado, o desempenho da carga de trabalho fica abaixo do ideal e o Repositório de Consultas pode alternar para o modo somente leitura ou excluir dados constantemente na tentativa de acompanhar as consultas que chegam.

Considere as seguintes opções:

- Parametrizar consultas quando aplicável. Por exemplo, encapsule as consultas dentro de um procedimento armazenado ou em sp_executesql. Para saber mais, confira [Reutilização de parâmetros e do plano de execução](../../relational-databases/query-processing-architecture-guide.md#PlanReuse).
- Use a opção [otimizar para cargas de trabalho ad hoc](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) se sua carga de trabalho contiver muitos lotes ad hoc de uso único com planos de consulta diferentes.
  - Compare o número de valores query_hash distintos ao número total de entradas em sys.query_store_query. Se o índice estiver próximo de 1, a carga de trabalho ad hoc gerará consultas diferentes.
- Aplique [parametrização forçada](../../relational-databases/query-processing-architecture-guide.md#ForcedParam) ao banco de dados ou a um subconjunto de consultas se o número de planos de consulta diferentes não for grande.
  - Use um [guia de plano](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md) para forçar a parametrização somente para a consulta selecionada.
  - Configure a parametrização forçada usando o comando [parameterization database option](../../relational-databases/databases/database-properties-options-page.md#miscellaneous) se houver um pequeno número de planos de consulta diferentes em sua carga de trabalho. Um exemplo é quando a taxa entre a contagem de query_hash distintos e o número total de entradas em sys.query_store_query é muito menor que 1.
- Defina QUERY_CAPTURE_MODE como AUTO para filtrar automaticamente, desconsiderando consultas ad hoc com consumo de recursos pequeno.

## <a name="avoid-a-drop-and-create-pattern-for-containing-objects"></a><a name="Drop"></a> Evitar um padrão DROP e CREATE para objetos recipientes

O Repositório de Consultas associa a entrada da consulta a um objeto recipiente, como um procedimento armazenado, função e gatilho. Ao recriar um objeto recipiente, uma nova entrada da consulta é gerada para o mesmo texto da consulta. Isso o impede de acompanhar estatísticas de desempenho para essa consulta ao longo do tempo e de usar o mecanismo de imposição de plano. Para evitar essa situação, use o processo `ALTER <object>` para alterar uma definição de objeto recipiente sempre que possível.

## <a name="check-the-status-of-forced-plans-regularly"></a><a name="CheckForced"></a> Verifique o status de planos forçados regularmente

A imposição de plano é um mecanismo prático para corrigir o desempenho das consultas críticas e torná-las mais previsíveis. Assim como ocorre com as dicas de plano e guias de plano, impor um plano não é uma garantia de que ele será usado em execuções futuras. Normalmente, quando o esquema de banco de dados é alterado de forma que os objetos referenciados pelo plano de execução são alterados ou removidos, a imposição de plano começa a falhar. Nesse caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fará fallback para a recompilação da consultas, enquanto o motivo real da falha da imposição é exposto em [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md). A consulta a seguir retorna informações sobre planos impostos:

```sql
USE [QueryStoreDB];
GO

SELECT p.plan_id, p.query_id, q.object_id as containing_object_id,
    force_failure_count, last_force_failure_reason_desc
FROM sys.query_store_plan AS p
JOIN sys.query_store_query AS q on p.query_id = q.query_id
WHERE is_forced_plan = 1;
```

Para obter uma lista completa dos motivos, confira [sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md). Você também pode usar o XEvent **query_store_plan_forcing_failed** para acompanhar e solucionar problemas de falhas de imposição de plano.

## <a name="avoid-renaming-databases-for-queries-with-forced-plans"></a><a name="Renaming"></a> Evitar renomear bancos de dados para consultas com planos forçados

Planos de execução fazem referência a objetos usando nomes de três partes, como `database.schema.object`.

Se você renomear um banco de dados, a imposição do plano falhará, causando recompilação em todas as execuções de consulta subsequentes.

## <a name="use-trace-flags-on-mission-critical-servers"></a><a name="Recovery"></a> Usar sinalizadores de rastreamento em servidores críticos

Os sinalizadores de rastreamento globais 7745 e 7752 podem ser usados para melhorar a disponibilidade dos bancos de dados usando o Repositório de Consultas. Para obter mais informações, confira [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).

- O sinalizador de rastreamento 7745 impede o comportamento padrão em que o Repositório de Consultas grava dados em disco antes que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possa ser desligado. Isso significa que os dados de Repositório de Consultas que foram coletados, mas ainda não foram mantidos no disco, serão perdidos até a janela de tempo definida com `DATA_FLUSH_INTERVAL_SECONDS`.
- O sinalizador de rastreamento 7752 permite o carregamento assíncrono do Repositório de Consultas. Isso permite colocar um banco de dados online e executar as consultas antes da recuperação total do Repositório de Consultas. O comportamento padrão é fazer um carregamento assíncrono do Repositório de Consultas. O comportamento padrão impede a execução de consultas antes da recuperação do Repositório de Consultas, mas também impede a perda de consultas na coleta de dados.

> [!NOTE]
> No [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] e em versões posteriores, o mecanismo controla esse comportamento e o sinalizador de rastreamento 7752 não tem nenhum efeito.

> [!IMPORTANT]
> Se você estiver usando o Repositório de Consultas para obter informações de carga de trabalho just-in-time no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], planeje instalar as correções de escalabilidade de desempenho na [KB 4340759](https://support.microsoft.com/help/4340759) assim que possível.

## <a name="see-also"></a>Confira também

- [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)
- [Exibições de Catálogo do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)
- [Procedimentos armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)
- [Usar o Repositório de Consultas com OLTP in-memory](../../relational-databases/performance/using-the-query-store-with-in-memory-oltp.md)
- [Monitorar o desempenho usando o Repositório de Consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)
