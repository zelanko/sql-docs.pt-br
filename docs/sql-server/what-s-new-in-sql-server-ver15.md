---
title: Novidades no SQL Server 2019 | Microsoft Docs
description: Saiba mais sobre os novos recursos do SQL Server 2019 (15.x), que oferecem opções de linguagens de desenvolvimento, tipos de dados, ambientes e sistemas operacionais.
ms.date: 11/04/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15'
ms.openlocfilehash: 28b2d4cf892aa21b44d989fb56351a6ab5448bff
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482284"
---
# <a name="whats-new-in-sql-server-2019"></a>Novidades no [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]

[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] baseia-se em versões anteriores para ampliar o SQL Server como uma plataforma que fornece opções de linguagens de desenvolvimento, tipos de dados, ambientes locais ou na nuvem e sistemas operacionais.

Este artigo resume os novos recursos e aprimoramentos para o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)].

Para obter mais informações e ver os problemas conhecidos, confira as [notas sobre a versão do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-version-15-release-notes.md).

Para a melhor experiência com o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], use as [ferramentas mais recentes](https://aka.ms/getazuredatastudio).

[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduz [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] para [!INCLUDE[sql-server](../includes/ssnoversion-md.md)]. Ele também fornece melhorias e recursos adicionais para o mecanismo de banco de dados do SQL Server, SQL Server Analysis Services, SQL Server Serviços de Machine Learning, SQL Server em Linux e SQL Server Master Data Services.

O vídeo a seguir fornece uma introdução de 13 minutos ao SQL Server 2019:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Introducing-SQL-Server-2019/player?WT.mc_id=dataexposed-c9-niner]


As seções a seguir fornecem uma visão geral desses recursos.

## <a name="data-virtualization-and-big-data-clusters-2019"></a>Virtualização de dados e [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]

Hoje em dia, as empresas costumam gerenciar grandes acervos de dados que consistem em uma ampla gama de conjuntos de dados cada vez maiores e são hospedados em fontes de dados em silos e presentes em toda a empresa. Obter informações quase em tempo real de todos os seus dados com [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], que fornecem um ambiente completo para trabalhar com grandes conjuntos de dados, incluindo funcionalidades de aprendizado de máquina e IA.

| Novo recurso ou atualização | Detalhes |
|:---|:---|
| Solução de Big Data escalonável | [Implantar clusters escalonáveis](../big-data-cluster/deploy-get-started.md) de contêineres do SQL Server, do Spark e do HDFS em execução no Kubernetes. <br/><br/> Ler, gravar e processar Big Data do Transact-SQL ou do Spark.<br/><br/> Combine e analise facilmente dados relacionais de valor elevado com Big Data de volume grande.<br/><br/>Consultar fontes de dados externas.<br/><br/>Armazenar Big Data no HDFS gerenciado por SQL Server.<br/><br/>Consultar dados de várias fontes de dados externas por meio do cluster.<br/><br/> Usar os dados para IA, aprendizado de máquina e outras tarefas de análise.<br/><br/> [Implantar e executar aplicativos](../big-data-cluster/concept-application-deployment.md) em [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)]. <br/><br/> A instância mestra do SQL Server fornece alta disponibilidade e recuperação de desastre para todos os bancos de dados usando a tecnologia de grupo de disponibilidade Always On.<br/>|
|Virtualização de dados com o PolyBase | Consulte dados de SQL Server externos, Oracle, Teradata, MongoDB e fontes de dados ODBC com tabelas externas, agora com [suporte à codificação UTF-8](../relational-databases/collations/collation-and-unicode-support.md). Para saber mais, confira [O que é PolyBase?](../relational-databases/polybase/polybase-guide.md).|
| &nbsp; | &nbsp; |

Para obter mais informações, confira [O que são [!INCLUDE[big-data-clusters](../includes/ssbigdataclusters-nover.md)] do SQL Server?](../big-data-cluster/big-data-cluster-overview.md).

## <a name="intelligent-database"></a>Banco de dados inteligente
O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] baseia-se em inovações em versões anteriores para fornecer um desempenho líder do setor pronto para uso. Do [Processamento de Consulta Inteligente](../relational-databases/performance/intelligent-query-processing.md) para dar suporte a dispositivos de memória persistente, os recursos do Banco de Dados Inteligente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] aprimoram o desempenho e a escalabilidade de todas as cargas de trabalho de banco de dados sem nenhuma alteração ao design do aplicativo ou do banco de dados.

