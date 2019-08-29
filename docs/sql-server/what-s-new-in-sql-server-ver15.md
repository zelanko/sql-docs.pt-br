---
title: Novidades no SQL Server 2019 | Microsoft Docs
ms.date: 08/21/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 275ef0ef83c073726cebf80b63e1d8f9640eca81
ms.sourcegitcommit: 676458a9535198bff4c483d67c7995d727ca4a55
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69903637"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>Novidades no [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] se baseia em versões anteriores para ampliar o SQL Server como uma plataforma que fornece opções de linguagens de desenvolvimento, tipos de dados, operações locais ou na nuvem e sistemas operacionais.

Este artigo resume os novos recursos e aprimoramentos para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Para obter mais informações e ver os problemas conhecidos, consulte as [Notas sobre a versão do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-ver15-release-notes.md).

**Use as [ferramentas mais recentes](what-s-new-in-sql-server-ver15-prerelease.md#tools) para melhorar sua experiência com o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].**

>[!NOTE]
>O conteúdo é publicado para a versão Release Candidate [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. A versão Release Candidate é um software de pré-lançamento. As informações estão sujeitas a alterações. Para obter informações sobre cenários de suporte, confira [Suporte](#support).
>
>Esta versão inclui melhorias que foram anunciadas anteriormente nas versões CTP (Community Technology Preview). Os aprimoramentos foram adicionados aos recursos, aos bugs corrigidos, à segurança aprimorada e ao desempenho otimizado. Para obter uma lista dos recursos introduzidos ou aprimorados nas versões CTP anteriores à versão Release Candidate [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], confira o [arquivo de anúncio do CTP [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](what-s-new-in-sql-server-ver15-prerelease.md).

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduz [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] para [!INCLUDE[sql-server](../includes/ssnoversion-md.md)]. Ele também fornece melhorias e recursos adicionais para o mecanismo de banco de dados do SQL Server, SQL Server Analysis Services, SQL Server Serviços de Machine Learning, SQL Server em Linux e SQL Server Master Data Services.

As seções a seguir fornecem uma visão geral desses recursos.

## [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]

| Novo recurso ou atualização | Detalhes |
|:---|:---|
| Solução de Big Data escalonável | [Implantar clusters escalonáveis](../big-data-cluster/deploy-get-started.md) de contêineres do SQL Server, do Spark e do HDFS em execução no Kubernetes <br/><br/> Ler, gravar e processar Big Data do Transact-SQL ou do Spark<br/><br/> Combine e analise facilmente dados relacionais de valor elevado com Big Data de volume grande<br/><br/>Consultar fontes de dados externas<br/><br/>Armazenar Big Data no HDFS gerenciado por SQL Server<br/><br/>Consultar dados de várias fontes de dados externas por meio do cluster<br/><br/> Usar os dados para IA, aprendizado de máquina e outras tarefas de análise<br/><br/> Implantar e executar aplicativos em [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] <br/>|
| &nbsp; | &nbsp; |

Para obter mais detalhes, confira [O que são SQL Server [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]](../big-data-cluster/big-data-cluster-overview.md).

[O arquivo de anúncios do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (CTP)](what-s-new-in-sql-server-ver15-prerelease.md) contém uma lista de recursos anunciados e alterados para todas as versões CTP anteriores desse recurso.

>[!NOTE]
>[!INCLUDE[ssbdc-rcnote](../includes/ssbigdataclusters-ver15-rcnote.md)]

## <a name="database-engine"></a>Mecanismo de banco de dados

### <a name="security"></a>Segurança

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Indexar colunas criptografadas|Criar índices em colunas criptografadas usando criptografia aleatória e chaves habilitada para enclave, a fim de melhorar o desempenho de consultas avançadas (usando `LIKE` e operadores de comparação). Veja [Always Encrypted com enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md).
|Suspender e retomar a verificação inicial para TDE (Transparent Data Encryption)|Confira [Verificação de TDE (Transparent Data Encryption) – suspender e retomar](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume).|
|Gerenciamento de certificados no SQL Server Configuration Manager|Confira [Gerenciamento de certificado (SQL Server Configuration Manager)](../database-engine/configure-windows/manage-certificates.md).|
| &nbsp; | &nbsp; |

### <a name="graph"></a>Gráfico

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Ações de exclusão em cascata de restrição de borda |Defina as ações de exclusão em cascata em uma restrição de borda em um banco de dados de grafo. Confira [Restrições de borda](../relational-databases/tables/graph-edge-constraints.md). |
|Nova função do grafo – `SHORTEST_PATH` | Use `SHORTEST_PATH` dentro de `MATCH` para localizar o caminho mais curto entre quaisquer dois nós em um grafo ou para executar passagens de comprimento arbitrário.|
|Índices e tabelas de partição| Os dados de tabelas e índices particionados são divididos em unidades que podem ser difundidas por mais de um grupo de arquivos em um banco de dados de grafo. |
|Usar aliases de exibição ou tabela derivada em consulta de correspondência de grafo |Confira [Consulta de correspondência de grafo](../t-sql/queries/match-sql-graph.md). |
| &nbsp; | &nbsp; |

### <a name="indexes"></a>Índices

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|Ativa uma otimização no [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que ajuda a melhorar a taxa de transferência para inserções de alta simultaneidade em um índice. Essa opção destina-se a índices que estão sujeitos a contenção de inserção de última página, geralmente vista com os índices que têm uma chave sequencial, tal como uma coluna de identidade, uma sequência ou uma coluna de data/hora. Para obter mais informações, veja [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys).|
|Compilar e recompilar o índice de columnstore em cluster online | Confira [Executar operações de índice online](../relational-databases/indexes/perform-index-operations-online.md). |
|Compilar o índice de rowstore online retomável | Confira [Executar operações de índice online](../relational-databases/indexes/perform-index-operations-online.md). |
| &nbsp; | &nbsp; |

### <a name="in-memory-databases"></a>Bancos de dados na memória

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Controle DDL para pool de buffers híbrido |Com o [pool de buffers híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md), as páginas de banco de dados que residem em arquivos de banco de dados colocados em um dispositivo PMEM (memória persistente) serão acessadas diretamente quando necessário.|
| &nbsp; | &nbsp; |

### <a name="unicode-support"></a>Suporte de Unicode

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Suporte para codificação de caracteres UTF-8 |Suporte para caractere UTF-8 para importação e exportação de codificação, e como agrupamento de nível de banco de dados ou de nível de coluna para dados de cadeia de caracteres. Isso dá suporte a aplicativos que se estendem para uma escala global, em que o requisito de fornecer aplicativos e serviços de banco de dados multilíngues globais é essencial para atender às demandas dos clientes e às regulamentações específicas do mercado. Confira [Suporte a agrupamentos e a Unicode](../relational-databases/collations/collation-and-unicode-support.md)<br/><br/>[a versão Release Candidate [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] habilita o suporte a UTF-8 para tabelas externas do Polybase e para Always Encrypted.|
| &nbsp; | &nbsp; |

### <a name="polybase"></a>PolyBase

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Consultar tabelas externas |Os nomes de coluna da tabela externa agora são usados para consultar fontes de dados de SQL Server, Oracle, Teradata, MongoDB e ODBC. Confira [O que é o PolyBase](../relational-databases/polybase/polybase-guide.md).|
|Suporte para codificação de caracteres UTF-8|Suporte a caracteres UTF-8 com tabelas externas. Confira [Suporte a agrupamentos e a Unicode](../relational-databases/collations/collation-and-unicode-support.md)|
| &nbsp; | &nbsp; |

### <a name="server-settings"></a>Configurações do servidor

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Pool de buffers híbrido| Novo recurso do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)], em que as páginas de banco de dados que residem em arquivos de banco de dados colocados em um dispositivo PMEM (memória persistente) serão acessadas diretamente quando necessário. Confira [Pool de buffers híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md).|
| &nbsp; | &nbsp; |

### <a name="performance-monitoring"></a>Monitoramento de desempenho

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | Novo tipo de espera em `sys.dm_os_wait_stats` na exibição de gerenciamento dinâmico. Ele mostra o tempo de nível de instância acumulado gasto em operações de atualização de estatísticas síncronas. Confira [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|
|Política de captura personalizada para o Repositório de Consultas|Quando habilitadas, as configurações adicionais do Repositório de Consultas ficam disponíveis em uma nova configuração de Política de Captura do Repositório de Consultas, a fim de ajustar a coleta de dados em um servidor específico. Para obter mais informações, veja [Opções ALTER DATABASE SET (Transact-SQL)](../t-sql/statements/alter-database-transact-sql-set-options.md).|
|`LIGHTWEIGHT_QUERY_PROFILING`|Nova configuração no escopo do banco de dados. Confira [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp). |
|`sys.dm_exec_requests` da coluna `command` | Mostra `SELECT (STATMAN)` se um `SELECT` está aguardando até que uma operação de atualização de estatísticas síncronas seja concluída antes de continuar a execução da consulta. Confira [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|
|`sys.dm_exec_query_plan_stats` |O novo DMF retorna o equivalente do último plano de execução real conhecido para a maioria das consultas. Confira [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md).|
|`LAST_QUERY_PLAN_STATS` | Nova configuração no escopo do banco de dados para habilitar o `sys.dm_exec_query_plan_stats`. Veja [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|`query_post_execution_plan_profile` | O evento estendido coleta o equivalente a um plano de execução real com base em criação de perfil leve, ao contrário de `query_post_execution_showplan`, que usa a criação de perfil padrão. Confira [Infraestrutura de criação de perfil de consulta](../relational-databases/performance/query-profiling-infrastructure.md).|
| &nbsp; | &nbsp; |

### <a name="language-extensions"></a>Extensões de linguagem

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Novo SDK de linguagem Java | Simplifica o desenvolvimento de programas Java que podem ser executados do SQL Server. Confira [SDK de extensibilidade da Microsoft para Java para SQL Server](../language-extensions/how-to/extensibility-sdk-java-sql-server.md). |
|O SDK da linguagem Java é um software livre |O [SDK de Extensibilidade da Microsoft para Java para Microsoft SQL Server](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) já é software livre e está [disponível no GitHub](https://github.com/microsoft/sql-server-language-extensions).|
|Suporte para tipos de dados Java|Confira [Tipos de dados Java](../language-extensions/how-to/java-to-sql-data-types.md).|
|Novo Java Runtime padrão | O SQL Server agora inclui suporte ao Zulu Embedded for Java da Azul System em todo o produto. Para obter mais informações, confira [Java com suporte gratuito no SQL Server 2019 agora está disponível](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/). |
|Extensões de linguagem do SQL Server| Execute o código externo com a estrutura de extensibilidade. Confira [Extensões de linguagem do SQL Server](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview).
|Registrar linguagens externas|A nova DDL, `CREATE EXTERNAL LANGUAGE`, registra linguagens externas, como Java, no SQL Server. Confira [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md). |
| &nbsp; | &nbsp; |

### <a name="spatial"></a>Espacial

|Novo recurso ou atualização | Detalhes |
|:---|:---|
| Novos SRIDs (identificadores de referência espacial) |[GDA2020 australiano](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) fornece uma referência mais robusta e precisa, que está alinhada mais estreitamente a sistemas de posicionamento global. Os novos SRIDs são:<br/><br/> – 7843 para 2D geográfico<br/> – 7844 para 3D geográfico <br/><br/>A exibição [spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) contém as definições de SRIDs novos. |
| &nbsp; | &nbsp; |

### <a name="performance"></a>Desempenho

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Recuperação de banco de dados acelerada | Habilitar a recuperação de banco de dados acelerada por banco de dados. Confira [Recuperação acelerada de banco de dados](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr).|
|Forçar cursores estáticos e de avanço rápido | Suporte à imposição de plano de Repositório de Consultas para cursores fast forward e static. Confira [Planejar forçar suporte para cursores estáticos e de avanço rápido](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23).|
|Recompilações reduzidas para cargas de trabalho| Melhora o uso de tabelas temporárias entre vários escopos. Confira [Recompilações reduzidas para cargas de trabalho](../relational-databases/tables/tables.md#ctp23) |
|Escalabilidade de ponto de verificação indireto |Confira [Escalabilidade de ponto de verificação indireto aprimorada](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23).|
|Metadados `tempdb` com otimização de memória| O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] apresenta um novo recurso que faz parte da família de recursos do [Banco de Dados em Memória](../relational-databases/in-memory-database.md), os metadados do `tempdb` com otimização de memória, que efetivamente remove esse gargalo e possibilita um novo nível de escalabilidade para cargas de trabalho com uso intenso do `tempdb`. No [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], as tabelas do sistema envolvidas no gerenciamento dos metadados da tabela temporária podem ser movidas para tabelas com otimização de memória não duráveis e livres de travas. Confira [Metadados com otimização de memória `tempdb`](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata).|
|Atualizações de PFS simultâneas|As [páginas PFS](https://techcommunity.microsoft.com/t5/SQL-Server/Under-the-covers-GAM-SGAM-and-PFS-pages/ba-p/383125) são páginas especiais dentro de um arquivo de banco de dados que o SQL Server usa para ajudar a localizar espaço livre ao alocar espaço para um objeto. A contenção de trava de página em páginas PFS é algo que normalmente está associado com [`tempdb`](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d), mas também pode ocorrer em bancos de dados de usuário quando há muitos threads de alocação de objeto simultâneos. Essa melhoria altera a maneira como a simultaneidade é gerenciada com atualizações de PFS para que elas possam ser atualizadas em uma trava compartilhada, em vez de uma trava exclusiva. Esse comportamento é ativado por padrão em todos os bancos de dados (incluindo `tempdb`) a partir do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].|
|Comentários de concessão de memória do modo de linha |Expande o recurso de comentários de concessão de memória do modo de lote, ajustando os tamanhos de concessão de memória para operadores de modo de lote e de linha. Isso pode corrigir automaticamente concessões excessivas que resultam em desperdício de memória e redução da simultaneidade e corrigir concessões de memória insuficientes que causam despejos dispendiosos no disco. Confira [Comentários de concessão de memória do modo de linha](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback). |
|Compilação adiada de variável da tabela|Melhora a qualidade do plano e o desempenho geral para consultas que fazem referência a variáveis de tabela. Durante a otimização e compilação inicial, esse recurso propaga estimativas de cardinalidade com base nas contagens reais de linha de variável de tabela. Essas informações de contagem de linha precisas otimizam as operações de plano de downstream. Confira [Compilação adiada de variável da tabela](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation). |
|`APPROX_COUNT_DISTINCT `|Para cenários em que a precisão absoluta não é importante, mas a capacidade de resposta é essencial, `APPROX_COUNT_DISTINCT` agrega grandes conjuntos de dados usando menos recursos do que `COUNT(DISTINCT())` para uma simultaneidade superior. Confira [Processamento de consulta aproximada](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing).|
|Modo de Lote no Rowstore|O modo de lote em rowstore permite que a execução em modo de lote sem a necessidade de índices columnstore. A execução do modo em lote usa a CPU com mais eficiência durante cargas de trabalho analíticas, mas até [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] ela era usada apenas quando uma consulta incluía operações com índices columnstore. No entanto, alguns aplicativos podem usar recursos sem suporte dos índices columnstore e, portanto, não poderiam aproveitar o modo de lote. A partir do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], o modo de lote é habilitado em cargas de trabalho analíticas qualificadas cujas consultas incluem operações com qualquer tipo de índice (rowstore ou columnstore). Confira [Modo de lote em rowstore](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore). |
|Embutimento de UDF escalar|Transforma automaticamente UDFs escalares em expressões relacionais e as insere na consulta SQL chamada. Essa transformação melhora o desempenho de cargas de trabalho que aproveitam as UDFs escalares. [Inlining de UDF escalar](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining).|
| &nbsp; | &nbsp; |

### <a name="availability-groups"></a>Grupos de disponibilidade

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Até cinco réplicas síncronas|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] aumenta o número máximo de réplicas síncronas para 5, um aumento com relação às 3 no [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Você pode configurar esse grupo de cinco réplicas para ter failover automático dentro do grupo. Há uma réplica primária, além de quatro réplicas secundárias síncronas.|
|Redirecionamento de conexão de réplica secundária para primária| Permite que conexões do aplicativo cliente sejam direcionadas para a réplica primária, independentemente do servidor de destino especificado na cadeia de conexão. Para conhecer os detalhes, consulte [Secondary to primary replica read/write connection redirection (Always On Availability Groups)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) (Redirecionamento de conexão de leitura/gravação de réplica secundária para primária [Grupos de Disponibilidade Always On]).|
| &nbsp; | &nbsp; |

### <a name="setup"></a>Instalação 

|Novo recurso ou atualização | Detalhes | 
|:---|:---| 
|Novas opções de configuração de memória | Define durante a instalação as configurações de servidor de *memória mínima do servidor (MB)* e *memória máxima do servidor (MB)* . Para obter mais informações, confira a [página Configuração do mecanismo de banco de dados – memória](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#memory) e os parâmetros `USESQLRECOMMENDEDMEMORYLIMITS`, `SQLMINMEMORY` e `SQLMAXMEMORY` em [Instalar o SQL Server do prompt de comando](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install). O valor proposto será alinhado com as diretrizes de configuração de memória nas [Opções de configuração de memória do servidor](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually).| 
|Novas opções de configuração de paralelismo | Define o *grau máximo de configuração de* servidor de paralelismo durante a instalação. Para obter mais informações, confira a [página Configuração do mecanismo de banco de dados – MaxDOP](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#maxdop) e o parâmetro `SQLMAXDOP` em [Instalar SQL Server no prompt de comando](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install). O valor padrão será alinhado às diretrizes de grau máximo da opção de paralelismo especificadas em [Configurar a opção de configuração de servidor grau máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines).| 
| &nbsp; | &nbsp; |

### <a name="error-messages"></a>Mensagens de erro

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Avisos de truncamento detalhados | A mensagem de erro de truncamento inclui por padrão nomes de tabela e coluna, bem como o valor truncado. Confira [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation).|
| &nbsp; | &nbsp; |

## <a name="sql-server-on-linux"></a>SQL Server no Linux

| Novo recurso ou atualização | Detalhes |
|:-----|:-----|
|Novo registro de contêiner|[Introdução a contêineres do SQL Server no Docker](../linux/quickstart-install-connect-docker.md) |
|Suporte para replicação |[Objetos de replicação do SQL Server em Linux](../linux/sql-server-linux-replication.md)
|Suporte para MSDTC (Coordenador de Transações Distribuídas da Microsoft) |[Como configurar o MSDTC no Linux](../linux/sql-server-linux-configure-msdtc.md) |
|Suporte para OpenLDAP para provedores de AD de terceiros |[Tutorial: Usar autenticação do Azure Active Directory com o SQL Server em Linux](../linux/sql-server-linux-active-directory-authentication.md) |
|Machine Learning no Linux |[Configurar o Machine Learning no Linux](../linux/sql-server-linux-setup-machine-learning.md) |
|Aprimoramentos `tempdb` | Por padrão, uma nova instalação do SQL Server em Linux cria vários arquivos de dados `tempdb` com base no número de núcleos lógicos (com até 8 arquivos de dados). Isso não é aplicável a upgrades de versões principais ou secundárias no local. Cada arquivo do `tempdb` tem 8 MB com um aumento automático de 64 MB. Esse comportamento é semelhante à instalação padrão do SQL Server no Windows. |
| PolyBase em Linux | [Instalar o PolyBase](../relational-databases/polybase/polybase-linux-setup.md) no Linux para conectores não Hadoop.<br/><br/>[Mapeamento de tipo do PolyBase](../relational-databases/polybase/polybase-type-mapping.md). |
| Suporte ao CDC (captura de dados de alterações) | O CDC (captura de dados de alterações) agora é compatível no Linux para SQL Server 2019. |
| &nbsp; | &nbsp; |

### <a name="setup"></a>Instalação

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Novas opções de configuração de memória | Define durante a instalação as configurações de servidor de *memória mínima do servidor (MB)* e *memória máxima do servidor (MB)* . Para obter mais informações, confira os parâmetros `USESQLRECOMMENDEDMEMORYLIMITS`, `SQLMINMEMORY` e `SQLMAXMEMORY` em [Instalar SQL Server no prompt de comando](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install). O valor proposto será alinhado com as diretrizes de configuração de memória nas [Opções de configuração de memória do servidor](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually).|
|Novas opções de configuração de paralelismo | Define o *grau máximo de configuração de* servidor de paralelismo durante a instalação. Para obter mais informações, confira o parâmetro `SQLMAXDOP` em [Instalar SQL Server no prompt de comando](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install). O valor padrão será alinhado às diretrizes de grau máximo da opção de paralelismo especificadas em [Configurar a opção de configuração de servidor grau máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines).|
| &nbsp; | &nbsp; |

## <a id="ml"></a> Serviços de Machine Learning do SQL Server

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Modelagem baseada em partição|Processe scripts externos por partição de seus dados usando os novos parâmetros adicionados ao `sp_execute_external_script`. Essa funcionalidade dá suporte ao treinamento de muitos modelos pequenos (um modelo para cada partição de dados) em vez de um modelo grande. Confira [Criar modelos baseados em partição](../advanced-analytics/tutorials/r-tutorial-create-models-per-partition.md)|
|Cluster de failover do Windows Server| Configure alta disponibilidade para Serviços do Machine Learning em um Cluster de failover do Windows Server.|
| &nbsp; | &nbsp; |

## [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]

| Novo recurso ou atualização | Detalhes |
|:---|:---|
|Dá suporte a bancos de dados de instância gerenciada do Banco de Dados SQL do Azure.| Hospede [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] em uma instância gerenciada. Confira [Instalação e configuração do [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]](../master-data-services/master-data-services-installation-and-configuration.md#SetUpWeb).|
|Novos controles HTML| Os controles HTML substituem todos os componentes do Silverlight anteriores. Dependência do Silverlight removida.|
| &nbsp; | &nbsp; |

## <a name="analysis-services"></a>Analysis Services

| Novo recurso ou atualização | Detalhes |
|:---|:---|
|Intercalação de consulta| Confira [Intercalação de consulta](https://docs.microsoft.com/analysis-services/tabular-models/query-interleaving) |
|Suporte a consulta MDX para modelos de tabela com grupos de cálculo | Confira [Grupos de cálculo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). |
|Grupos de cálculo em modelo tabular| [Grupos de cálculo em modelo tabular](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|Suporte a consulta MDX para modelos de tabela com grupos de cálculo | Confira [Grupos de cálculo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). |
|Formatação dinâmica de medidas usando grupos de cálculo |Esse recurso permite que você altere condicionalmente cadeias de caracteres de formato para medidas com [grupos de cálculo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). Por exemplo, com a conversão de moeda, uma medida pode ser exibida usando diferentes formatos de moeda estrangeira.|
|Relações muitos para muitos em modelos tabulares|[Relações muitos para muitos em modelos tabulares](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|Configurações de propriedade para governança de recursos|[Configurações de propriedade para governança de recursos](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
| Configuração de governança para atualizações de cache do Power BI.  | O serviço do Power BI armazena em cache dados de bloco do dashboard e dados de relatório para carregamento inicial do relatório do Live Connect, fazendo com que um número excessivo de consultas de cache seja enviado ao SSAS e, em casos extremos, sobrecarregue o servidor. Esta versão introduz a propriedade **ClientCacheRefreshPolicy**. Essa propriedade permite que você substitua esse comportamento no nível do servidor. Para saber mais, confira [Propriedades gerais](https://docs.microsoft.com/analysis-services/server-properties/general-properties). |
| Anexação online  | Esse recurso fornece a capacidade de anexar um modelo de tabela como uma operação online. A anexação online pode ser usada para sincronização de réplicas somente leitura em ambientes de expansão de consulta local. Para saber mais, confira [Anexação online](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32) em Detalhes. |
| &nbsp; | &nbsp; |

[!INCLUDE[ctp-support-exclusion](../includes/ctp-support-exclusion.md)]

Para recursos específicos excluídos do suporte, confira as [notas sobre a versão](sql-server-ver15-release-notes.md).

Além disso, os recursos a seguir foram adicionados ou aprimorados para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2.

## <a name="see-also"></a>Confira também

- [`SqlServer` Módulo do PowerShell](https://www.powershellgallery.com/packages/Sqlserver)
- [Documentação do SQL Server PowerShell](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>Próximas etapas

- [[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]Notas sobre a versão](sql-server-ver15-release-notes.md).

- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: White paper técnico](http://info.microsoft.com/rs/157-GQE-382/images/EN-US-CNTNT-white-paper-DBMod-Microsoft-SQL-Server-2019-Technical-white-paper.pdf)<br />Publicado em setembro de 2018. Aplica-se ao Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 2.0 para contêineres do Windows, Linux e Docker.

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
