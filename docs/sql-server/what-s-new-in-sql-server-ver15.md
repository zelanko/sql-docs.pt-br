---
title: Novidades no SQL Server 2019 | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d988fc9dfc126bef79d94ca0867128085069456e
ms.sourcegitcommit: 63c6f3758aaacb8b72462c2002282d3582460e0b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/25/2019
ms.locfileid: "68495447"
---
# <a name="whats-new-in-includesql-server-2019includessssqlv15-mdmd"></a>Novidades no [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] se baseia em versões anteriores para ampliar o SQL Server como uma plataforma que fornece opções de linguagens de desenvolvimento, tipos de dados, operações locais ou na nuvem e sistemas operacionais.

Este artigo resume os novos recursos e aprimoramentos para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Para obter mais informações e ver os problemas conhecidos, consulte as [Notas sobre a versão do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-ver15-release-notes.md).

**Use as [ferramentas mais recentes](what-s-new-in-sql-server-ver15-prerelease.md#tools) para melhorar sua experiência com o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].**

## <a name="ctp-32-july-2019"></a>CTP 3.2 de julho de 2019

O CTP (Community Technology Preview) 3.2 é a última versão pública do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. Esta versão inclui aprimoramentos de versões CTP anteriores para corrigir bugs, melhorar a segurança e otimizar o desempenho. Para obter uma lista dos recursos introduzidos ou aprimorados em cada uma das versões CTP anteriores ao [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP 3.2, confira [arquivo de anúncio do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] CTP](what-s-new-in-sql-server-ver15-prerelease.md).

### <a name="new-in-big-data-clusters"></a>Novidades em clusters de Big Data

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Versão prévia pública |Antes do CTP 3.2, o cluster de Big Data do SQL Server estava disponível para os usuários pioneiros registrados. Esta versão permite que qualquer pessoa experimente os recursos dos clusters de Big Data do SQL Server. <br/><br/> Confira [Introdução aos clusters de Big data do SQL Server](../big-data-cluster/deploy-get-started.md).|
|`azdata` |O CTP 3.2 apresenta o `azdata` – um utilitário de linha de comando escrito em Python que permite aos administradores de cluster inicializar e gerenciar o cluster de Big Data por meio de APIs REST. O `azdata` substitui o `mssqlctl`. Confira [Instalar o `azdata`](../big-data-cluster/deploy-install-azdata.md). |
|PolyBase |Os nomes de coluna da tabela externa agora são usados para consultar fontes de dados de SQL Server, Oracle, Teradata, MongoDB e ODBC. Nas versões CTP anteriores, as colunas eram vinculadas somente com base no ordinal no destino e os nomes de coluna na definição de tabela externa não eram usados.|
|Atualização de camadas do HDFS |Introdução da funcionalidade de atualização de camadas do HDFS para que uma montagem existente possa ser atualizada para o instantâneo mais recente dos dados remotos. Confira [Camadas do HDFS](../big-data-cluster/hdfs-tiering.md) |
|Solução de problemas baseada em notebook |O CTP 3.2 introduz notebooks Jupyter para auxiliar na [implantação](../big-data-cluster/deploy-notebooks.md) e [descoberta, diagnóstico e solução de problemas](../big-data-cluster/manage-notebooks.md) de componentes em um cluster de Big Data do SQL Server. |
| &nbsp; | &nbsp; |

### <a name="new-in-analysis-services"></a>Novidades do Analysis Services

| Novo recurso ou atualização | Detalhes |
|:---|:---| 
| Configuração de governança para atualizações de cache do Power BI.  | O serviço do Power BI armazena em cache dados de bloco do dashboard e dados de relatório para carregamento inicial do relatório do Live Connect, fazendo com que um número excessivo de consultas de cache seja enviado ao SSAS e, em casos extremos, sobrecarregue o servidor. Esta versão introduz a propriedade **ClientCacheRefreshPolicy**. Essa propriedade permite que você substitua esse comportamento no nível do servidor. Para saber mais, confira [Propriedades gerais](../analysis-services/server-properties/general-properties.md). |
| Anexação online  | Esse recurso fornece a capacidade de anexar um modelo de tabela como uma operação online. A anexação online pode ser usada para sincronização de réplicas somente leitura em ambientes de expansão de consulta local. Para saber mais, confira [Anexação online](what-s-new-in-sql-server-ver15-prerelease.md#online-attach-ctp32) em Detalhes. |
| &nbsp; | &nbsp; |

### <a name="new-in-language-extensions"></a>Novidades em extensões de linguagem

|Novo recurso ou atualização | Detalhes |
|:---|:---|
| Novo Java Runtime padrão  | O SQL Server agora inclui suporte ao Zulu Embedded for Java da Azul System em todo o produto. Para obter mais informações, confira [Java com suporte gratuito no SQL Server 2019 agora está disponível](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/). |

### <a name="new-in-sql-server-on-linux"></a>Novidades no SQL Server em Linux

|Novo recurso ou atualização | Detalhes |
|:---|:---|
| Suporte ao CDC (captura de dados de alterações) | O CDC (captura de dados de alterações) agora é compatível no Linux para SQL Server 2019. |

## <a name="includesql-server-2019includessssqlv15-mdmd-features-by-component"></a>Recursos por componente do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

As seções a seguir destacam novos componentes e recursos que foram aprimorados em versões anteriores do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

## <a name="big-data-clusters"></a>Clusters de Big Data

| Novo recurso ou atualização | Detalhes |
|:---|:---|
| Solução de Big Data escalonável | [Implantar clusters escalonáveis](../big-data-cluster/deploy-get-started.md) de contêineres do SQL Server, do Spark e do HDFS em execução no Kubernetes <br/><br/> Ler, gravar e processar Big Data do Transact-SQL ou do Spark<br/><br/> Combine e analise facilmente dados relacionais de valor elevado com Big Data de volume grande<br/><br/>Consultar fontes de dados externas<br/><br/>Armazenar Big Data no HDFS gerenciado por SQL Server<br/><br/>Consultar dados de várias fontes de dados externas por meio do cluster<br/><br/> Usar os dados para IA, aprendizado de máquina e outras tarefas de análise<br/><br/> Implantar e executar aplicativos em clusters de Big Data <br/>|
| &nbsp; | &nbsp; |

Para obter mais detalhes, confira [O que são os clusters de Big Data do SQL Server?](../big-data-cluster/big-data-cluster-overview.md)

[O arquivo de anúncios do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] (CTP)](what-s-new-in-sql-server-ver15-prerelease.md) contém uma lista de recursos anunciados e alterados para todas as versões CTP anteriores desse recurso.

## <a name="database-engine"></a>Mecanismo de banco de dados

### <a name="security"></a>Segurança

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Restrições da funcionalidade| Prevenir que algumas formas de injeção de SQL vazem informações sobre o banco de dados, mesmo quando a injeção de SQL é bem-sucedida. Confira [Restrições de funcionalidade](../relational-databases/security/feature-restrictions.md)|
|Indexar colunas criptografadas|Criar índices em colunas criptografadas usando criptografia aleatória e chaves habilitada para enclave, a fim de melhorar o desempenho de consultas avançadas (usando `LIKE` e operadores de comparação). Veja [Always Encrypted com enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md).
|Suspender e retomar a verificação inicial para TDE (Transparent Data Encryption)|Confira [Verificação de TDE (Transparent Data Encryption) – suspender e retomar](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume)|
|Gerenciamento de certificados no SQL Server Configuration Manager|Confira [Gerenciamento de certificado (SQL Server Configuration Manager)](../database-engine/configure-windows/manage-certificates.md)
| &nbsp; | &nbsp; |


### <a name="graph"></a>Gráfico

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Ações de exclusão em cascata de restrição de borda |Defina as ações de exclusão em cascata em uma restrição de borda em um banco de dados de grafo. Confira [Restrições de borda](../relational-databases/tables/graph-edge-constraints.md). |
|Nova função do grafo – `SHORTEST_PATH` | Use `SHORTEST_PATH` dentro de `MATCH` para localizar o caminho mais curto entre quaisquer dois nós em um grafo ou para executar passagens de comprimento arbitrário.|
|Índices e tabelas de partição| Os dados de tabelas e índices particionados são divididos em unidades que podem ser difundidas por mais de um grupo de arquivos em um banco de dados de grafo. |
|Usar aliases de exibição ou tabela derivada em consulta de correspondência de grafo |Confira [Restrições de borda de grafo](../relational-databases/tables/graph-edge-constraints.md). |
| &nbsp; | &nbsp; |

### <a name="indexes"></a>Índices

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|Ativa uma otimização no mecanismo de banco de dados que ajuda a melhorar a taxa de transferência para inserções de alta simultaneidade em um índice. Essa opção destina-se a índices que estão sujeitos a contenção de inserção de última página, geralmente vista com os índices que têm uma chave sequencial, tal como uma coluna de identidade, uma sequência ou uma coluna de data/hora. Para obter mais informações, veja [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys).|
|Compilar e recompilar índices de columnstore em cluster online | Confira [Executar operações de índice online](../relational-databases/indexes/perform-index-operations-online.md). |
| &nbsp; | &nbsp; |

### <a name="in-memory-databases"></a>Bancos de dados na memória

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Controle DDL para pool de buffers híbrido |Com o [pool de buffers híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md), as páginas de banco de dados que residem em arquivos de banco de dados colocados em um dispositivo PMEM (memória persistente) serão acessadas diretamente quando necessário.|
|Metadados do tempdb com otimização de memória|Confira [Metadados do TempDB com otimização de memória](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata)|
| &nbsp; | &nbsp; |

### <a name="linked-servers"></a>Servidores vinculados

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Os servidores vinculados dão suporte a codificação de caracteres UTF-8. |[Suporte a ordenações e a Unicode](../relational-databases/collations/collation-and-unicode-support.md) |
| &nbsp; | &nbsp; |

### <a name="polybase"></a>PolyBase

|Novo recurso ou atualização | Detalhes | PolyBase | Os nomes de coluna da tabela externa agora são usados para consultar fontes de dados de SQL Server, Oracle, Teradata, MongoDB e ODBC. | | &nbsp; | &nbsp; |

### <a name="collation"></a>Ordenação

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Suporte a codificação de caracteres UTF-8 |Habilitado para um agrupamento BIN2 (`Latin1_General_100_BIN2_UTF8`). Confira [Suporte a agrupamentos e a Unicode](../relational-databases/collations/collation-and-unicode-support.md). |
|Selecionar o agrupamento de UTF-8 como padrão durante a instalação | Confira [Suporte a agrupamentos e a Unicode](../relational-databases/collations/collation-and-unicode-support.md#ctp23). |
| &nbsp; | &nbsp; |

### <a name="server-settings"></a>Configurações do servidor

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Definir os valores de memória do servidor `MIN` e `MAX` na instalação |Durante a instalação, você pode definir valores de memória do servidor. Use os valores padrão, os valores recomendados calculados ou especifique manualmente seus próprios valores depois de escolher a opção **Recomendado** em [Opções de Configuração de Memória do Servidor](../database-engine/configure-windows/server-memory-server-configuration-options.md#setting-the-memory-options-manually).|
|A Instalação do SQL Server habilita as configurações de MAXDOP |As novas recomendações seguem as diretrizes documentadas. [Configurar a opção de configuração de servidor max degree of parallelism](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines)|
|Pool de buffers híbrido| É um novo recurso do mecanismo de banco de dados do SQL Server em que páginas de banco de dados em arquivos de banco de dados são colocadas em um dispositivo de PMEM (memória persistente) que será acessado diretamente quando necessário. Confira [Pool de buffers híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md).|
| &nbsp; | &nbsp; |

### <a name="performance-monitoring"></a>Monitoramento de desempenho

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Embutimento de UDF escalar |Transforma automaticamente UDFs (funções definidas pelo usuário) escalares em expressões relacionais e as insere na consulta SQL chamada. Confira [Inlining de UDF escalar](../relational-databases/user-defined-functions/scalar-udf-inlining.md). |
| `sys.dm_exec_requests` da coluna `command` | Mostra `SELECT (STATMAN)` se um `SELECT` está aguardando até que uma operação de atualização de estatísticas síncronas seja concluída antes de continuar a execução da consulta. Confira [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | Novo tipo de espera em `sys.dm_os_wait_stats` na exibição de gerenciamento dinâmico. Ele mostra o tempo de nível de instância acumulado gasto em operações de atualização de estatísticas síncronas. Confira [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|
|Política de captura personalizada para o Repositório de Consultas|Quando habilitadas, as configurações adicionais do Repositório de Consultas ficam disponíveis em uma nova configuração de Política de Captura do Repositório de Consultas, a fim de ajustar a coleta de dados em um servidor específico. Para obter mais informações, veja [Opções ALTER DATABASE SET (Transact-SQL)](../t-sql/statements/alter-database-transact-sql-set-options.md).|
|`sys.dm_exec_query_plan_stats` |O novo DMF retorna o equivalente do último plano de execução real conhecido para a maioria das consultas. Confira [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md).|
|`LAST_QUERY_PLAN_STATS` | Nova configuração no escopo do banco de dados para habilitar o `sys.dm_exec_query_plan_stats`. Veja [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|`LIGHTWEIGHT_QUERY_PROFILING`|Nova configuração no escopo do banco de dados. Confira [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp). |
|`query_post_execution_plan_profile` | O evento estendido coleta o equivalente a um plano de execução real com base em criação de perfil leve, ao contrário de `query_post_execution_showplan`, que usa a criação de perfil padrão. Confira [Infraestrutura de criação de perfil de consulta](../relational-databases/performance/query-profiling-infrastructure.md).|
|Comentários de concessão de memória do modo de linha. |[Comentários de concessão de memória do modo de linha](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback) |
|Compilação adiada de variável da tabela.|[Compilação Adiada de Variável da Tabela](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation) |
|`COUNT DISTINCT` aproximado.|[Processamento de consulta aproximada](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing)|
|Modo de Lote em rowstore.|[Modo de Lote no Rowstore](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore) |

### <a name="language-extensions"></a>Extensões de linguagem

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Novo SDK de linguagem Java | Simplifica o desenvolvimento de programas Java que podem ser executados do SQL Server. Veja [Novidades em Serviços do Machine Learning do SQL Server](../advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md). |
|Extensões de Linguagem do SQL Server – [Extensão da linguagem Java](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview)|O [SDK de Extensibilidade da Microsoft para Java para Microsoft SQL Server](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) já é software livre e está [disponível no GitHub](https://github.com/microsoft/sql-server-language-extensions).|
|Registrar linguagens externas|A nova DDL, `CREATE EXTERNAL LANGUAGE`, registra linguagens externas, como Java, no SQL Server. Confira [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md). |
|Suporte para tipos de dados Java|Confira [Tipos de dados Java](../language-extensions/how-to/java-to-sql-data-types.md).|

### <a name="spatial"></a>Espacial

|Novo recurso ou atualização | Detalhes |
|:---|:---|
| Novos SRIDs (identificadores de referência espacial) |[GDA2020 australiano](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) fornece uma referência mais robusta e precisa, que está alinhada mais estreitamente a sistemas de posicionamento global. Os novos SRIDs são:<br/><br/> – 7843 – 2D geográfico<br/> – 7844 – 3D geográfico <br/><br/>A exibição [spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md) contém as definições de SRIDs novos. |
| &nbsp; | &nbsp; |

### <a name="performance"></a>Desempenho

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Recuperação de banco de dados acelerada | Habilitar a recuperação de banco de dados acelerada por banco de dados. Confira [Recuperação acelerada de banco de dados](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr).|
|Forçar cursores estáticos e de avanço rápido | Suporte à imposição de plano de Repositório de Consultas para cursores fast forward e static. Confira [Planejar forçar suporte para cursores estáticos e de avanço rápido](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23).|
|Recompilações reduzidas para cargas de trabalho| Melhora o uso de tabelas temporárias entre vários escopos. Confira [Recompilações reduzidas para cargas de trabalho](../relational-databases/tables/tables.md#ctp23) |
|Escalabilidade de ponto de verificação indireto |Confira [Escalabilidade de ponto de verificação indireto aprimorada](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23).|
| &nbsp; | &nbsp; |

### <a name="availability-groups"></a>Grupos de disponibilidade

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Até cinco réplicas síncronas|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] aumenta o número máximo de réplicas síncronas para 5, um aumento com relação às 3 no [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Você pode configurar esse grupo de cinco réplicas para ter failover automático dentro do grupo. Há uma réplica primária, além de quatro réplicas secundárias síncronas.|
|Redirecionamento de conexão de réplica secundária para primária| Permite que conexões do aplicativo cliente sejam direcionadas para a réplica primária, independentemente do servidor de destino especificado na cadeia de conexão. Para conhecer os detalhes, consulte [Secondary to primary replica read/write connection redirection (Always On Availability Groups)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) (Redirecionamento de conexão de leitura/gravação de réplica secundária para primária [Grupos de Disponibilidade Always On]).|
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
|Grupos de Disponibilidade Always On em contêineres do Docker com Kubernetes |[Grupos de Disponibilidade Always On para contêineres](../linux/sql-server-ag-kubernetes.md) |
|Suporte para replicação |[Objetos de replicação do SQL Server em Linux](../linux/sql-server-linux-replication.md)
|Suporte para MSDTC (Coordenador de Transações Distribuídas da Microsoft) |[Como configurar o MSDTC no Linux](../linux/sql-server-linux-configure-msdtc.md) |
|Suporte para OpenLDAP para provedores de AD de terceiros |[Tutorial: Usar autenticação do Azure Active Directory com o SQL Server em Linux](../linux/sql-server-linux-active-directory-authentication.md) |
|Machine Learning no Linux |[Configurar o Machine Learning no Linux](../linux/sql-server-linux-setup-machine-learning.md) |
|Aprimoramentos do Tempdb | Por padrão, uma nova instalação do SQL Server em Linux cria vários arquivos de dados tempdb com base no número de núcleos lógicos (com até 8 arquivos de dados). Isso não é aplicável a upgrades de versões principais ou secundárias no local. Cada arquivo do tempdb tem 8 MB com um aumento automático de 64 MB. Esse comportamento é semelhante à instalação padrão do SQL Server no Windows. |
| PolyBase em Linux | [Instalar o PolyBase](../relational-databases/polybase/polybase-linux-setup.md) no Linux para conectores não Hadoop.<br/><br/>[Mapeamento de tipo do PolyBase](../relational-databases/polybase/polybase-type-mapping.md). |
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
|Grupos de cálculo em modelo tabular| [Grupos de cálculo em modelo tabular](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24) |
|Suporte a consulta MDX para modelos de tabela com grupos de cálculo | Confira [Grupos de cálculo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). |
|Formatação dinâmica de medidas usando grupos de cálculo |Esse recurso permite que você altere condicionalmente cadeias de caracteres de formato para medidas com [grupos de cálculo](what-s-new-in-sql-server-ver15-prerelease.md#calc-ctp24). Por exemplo, com a conversão de moeda, uma medida pode ser exibida usando diferentes formatos de moeda estrangeira.|
|Relações muitos para muitos em modelos tabulares|[Relações muitos para muitos em modelos tabulares](what-s-new-in-sql-server-ver15-prerelease.md#many-to-many-ctp24)|
|Configurações de propriedade para governança de recursos|[Configurações de propriedade para governança de recursos](what-s-new-in-sql-server-ver15-prerelease.md#property-ctp24)|
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