### <a name="intelligent-query-processing"></a>Processamento de consulta inteligente
Com o [Processamento de Consulta Inteligente](../relational-databases/performance/intelligent-query-processing.md), você sabe que cargas de trabalho paralelas críticas melhoram quando estão em execução em escala. Ao mesmo tempo, elas permanecem adaptáveis ao mundo dos dados em constante mudança. O Processamento de Consulta Inteligente está disponível por padrão na configuração mais recente do [nível de compatibilidade do banco de dados](../t-sql/statements/alter-database-transact-sql-compatibility-level.md#differences-between-compatibility-level-140-and-level-150), proporcionando um amplo impacto que melhora o desempenho das cargas de trabalho existentes com mínimo esforço de implementação.

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Comentários de concessão de memória do modo de linha |Expande o recurso de comentários de concessão de memória do modo de lote, ajustando os tamanhos de concessão de memória para operadores de modo de lote e de linha. Esse ajuste pode corrigir automaticamente concessões excessivas, o que resulta em desperdício de memória e menor simultaneidade. Também pode corrigir concessões de memória insuficientes que causam derramamentos caros no disco. Confira [Comentários de concessão de memória do modo de linha](../relational-databases/performance/intelligent-query-processing.md#row-mode-memory-grant-feedback). |
|Modo de Lote no Rowstore | Permite que a execução em modo de lote sem a necessidade de índices columnstore. A execução do modo em lote usa a CPU com mais eficiência durante cargas de trabalho analíticas, mas até [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] ela era usada apenas quando uma consulta incluía operações com índices columnstore. No entanto, alguns aplicativos podem usar recursos sem suporte dos índices columnstore e, portanto, não podem utilizar o modo de lote. A partir do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], o modo de lote é habilitado em cargas de trabalho analíticas qualificadas cujas consultas incluem operações com qualquer tipo de índice (rowstore ou columnstore). Confira [Modo de lote em rowstore](../relational-databases/performance/intelligent-query-processing.md#batch-mode-on-rowstore). |
|Embutimento de UDF escalar|Transforma automaticamente UDFs escalares em expressões relacionais e as insere na consulta SQL chamada. Essa transformação melhora o desempenho de cargas de trabalho que aproveitam as UDFs escalares. Confira [Inlining de UDF escalar](../relational-databases/performance/intelligent-query-processing.md#scalar-udf-inlining).|
|Compilação adiada de variável da tabela|Melhora a qualidade do plano e o desempenho geral para consultas que fazem referência a variáveis de tabela. Durante a otimização e compilação inicial, esse recurso propaga estimativas de cardinalidade com base nas contagens reais de linha de variável de tabela. Essas informações de contagem de linha precisas otimizam as operações de plano de downstream. Confira [Compilação adiada de variável da tabela](../relational-databases/performance/intelligent-query-processing.md#table-variable-deferred-compilation). |
|Processamento de consulta aproximada com `APPROX_COUNT_DISTINCT` |Para cenários em que a precisão absoluta não é importante, mas a capacidade de resposta é crítica, o `APPROX_COUNT_DISTINCT` agrega grandes conjuntos de dados enquanto usa menos recursos do que o `COUNT(DISTINCT())` para uma simultaneidade superior. Confira [Processamento de consulta aproximada](../relational-databases/performance/intelligent-query-processing.md#approximate-query-processing).|
| &nbsp; | &nbsp; |


### <a name="in-memory-database"></a>Banco de dados em memória
As tecnologias de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Banco de Dados em Memória](../relational-databases/in-memory-database.md) aproveitam a inovação de hardware moderna para fornecer escala e desempenho inigualáveis. O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] baseia-se em inovações anteriores nessa área, como OLTP (processamento de transações online) na memória, para aproveitar um novo nível de escalabilidade em todas as cargas de trabalho de banco de dados.  

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Pool de buffers híbrido| Novo recurso do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)], em que as páginas de banco de dados que residem em arquivos de banco de dados colocados em um dispositivo PMEM (memória persistente) serão acessadas diretamente quando necessário. Confira [Pool de buffers híbrido](../database-engine/configure-windows/hybrid-buffer-pool.md).|
|Metadados do TempDB com otimização de memória| O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] apresenta um novo recurso que faz parte da família de recursos do [Banco de dados em memória](../relational-databases/in-memory-database.md), os metadados do TempDB com otimização de memória, que remove de maneira efetiva esse gargalo e possibilita um novo nível de escalabilidade para cargas de trabalho com uso intenso do TempDB. No [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], as tabelas do sistema envolvidas no gerenciamento dos metadados da tabela temporária podem ser movidas para tabelas com otimização de memória não duráveis e livres de travas. Confira [Metadados do TempDB com otimização de memória](../relational-databases/databases/tempdb-database.md#memory-optimized-tempdb-metadata).|
| Suporte a OLTP in-memory para instantâneos de banco de dados | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] apresenta suporte para a criação de [instantâneos do banco de dados](../relational-databases/databases/database-snapshots-sql-server.md) de bancos de dados que incluem grupos de arquivos com otimização de memória. |
| &nbsp; | &nbsp; |

### <a name="intelligent-performance"></a>Desempenho inteligente
O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] baseia-se em inovações de Banco de Dados Inteligente em versões anteriores para garantir que [ela seja executada mais rapidamente](https://docs.microsoft.com/archive/blogs/bobsql/). Esses aprimoramentos ajudam a superar gargalos de recursos conhecidos e fornecem opções para configurar seu servidor de banco de dados para proporcionar desempenho previsível em todas as cargas de trabalho.

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|`OPTIMIZE_FOR_SEQUENTIAL_KEY`|Ativa uma otimização no [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que ajuda a melhorar a taxa de transferência para inserções de alta simultaneidade em um índice. Essa opção destina-se a índices que estão sujeitos a contenção de inserção de última página, que costuma ser vista com os índices que têm uma chave sequencial, tal como uma coluna de identidade, uma sequência ou uma coluna de data/hora. Confira [CREATE INDEX](../t-sql/statements/create-index-transact-sql.md#sequential-keys).|
|Forçar cursores estáticos e de avanço rápido | Fornece suporte à imposição de plano de Repositório de Consultas para cursores de avanço rápido e estáticos. Confira [Planejar forçar suporte para cursores estáticos e de avanço rápido](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md#ctp23).|
|Governança de recursos| O valor configurável para a opção `REQUEST_MAX_MEMORY_GRANT_PERCENT` de `CREATE WORKLOAD GROUP` e `ALTER WORKLOAD GROUP` foi alterado de um inteiro para um tipo de dados float, para permitir um controle mais granular dos limites de memória. Confira [ALTER WORKLOAD GROUP](../t-sql/statements/alter-workload-group-transact-sql.md) e [CREATE WORKLOAD GROUP](../t-sql/statements/create-workload-group-transact-sql.md).|
|Recompilações reduzidas para cargas de trabalho| Melhora o desempenho ao usar tabelas temporárias em vários escopos, reduzindo recompilações desnecessárias. Confira [Recompilações reduzidas para cargas de trabalho](../relational-databases/tables/tables.md#ctp23). |
|Escalabilidade de ponto de verificação indireto |Confira [Escalabilidade de ponto de verificação indireto aprimorada](../relational-databases/logs/database-checkpoints-sql-server.md#ctp23).|
|Atualizações de PFS simultâneas|As [páginas PFS (espaço livre na página)](https://techcommunity.microsoft.com/t5/SQL-Server/Under-the-covers-GAM-SGAM-and-PFS-pages/ba-p/383125) são páginas especiais dentro de um arquivo de banco de dados que o SQL Server usa para ajudar a localizar espaço livre ao alocar espaço para um objeto. A contenção de trava de página em páginas PFS é comumente associada a [TempDB](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d), mas também pode ocorrer em bancos de dados de usuário quando há muitos threads de alocação de objeto simultâneos. Essa melhoria altera a maneira como a simultaneidade é gerenciada com atualizações de PFS para que elas possam ser atualizadas em uma trava compartilhada, em vez de uma trava exclusiva. Esse comportamento é ativado por padrão em todos os bancos de dados (incluindo TempDB) do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] em diante.|
|Migração de trabalho do agendador |A migração de trabalho permite que um agendador ocioso migre uma função de trabalho da fila executável de outro agendador no mesmo nó NUMA e retome imediatamente a tarefa da função de trabalho migrada. Essa melhoria permite um uso de CPU mais equilibrado em situações em que tarefas de longa execução são atribuídas ao mesmo agendador. Confira [Desempenho inteligente do SQL Server 2019 – migração de função de trabalho](https://techcommunity.microsoft.com/t5/SQL-Server/SQL-Server-2019-Intelligent-Performance-Worker-Migration/ba-p/939610) para obter mais informações. |
| &nbsp; | &nbsp; |

### <a name="monitoring"></a>Monitoramento
As melhorias de monitoramento apresentam insights sobre o desempenho sobre qualquer carga de trabalho de banco de dados exatamente quando você precisa.

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|`WAIT_ON_SYNC_STATISTICS_REFRESH` | Um novo tipo de espera em `sys.dm_os_wait_stats` na exibição de gerenciamento dinâmico. Ele mostra o tempo de nível de instância acumulado gasto em operações de atualização de estatísticas síncronas. Confira [`sys.dm_os_wait_stats`](../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md).|
|Política de captura personalizada para o Repositório de Consultas | Quando essa política é habilitada, as configurações adicionais do Repositório de Consultas ficam disponíveis em uma nova configuração de Política de Captura do Repositório de Consultas para ajustar a coleta de dados em um servidor específico. Confira [opções ALTER DATABASE SET](../t-sql/statements/alter-database-transact-sql-set-options.md).|
|`LIGHTWEIGHT_QUERY_PROFILING`| Uma nova configuração no escopo do banco de dados. Confira [`LIGHTWEIGHT_QUERY_PROFILING`](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#lqp). |
|`sys.dm_exec_requests` da coluna `command` | Mostra `SELECT (STATMAN)` se um `SELECT` está aguardando uma operação de atualização de estatísticas síncronas ser concluída antes de continuar a execução da consulta. Confira [`sys.dm_exec_requests`](../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md).|
|`sys.dm_exec_query_plan_stats` | Uma nova DMF (função de gerenciamento dinâmico) que retorna o equivalente do último plano de execução real conhecido para todas as consultas. Confira [sys.dm_exec_query_plan_stats](../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-stats-transact-sql.md).|
|`LAST_QUERY_PLAN_STATS` | Uma nova configuração no escopo do banco de dados que habilita `sys.dm_exec_query_plan_stats`. Veja [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|`query_post_execution_plan_profile` | Um evento estendido que coleta o equivalente a um plano de execução real baseado na criação de perfil leve, diferentemente de `query_post_execution_showplan`, que usa a criação de perfil padrão. Confira [Infraestrutura de criação de perfil de consulta](../relational-databases/performance/query-profiling-infrastructure.md).|
|`sys.dm_db_page_info(database_id, file_id, page_id, mode)` | Um novo DMF que retorna informações sobre uma página em um banco de dados. Confira [sys.dm_db_page_info (Transact-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-page-info-transact-sql.md).|
| &nbsp; | &nbsp; |

## <a name="developer-experience"></a>Experiência do desenvolvedor
O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] continua a proporcionar uma experiência de desenvolvedor de nível mundial com aprimoramentos a tipos de dados espaciais e de grafo, suporte a UTF-8 e uma nova estrutura de extensibilidade que permite aos desenvolvedores usar a linguagem preferida para obter informações sobre todos os dados.

### <a name="graph"></a>Grafo

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Ações de exclusão em cascata de restrição de borda | Agora é possível definir as ações de exclusão em cascata em uma restrição de borda em um banco de dados de grafo. Confira [Restrições de borda](../relational-databases/tables/graph-edge-constraints.md). |
|Nova função do grafo – `SHORTEST_PATH` | Agora é possível usar o `SHORTEST_PATH` dentro de `MATCH` para localizar o caminho mais curto entre quaisquer dois nós em um grafo ou para executar passagens de comprimento arbitrário.|
|Índices e tabelas de partição| As tabelas de grafo agora dão suporte a particionamento de tabela e índice. |
|Usar aliases de exibição ou tabela derivada em consulta de correspondência de grafo |Confira [Consulta de correspondência de grafo](../t-sql/queries/match-sql-graph.md). |
| &nbsp; | &nbsp; |

### <a name="unicode-support"></a>Suporte de Unicode
Dê suporte a empresas em diferentes países e regiões em que o requisito de fornecer aplicativos e serviços de banco de dados multilíngues globais é crítica para atender às demandas dos clientes e cumprir regulamentos de mercado específicos. 

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Suporte para codificação de caracteres UTF-8 |Suporte para UTF-8 para importação e exportação de codificação e como ordenação em nível de coluna ou em nível de banco de dados para dados de cadeia de caracteres. O suporte inclui tabelas externas do PolyBase e Always Encrypted (quando não usado com enclaves). Confira [Suporte a agrupamentos e a Unicode](../relational-databases/collations/collation-and-unicode-support.md).|
| &nbsp; | &nbsp; |

### <a name="language-extensions"></a>Extensões de linguagem

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Novo SDK de linguagem Java | Simplifica o desenvolvimento de programas Java que podem ser executados do SQL Server. Confira [SDK de extensibilidade da Microsoft para Java para SQL Server](../language-extensions/how-to/extensibility-sdk-java-sql-server.md). |
|O SDK da linguagem Java é um software livre |O [SDK de Extensibilidade da Microsoft para Java para Microsoft SQL Server](https://docs.microsoft.com/sql/language-extensions/how-to/extensibility-sdk-java-sql-server) já é software livre e está [disponível no GitHub](https://github.com/microsoft/sql-server-language-extensions).|
|Suporte para tipos de dados Java|Confira [Tipos de dados Java](../language-extensions/how-to/java-to-sql-data-types.md).|
|Novo Java Runtime padrão | O SQL Server agora inclui suporte ao Zulu Embedded for Java da Azul System em todo o produto. Confira [Java com suporte gratuito no SQL Server 2019 agora está disponível](https://cloudblogs.microsoft.com/sqlserver/2019/07/24/free-supported-java-in-sql-server-2019-is-now-available/). |
|Extensões de linguagem do SQL Server| Execute o código externo com a estrutura de extensibilidade. Confira [Extensões de linguagem do SQL Server](https://docs.microsoft.com/sql/language-extensions/language-extensions-overview).
|Registrar linguagens externas|Uma nova DDL (linguagem de definição de dados), `CREATE EXTERNAL LANGUAGE`, registra os linguagens externas, como Java, em SQL Server. Confira [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md). |
| &nbsp; | &nbsp; |

### <a name="spatial"></a>Espacial

|Novo recurso ou atualização | Detalhes |
|:---|:---|
| Novos SRIDs (identificadores de referência espacial) |O [GDA2020 australiano](http://www.ga.gov.au/scientific-topics/positioning-navigation/geodesy/datums-projections/gda2020) fornece uma referência mais robusta e precisa fortemente alinhada a sistemas de posicionamento global. Os novos SRIDs são:<ul><li>7843 para 2D geográfico</li><li>7844 para 3D geográfico</li></ul> Para definições de novos SRIDs, confira a exibição [sys.spatial_reference_systems](../relational-databases/system-catalog-views/sys-spatial-reference-systems-transact-sql.md). |
| &nbsp; | &nbsp; |

### <a name="error-messages"></a>Mensagens de erro
Quando um processo de ETL (extração, transformação e carregamento) falha porque a origem e o destino não têm tipos de dados e/ou comprimento correspondentes, a solução de problemas costumava ser demorada, especialmente em grandes conjuntos de dados. O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] permite informações mais rápidas sobre erros de truncamento de dados.

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Avisos de truncamento detalhados | A mensagem de erro de truncamento de dados inclui por padrão nomes de tabela e coluna, bem como o valor truncado. Confira [VERBOSE_TRUNCATION_WARNINGS](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#verbose-truncation).|
| &nbsp; | &nbsp; |

## <a name="mission-critical-security"></a>Segurança crítica
O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece uma arquitetura de segurança projetada para permitir que administradores de banco de dados e desenvolvedores criem aplicativos de banco de dados e combatam ameaças. Cada versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] foi aprimorada em versões anteriores com a introdução de novos recursos e funcionalidades e o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] continua a desenvolver com base nessa história.

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Always Encrypted com enclaves seguros|Expande sobre Always Encrypted com criptografia in-loco e computações avançadas, habilitando cálculos em dados de texto sem formatação dentro de um enclave seguro no lado do servidor. A criptografia in-loco melhora o desempenho e a confiabilidade das operações de criptografia (criptografia de colunas, chaves de criptografia de colunas giratórias e assim por diante), pois evita a movimentação de dados para fora do banco de dados.<br><br> O suporte para computações avançadas (correspondência de padrões e operações de comparação) desbloqueia o Always Encrypted a um conjunto muito mais amplo de cenários e aplicativos que demandam proteção de dados confidenciais, além de exigir uma funcionalidade mais rica em consultas Transact-SQL. Veja [Always Encrypted com enclaves seguros](../relational-databases/security/encryption/always-encrypted-enclaves.md).|
|Gerenciamento de certificados no SQL Server Configuration Manager|Tarefas de gerenciamento de certificados, como exibir e implantar certificados, agora são possíveis usando o SQL Server Configuration Manager. Confira [Gerenciamento de certificado (SQL Server Configuration Manager)](../database-engine/configure-windows/manage-certificates.md).|
|Descoberta e Classificação de Dados|A Descoberta e Classificação de Dados fornece recursos para classificar e rotular colunas em tabelas de usuário. A classificação dos dados confidenciais (de negócios, financeiros, de serviços de saúde, PII, etc.) pode desempenhar um papel fundamental na dimensão da proteção de informações organizacionais. Esse recurso pode funcionar como a infraestrutura para:<ul><li>ajudar a atender a padrões de privacidade de dados e requisitos de conformidade regulamentar</li><li>Vários cenários de segurança, como monitoramento (auditoria) e alerta sobre acesso anômalo a dados confidenciais</li><li>facilitar a identificação de onde os dados confidenciais residem na empresa, para que os administradores possam adotar as etapas corretas para proteger o banco de dados</li></ul>|
|Auditoria do SQL Server|A [Auditoria](../relational-databases/security/auditing/sql-server-audit-database-engine.md) também foi aprimorada para incluir um novo campo `data_sensitivity_information` no registro do log de auditoria, que contém as classificações (rótulos) de confidencialidade dos dados reais retornados pela consulta. Confira detalhes e exemplos em [`ADD SENSITIVITY CLASSIFICATION`](../t-sql/statements/add-sensitivity-classification-transact-sql.md).|
| &nbsp; | &nbsp; |

## <a name="high-availability"></a>Alta disponibilidade
Uma tarefa comum que todos que implantam o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] precisam considerar é garantir que todas as instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] críticas e os bancos de dados dentro delas estejam disponíveis sempre que os usuários empresariais e finais precisarem delas. A disponibilidade é o principal pilar da plataforma [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], e o [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduz muitos novos recursos e aprimoramentos que permitem às empresas garantir a alta disponibilidade de seus ambientes de banco de dados.

### <a name="availability-groups"></a>Grupos de Disponibilidade

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Até cinco réplicas síncronas|[!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] aumenta o número máximo de réplicas síncronas para 5, um aumento com relação às 3 no [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Você pode configurar esse grupo de cinco réplicas para ter failover automático dentro do grupo. Há uma réplica primária, além de quatro réplicas secundárias síncronas.|
|Redirecionamento de conexão de réplica secundária para primária| Permite que conexões do aplicativo cliente sejam direcionadas para a réplica primária, independentemente do servidor de destino especificado na cadeia de conexão. Para conhecer os detalhes, consulte [Secondary to primary replica read/write connection redirection (Always On Availability Groups)](../database-engine/availability-groups/windows/secondary-replica-connection-redirection-always-on-availability-groups.md) (Redirecionamento de conexão de leitura/gravação de réplica secundária para primária [Grupos de Disponibilidade Always On]).|
|Benefícios do HADR| Cada cliente do Software Assurance do SQL Server poderá usar três benefícios aprimorados para qualquer versão do SQL Server que ainda tenha suporte da Microsoft. Para obter detalhes, confira [nosso comunicado aqui.](https://cloudblogs.microsoft.com/sqlserver/2019/10/30/new-high-availability-and-disaster-recovery-benefits-for-sql-server/)
| &nbsp; | &nbsp; |

### <a name="recovery"></a>Recuperação

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Recuperação de banco de dados acelerada | Reduza o tempo de recuperação após uma reinicialização ou uma reversão de transação de execução longa com a ADR (recuperação de banco de dados acelerada). Confira [Recuperação acelerada de banco de dados](../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#adr).|
| &nbsp; | &nbsp; |

### <a name="resumable-operations"></a>Operações retomáveis

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Compilar e recompilar o índice de columnstore em cluster online | Confira [Executar operações de índice online](../relational-databases/indexes/perform-index-operations-online.md). |
|Compilar o índice de rowstore online retomável | Confira [Executar operações de índice online](../relational-databases/indexes/perform-index-operations-online.md). |
|Suspender e retomar a verificação inicial para TDE (Transparent Data Encryption)|Confira [Verificação de TDE (Transparent Data Encryption) – suspender e retomar](../relational-databases/security/encryption/transparent-data-encryption.md#scan-suspend-resume).|
| &nbsp; | &nbsp; |

## <a name="platform-choice"></a>Opção de plataforma
O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] baseia-se nas inovações introduzidas no [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] para permitir que você execute [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em sua plataforma preferida com ainda mais funcionalidade e segurança.

### <a name="linux"></a><a id="sql-server-on-linux"></a>Linux

| Novo recurso ou atualização | Detalhes |
|:-----|:-----|
|Suporte para replicação | Confira [Replicação do SQL Server no Linux](../linux/sql-server-linux-replication.md). |
|Suporte para MSDTC (Coordenador de Transações Distribuídas da Microsoft) | Configura [Como configurar o MSDTC no Linux](../linux/sql-server-linux-configure-msdtc.md). |
|Suporte para OpenLDAP para provedores de AD de terceiros | Confira o [Tutorial: Use a autenticação do Active Directory com o SQL Server em Linux](../linux/sql-server-linux-active-directory-authentication.md). |
|Serviços de Machine Learning no Linux | Confira [Instalar Serviços de Machine Learning do SQL Server (R e Python) no Linux](../linux/sql-server-linux-setup-machine-learning.md). |
|Aprimoramentos do TempDB | Por padrão, uma nova instalação do SQL Server em Linux cria vários arquivos de dados TempDB com base no número de núcleos lógicos (com até oito arquivos de dados). Isso não é aplicável a upgrades de versões principais ou secundárias no local. Cada arquivo do TempDB tem 8 MB com um aumento automático de 64 MB. Esse comportamento é semelhante à instalação padrão do SQL Server no Windows. |
|PolyBase em Linux | Confira [Instalar o PolyBase](../relational-databases/polybase/polybase-linux-setup.md) no Linux para conectores não Hadoop.<br/><br/>Confira [Mapeamento de tipo do PolyBase](../relational-databases/polybase/polybase-type-mapping.md). |
| Suporte ao CDC (captura de dados de alterações) | A CDA (captura de dados de alterações) agora é compatível no Linux para [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. |
| &nbsp; | &nbsp; |

### <a name="containers"></a>Contêineres
A maneira mais fácil de começar a trabalhar com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é usar contêineres. O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] baseia-se nas inovações introduzidas em versões anteriores para permitir que você implante contêineres [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em novas plataformas de maneira mais segura e com mais funcionalidade.

|Novo recurso ou atualização | Detalhes |
|:---|:---|
| Registro de Contêiner da Microsoft | O [Registro de Contêiner da Microsoft](https://azure.microsoft.com/blog/microsoft-syndicates-container-catalog/) agora substitui o Docker Hub para novas imagens oficiais de contêiner da Microsoft, incluindo [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]. |
| Contêineres não raiz | [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] introduz a capacidade de criar contêineres mais seguros, iniciando o processo [!INCLUDE[sql-server](../includes/ssnoversion-md.md)] como um usuário não raiz por padrão. Confira [compilar e executar contêineres do SQL Server como um usuário não raiz](../linux/sql-server-linux-configure-docker.md#buildnonrootcontainer). |
| Imagens de contêiner certificadas do Red Hat | Do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] em diante, você pode executar contêineres do SQL Server no Red Hat Enterprise Linux. |
| Suporte para PolyBase e Machine Learning| O [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] apresenta novas maneiras de trabalhar com contêineres do SQL Server, como Serviços de Machine Learning e PolyBase. Confira alguns exemplos no [SQL Server no repositório GitHub do contêiner](https://github.com/microsoft/mssql-docker/tree/master/linux/preview/examples). |
| &nbsp; | &nbsp; |

## <a name="setup-options"></a>Opções de instalação

|Novo recurso ou atualização | Detalhes |
|:---|:---| 
|Novas opções de configuração de memória | Define durante a instalação as configurações de servidor de *memória mínima do servidor (MB)* e *memória máxima do servidor (MB)* . Confira a [página Configuração do mecanismo de banco de dados – memória](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#memory) e os parâmetros `USESQLRECOMMENDEDMEMORYLIMITS`, `SQLMINMEMORY` e `SQLMAXMEMORY` em [Instalar o SQL Server do prompt de comando](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install). O valor proposto está alinhado com as diretrizes de configuração de memória nas [Opções de configuração de memória do servidor](../database-engine/configure-windows/server-memory-server-configuration-options.md#manually).| 
|Novas opções de configuração de paralelismo | Define o *grau máximo de configuração de* servidor de paralelismo durante a instalação. Confira a [página Configuração do mecanismo de banco de dados – MaxDOP](https://docs.microsoft.com/sql/sql-server/install/instance-configuration?view=sql-server-ver15#maxdop) e o parâmetro `SQLMAXDOP` em [Instalar SQL Server no prompt de comando](../database-engine/install-windows/install-sql-server-from-the-command-prompt.md#Install). O valor padrão está alinhado às diretrizes de grau máximo da opção de paralelismo especificadas em [Configurar a opção de configuração de servidor grau máximo de paralelismo](../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines).| 
|Aviso de instalação na chave do produto (Product Key) da licença do servidor/CAL|Se uma chave do produto (Product Key) de licença de servidor corporativo/CAL for inserida e o computador tiver mais que 20 núcleos físicos ou 40 núcleos lógicos quando o Hyper-Threading estiver habilitado, será exibido um aviso durante a instalação. Os usuários ainda podem reconhecer a limitação e continuar a instalação ou podem inserir uma Chave de Licença que dê suporte ao número máximo de processadores do sistema operacional.|
| &nbsp; | &nbsp; |

## <a name="sql-server-machine-learning-services"></a><a id="ml"></a> Serviços de Machine Learning do SQL Server

|Novo recurso ou atualização | Detalhes |
|:---|:---|
|Modelagem baseada em partição | Processe scripts externos por partição de seus dados usando os novos parâmetros adicionados ao `sp_execute_external_script`. Essa funcionalidade dá suporte ao treinamento de muitos modelos pequenos (um modelo para cada partição de dados) em vez de um modelo grande. Confira [Criar modelos baseados em partição](../machine-learning/tutorials/r-tutorial-create-models-per-partition.md).|
|Cluster de failover do Windows Server| Configure alta disponibilidade para Serviços de Machine Learning em um Cluster de failover do Windows Server.|
| &nbsp; | &nbsp; |

## <a name="sql-server-analysis-services"></a>SQL Server Analysis Services

Esta versão apresenta novos recursos e aprimoramentos para desempenho, governança de recursos e suporte ao cliente.

| Novo recurso ou atualização | Detalhes |
|:---|:---|
|Grupos de cálculo em modelos tabulares| Os grupos de cálculo podem reduzir significativamente o número de medidas redundantes agrupando expressões de medida comuns como *itens de cálculo*. Para saber mais, confira [Grupos de cálculo no modelo tabular](/analysis-services/tabular-models/calculation-groups). |
|Intercalação de consulta| A intercalação de consulta é uma configuração do sistema no modo tabular que pode melhorar os tempos de resposta de consulta do usuário em cenários de alta simultaneidade. Para saber mais, confira [Intercalação de consulta](/analysis-services/tabular-models/query-interleaving). |
|Relações muitos para muitos em modelos tabulares| Permite relações muitos para muitos entre tabelas em que ambas as colunas não são exclusivas. Para saber mais, confira [Relações de modelos tabulares](/analysis-services/tabular-models/relationships-ssas-tabular).|
|Configurações de propriedade para governança de recursos| Esta versão inclui novas configurações de memória: Memory\QueryMemoryLimit, DbpropMsmdRequestMemoryLimit e OLAP\Query\RowsetSerializationLimit para governança de recurso. Para saber mais, confira [Configurações de memória](/analysis-services/server-properties/memory-properties).|
|Configuração de governança para atualizações de cache do Power BI | Esta versão apresenta a propriedade ClientCacheRefreshPolicy, que substitui os dados de bloco do painel de cache e dados de relatório para o carregamento inicial de relatórios do Live Connect pelo serviço do Power BI. Para saber mais, confira [Propriedades gerais](/analysis-services/server-properties/general-properties). |
| Anexação online  | A anexação online pode ser usada para sincronização de réplicas somente leitura em ambientes de expansão de consulta local. Para saber mais, confira [Anexação online](/analysis-services/what-s-new-in-sql-server-analysis-services#online-attach). |
| &nbsp; | &nbsp; |

## <a name="sql-server-integration-services"></a>SQL Server Integration Services

Esta versão apresenta novos recursos para melhorar operações de arquivo.

| Novo recurso ou atualização | Detalhes |
|:---|:---|
|Tarefa de arquivo flexível |Execute operações de arquivo no Sistema de Arquivos Local, no Armazenamento de Blobs do Azure e no Azure Data Lake Storage Gen2. Confira [Tarefa Arquivo Flexível](../integration-services/control-flow/flexible-file-task.md).|
|Origem e destino de arquivo flexível |Leia e grave dados para o Armazenamento de Blobs do Azure e o Azure Data Lake Storage Gen2. Confira [Origem de Arquivo Flexível](../integration-services/data-flow/flexible-file-source.md) e [Destino de Arquivo Flexível](../integration-services/data-flow/flexible-file-destination.md). |

## <a name="sql-server-master-data-services"></a>SQL Server [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]

| Novo recurso ou atualização | Detalhes |
|:---|:---|
|Suporte para bancos de dados da Instância Gerenciada de SQL do Azure| Hospede o [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)] na Instância Gerenciada de SQL do Azure. Confira [Instalação e configuração do [!INCLUDE[master-data-services](../includes/ssmdsshort-md.md)]](../master-data-services/master-data-services-installation-and-configuration.md#SetUpWeb).|
|Novos controles HTML| Os controles HTML substituem todos os componentes do Silverlight anteriores. Dependência do Silverlight removida.|
| &nbsp; | &nbsp; |

## <a name="sql-server-reporting-services"></a>SQL Server Reporting Services

Esta versão do SQL Server Reporting Services dá suporte a instâncias gerenciadas do Azure SQL, a conjuntos de dados do Power BI Premium, a acessibilidade aprimorada, ao Proxy de Aplicativo do Azure Active Directory e a Criptografia de Banco de Dados Transparente. Também traz uma atualização para o Construtor de Relatórios da Microsoft. Confira [Novidades do SSRS (SQL Server Reporting Services)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md) para obter detalhes.

## <a name="see-also"></a>Confira também

- [`SqlServer` Módulo do PowerShell](https://www.powershellgallery.com/packages/Sqlserver)
- [Documentação do SQL Server PowerShell](../powershell/sql-server-powershell.md)

## <a name="next-steps"></a>Próximas etapas

- [Workshops do SQL Server](https://aka.ms/sqlworkshops)
- [Notas sobre a versão do [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](sql-server-version-15-release-notes.md)
- [Microsoft [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]: White paper técnico](https://aka.ms/sql2019whitepaper)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
