---
title: Visão geral e cenários de uso | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 62c964c5-eae4-4cf1-9024-d5a19adbd652
caps.latest.revision: 5
author: jodebrui
ms.author: jodebrui
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: defc260673b6dd9a2170c154ca35730ec5bb4309
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983348"
---
# <a name="overview-and-usage-scenarios"></a>Visão geral e cenários de uso
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

O OLTP in-memory é a principal tecnologia disponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] para otimizar o desempenho do processamento de transações, ingestão de dados, carregamento de dados e cenários de dados transitórios. Este artigo inclui uma visão geral da tecnologia e descreve os cenários de uso do OLTP in-memory. Use essas informações para determinar se o OLTP in-memory é adequado para seu aplicativo. O artigo termina com um exemplo que mostra objetos OLTP in-memory, referências a uma demonstração de desempenho e a recursos que você pode usar para as próximas etapas.

Este artigo aborda a tecnologia OLTP in-memory no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. A seguinte postagem no blog contém um aprofundamento dos benefícios de desempenho e de utilização de recursos no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]: 
- [OLTP in-memory no Banco de Dados SQL do Azure](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

## <a name="in-memory-oltp-overview"></a>Visão geral do OLTP in-memory

O OLTP in-memory pode fornecer excelentes ganhos de desempenho para as cargas de trabalho corretas. Um cliente, a bwin, conseguiu [atingir 1,2 milhão de solicitações por segundo](https://blogs.msdn.microsoft.com/sqlcat/2016/10/26/how-bwin-is-using-sql-server-2016-in-memory-oltp-to-achieve-unprecedented-performance-and-scale/) com um único computador executando o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], aproveitando o OLTP in-memory. Outro cliente, a Quorum, conseguiu dobrar sua carga de trabalho, [reduzindo a utilização de recursos em 70%](https://customers.microsoft.com/en-US/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database), aproveitando o OLTP in-memory no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Os clientes observaram até 30 vezes de ganho de desempenho em alguns casos. O quanto de ganho você terá depende da carga de trabalho.

De onde vem esse ganho de desempenho? Em essência, o OLTP in-memory melhora o desempenho de processamento, tornando a execução de transações e o acesso aos dados mais eficaz, removendo a contenção de bloqueio e de trava entre transações em execução simultânea: não é rápido porque ele está na memória. é rápido porque ele é otimizado em torno de dados na memória. Os algoritmos de processamento, o acesso e o armazenamento de dados foram reprojetados desde o início para tirar proveito dos aprimoramentos mais recentes da computação na memória e de alta simultaneidade.

Só porque os dados residem na memória não significa que você os perde quando há uma falha. Por padrão, todas as transações são completamente duráveis, o que significa que você tem as mesmas garantias de durabilidade de qualquer outra tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: como parte da confirmação da transação, todas as alterações são gravadas no log de transações em disco. Se houver uma falha a qualquer momento depois que a transação seja confirmada, seus dados estarão lá quando o banco de dados ficar online novamente. Além disso, o OLTP in-memory funciona com todas as funcionalidades de alta disponibilidade e recuperação de desastre do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como Always On, backup/restauração, etc.

Para aproveitar o OLTP in-memory no banco de dados, você pode usar um ou mais dos seguintes tipos de objetos:

- *Tabelas com otimização de memória* são usadas para armazenar dados do usuário. Você declara uma tabela com otimização de memória no momento da criação.
- *Tabelas não duráveis* são usadas para dados transitórios, para armazenar em cache ou para conjuntos de resultados intermediários (substituindo tabelas temporárias tradicionais). Uma tabela não durável é uma tabela com otimização de memória que é declarada com DURABILITY=SCHEMA_ONLY, o que significa que as alterações nessas tabelas não incorrerão em nenhuma E/S. Isso evita o consumo de recursos de E/S de log para casos em que a durabilidade não é uma preocupação.
- *Tipos de tabela com otimização de memória* são usados para parâmetros com valor de tabela (TVPs), bem como conjuntos de resultados intermediários em procedimentos armazenados. Eles podem ser usados em vez de tipos de tabela tradicionais. Variáveis de tabela e TVPs que são declarados usando um tipo de tabela com otimização de memória herdam os benefícios de tabelas com otimização de memória não duráveis: acesso a dados eficiente e nenhuma E/S.
- *Módulos T-SQL compilados nativamente* são usados para reduzir ainda mais o tempo necessário para uma transação individual, reduzindo os ciclos de CPU necessários para processar as operações. Você declara um módulo Transact-SQL para ser compilado nativamente no momento da criação. No momento, os seguintes módulos T-SQL podem ser compilados nativamente: procedimentos armazenados, gatilhos e funções escalares definidas pelo usuário.

O OLTP in-memory é integrado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Além disso, como esses objetos se comportam de forma semelhante a seus equivalentes tradicionais, você geralmente pode obter benefícios de desempenho fazendo somente alterações mínimas no banco de dados e no aplicativo. Além disso, você pode ter tabelas com otimização de memória e tabelas tradicionais baseadas em disco no mesmo banco de dados, e executar consultas entre as duas. Encontre um script Transact-SQL mostrando um exemplo de cada um desses tipos de objetos ao final deste artigo.

## <a name="usage-scenarios-for-in-memory-oltp"></a>Cenários de uso do OLTP in-memory

O OLTP in-memory não é um botão de aceleração mágico e não é adequado para todas as cargas de trabalho. Por exemplo, as tabelas com otimização de memória não diminuirão a utilização da CPU se a maioria das consultas estiver fazendo agregação em intervalos de dados grandes – os índices Columnstore ajudam nesse cenário.

Aqui está uma lista de cenários e padrões de aplicativo em que temos visto os clientes serem bem-sucedidos com o OLTP in-memory.

### <a name="high-throughput-and-low-latency-transaction-processing"></a>Processamento de transações de baixa latência e alta taxa de transferência

Este é o cenário principal para o qual criamos o OLTP in-memory: suporte a grandes volumes de transações, com baixa latência consistente para transações individuais.

Cenários comuns de carga de trabalho são: troca de instrumentos financeiros, apostas esportivas, jogos móveis e entrega de anúncios. Outro padrão comum que vimos é um "catálogo" que é frequentemente lido e/ou atualizado. Um exemplo é quando você tem arquivos grandes, distribuídos ao longo de alguns nós de cluster e cataloga o local de cada fragmento de cada arquivo em uma tabela com otimização de memória.

#### <a name="implementation-considerations"></a>Considerações sobre implementação

Use tabelas com otimização de memória para suas tabelas de transação principal, ou seja, as tabelas com as transações de desempenho crítico. Use procedimentos armazenados compilados nativamente para otimizar a execução da lógica associada à transação comercial. Quanto mais da lógica você inserir em procedimentos armazenados no banco de dados, mais benefícios obterá do OLTP in-memory.

Para começar a usar em um aplicativo existente:
1. Use o [relatório de análise de desempenho de transação](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) para identificar os objetos que você deseja migrar, 
2. e use a [otimização de memória](memory-optimization-advisor.md) e consultores de [compilação nativa](native-compilation-advisor.md) para ajudar na migração.

#### <a name="customer-case-studies"></a>Estudos de caso de cliente

- O CMC Markets utiliza o OLTP in-memory no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] para conseguir baixa latência consistente: [como um segundo é muito tempo de espera, essa empresa de serviços financeiros está atualizando seu software comercial agora.](https://customers.microsoft.com/en-us/story/because-a-second-is-too-long-to-wait-this-financial-services-firm-is-updating-its-trading-software)
- A Derivco utiliza o OLTP in-memory no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] para dar suporte a uma maior taxa de transferência e lidar com picos na carga de trabalho: [quando uma empresa de jogos online não quer correr risco, ela aposta no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)].](https://customers.microsoft.com/en-us/story/when-an-online-gaming-company-doesnt-want-to-risk-its-future-it-bets-on-sql-server-2016)


### <a name="data-ingestion-including-iot-internet-of-things"></a>Ingestão de dados, incluindo a IoT (Internet das coisas)

O OLTP in-memory é bom na ingestão de grandes volumes de dados de várias fontes diferentes ao mesmo tempo. Além disso, geralmente, é útil ingerir dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em comparação com outros destinos, pois o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agiliza a execução de consultas nos dados e permite que você obtenha insights em tempo real.

Os padrões comuns de aplicativo são: 
-  Ingestão de eventos e leituras do sensor e permissão de notificações, bem como da análise histórica. 
-  Gerenciamento de atualizações em lotes, até mesmo de várias fontes, minimizando o impacto sobre a carga de trabalho de leitura simultânea.

#### <a name="implementation-considerations"></a>Considerações sobre implementação

Use uma tabela com otimização de memória para a ingestão de dados. Se a ingestão consistir principalmente de inserções (em vez de atualizações) e o espaço de armazenamento do OLTP in-memory dos dados for uma preocupação,

- use um trabalho para a descarga em lotes regular de dados em uma tabela baseada em disco com um [índice Columnstore clusterizado](../indexes/columnstore-indexes-overview.md), usando um trabalho que faz `INSERT INTO <disk-based table> SELECT FROM <memory-optimized table>`; ou
- use uma [tabela com otimização de memória temporária](../tables/system-versioned-temporal-tables-with-memory-optimized-tables.md) para gerenciar dados históricos. Neste modo, os dados históricos residem no disco e a movimentação de dados é gerenciada pelo sistema.

O repositório de amostras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém um aplicativo de grade inteligente que usa uma tabela com otimização de memória temporária, um tipo de tabela com otimização de memória e um procedimento armazenado compilado nativamente, para agilizar a ingestão de dados e ao mesmo tempo gerenciar a superfície de armazenamento do OLTP in-memory dos dados do sensor: 

 - [smart-grid-release](https://github.com/Microsoft/sql-server-samples/releases/tag/iot-smart-grid-v1.0) 
 - [smart-grid-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/applications/iot-smart-grid)
 
#### <a name="customer-case-studies"></a>Estudos de caso de cliente

- [A Quorum dobra a carga de trabalho principal do banco de dados, reduzindo a utilização em 70%, aproveitando o OLTP in-memory no Banco de Dados SQL do Azure](http://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)
- A EdgeNet melhorou o desempenho do carregamento de dados em lote e eliminou a necessidade de manter um cache de camada intermediária, com o OLTP in-memory no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]: [uma empresa de serviços de dados obtém acesso em tempo real aos dados de produtos com a tecnologia in-memory](https://customers.microsoft.com/en-us/story/data-services-firm-gains-real-time-access-to-product-d)
- O Beth Israel Deaconess Medical Center conseguiu melhorar de forma significativa a taxa de ingestão de dados de controladores de domínio e lidar com picos na carga de trabalho, com o OLTP In-Memory no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]: [https://customers.microsoft.com/en-us/story/strengthening-data-security-and-creating-more-time-for]

### <a name="caching-and-session-state"></a>Estado de sessão e cache

A tecnologia OLTP in-memory torna o SQL realmente atraente para manter o estado de sessão (por exemplo, para um aplicativo ASP.NET) e para o cache.

O estado de sessão do ASP.NET é um caso de uso muito bem-sucedido do OLTP in-memory. Com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um cliente estava prestes a atingir 1,2 milhão de solicitações por segundo. Enquanto isso, eles começaram a usar o OLTP in-memory para fins de armazenamento em cache de todos os aplicativos de camada intermediária na empresa. Detalhes: [como a bwin está usando o OLTP in-memory do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] para atingir um desempenho e uma escala sem precedentes](https://blogs.msdn.microsoft.com/sqlcat/2016/10/26/how-bwin-is-using-sql-server-2016-in-memory-oltp-to-achieve-unprecedented-performance-and-scale/)

#### <a name="implementation-considerations"></a>Considerações sobre implementação

Você pode usar tabelas não duráveis com otimização de memória como um repositório de chave-valor simples armazenando um BLOB em uma coluna varbinary(max). Como alternativa, implemente um cache semiestruturado com [suporte a JSON](https://azure.microsoft.com/blog/json-support-is-generally-available-in-azure-sql-database/) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Por fim, você pode criar um cache relacional completo por meio de tabelas não duráveis com um esquema relacional completo, incluindo vários tipos de dados e restrições.

Comece a usar o estado de sessão do ASP.NET com otimização de memória, aproveitando os scripts publicados no GitHub para substituir os objetos criados pelo provedor de estado de sessão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interno:

- [aspnet-session-state](https://github.com/Microsoft/sql-server-samples/tree/master/samples/applications/aspnet-session-state)

#### <a name="customer-case-studies"></a>Estudos de caso de cliente

- A bwin conseguiu aumentar consideravelmente a taxa de transferência e reduzir a superfície de hardware do estado de sessão do ASP.NET com o OLTP in-memory no [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]: [um site de jogos pode aumentar para 250.000 solicitações por segundo e melhorar a experiência do jogador](https://customers.microsoft.com/en-us/story/gaming-site-can-scale-to-250000-requests-per-second-an)
- A bwin aumentou a taxa de transferência com o estado de sessão do ASP.NET e implementou um sistema de cache intermediário em toda a empresa com o OLTP in-memory no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]: [como a bwin está usando o OLTP in-memory do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] para atingir um desempenho e uma escala sem precedentes](https://blogs.msdn.microsoft.com/sqlcat/2016/10/26/how-bwin-is-using-sql-server-2016-in-memory-oltp-to-achieve-unprecedented-performance-and-scale/)

### <a name="tempdb-object-replacement"></a>Substituição de objeto tempdb

Aproveite as tabelas não duráveis e os tipos de tabela com otimização de memória para substituir as estruturas tradicionais baseadas no TempDB, como tabelas temporárias, variáveis de tabela e TVPs (parâmetros com valor de tabela).

Variáveis de tabela com otimização de memória e tabelas não duráveis normalmente reduzem a CPU e removem completamente a E/S de log, em comparação a variáveis de tabela tradicionais e à tabela #temp.

#### <a name="implementation-considerations"></a>Considerações sobre implementação

Para começar, veja: [Melhorando o desempenho da tabela temporária e da variável de tabela usando a otimização de memória.](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)

#### <a name="customer-case-studies"></a>Estudos de caso de cliente

- Um cliente foi capaz de melhorar o desempenho em 40%, simplesmente substituindo TVPs tradicionais por TVPs com otimização de memória: [ingestão de dados IoT de alta velocidade usando o OLTP in-memory no Azure](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/04/07/a-technical-case-study-high-speed-iot-data-ingestion-using-in-memory-oltp-in-azure/)

### <a name="etl-extract-transform-load"></a>ETL (Extrair, Transformar e Carregar)

Fluxos de trabalho ETL normalmente incluem o carregamento de dados em uma tabela de preparo, transformações de dados e carregamento nas tabelas finais.

#### <a name="implementation-considerations"></a>Considerações sobre implementação

Use tabelas com otimização de memória não duráveis para a preparação de dados. Elas removem completamente toda E/S e tornam o acesso aos dados mais eficiente.

Caso realize transformações na tabela de preparo como parte do fluxo de trabalho, você poderá usar procedimentos armazenados compilados nativamente para acelerar essas transformações. Caso possa fazer essas transformações em paralelo, você obterá benefícios adicionais de dimensionamento da otimização de memória.

## <a name="sample-script"></a>Exemplo de Script

Antes de começar a usar o OLTP in-memory, você precisa criar um grupo de arquivos MEMORY_OPTIMIZED_DATA. Além disso, recomendamos o uso do nível de compatibilidade do banco de dados 130 (ou superior) e a definição da opção de banco de dados MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT como ON.

Você pode usar o script que se encontra no local a seguir para criar o grupo de arquivos na pasta de dados padrão e definir as configurações recomendadas:

- [enable-in-memory-oltp.sql](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)

O script a seguir ilustra os objetos OLTP in-memory que você pode criar no banco de dados:

```sql
-- configure recommended DB option
ALTER DATABASE CURRENT SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON
GO
-- memory-optimized table
CREATE TABLE dbo.table1
( c1 INT IDENTITY PRIMARY KEY NONCLUSTERED,
  c2 NVARCHAR(MAX))
WITH (MEMORY_OPTIMIZED=ON)
GO
-- non-durable table
CREATE TABLE dbo.temp_table1
( c1 INT IDENTITY PRIMARY KEY NONCLUSTERED,
  c2 NVARCHAR(MAX))
WITH (MEMORY_OPTIMIZED=ON,
      DURABILITY=SCHEMA_ONLY)
GO
-- memory-optimized table type
CREATE TYPE dbo.tt_table1 AS TABLE
( c1 INT IDENTITY,
  c2 NVARCHAR(MAX),
  is_transient BIT NOT NULL DEFAULT (0),
  INDEX ix_c1 HASH (c1) WITH (BUCKET_COUNT=1024))
WITH (MEMORY_OPTIMIZED=ON)
GO
-- natively compiled stored procedure
CREATE PROCEDURE dbo.usp_ingest_table1
  @table1 dbo.tt_table1 READONLY
WITH NATIVE_COMPILATION, SCHEMABINDING
AS
BEGIN ATOMIC
    WITH (TRANSACTION ISOLATION LEVEL=SNAPSHOT,
          LANGUAGE=N'us_english')

  DECLARE @i INT = 1

  WHILE @i > 0
  BEGIN
    INSERT dbo.table1
    SELECT c2
    FROM @table1
    WHERE c1 = @i AND is_transient=0

    IF @@ROWCOUNT > 0
      SET @i += 1
    ELSE
    BEGIN
      INSERT dbo.temp_table1
      SELECT c2
      FROM @table1
      WHERE c1 = @i AND is_transient=1

      IF @@ROWCOUNT > 0
        SET @i += 1
      ELSE
        SET @i = 0
    END
  END

END
GO
-- sample execution of the proc
DECLARE @table1 dbo.tt_table1
INSERT @table1 (c2, is_transient) VALUES (N'sample durable', 0)
INSERT @table1 (c2, is_transient) VALUES (N'sample non-durable', 1)
EXECUTE dbo.usp_ingest_table1 @table1=@table1
SELECT c1, c2 from dbo.table1
SELECT c1, c2 from dbo.temp_table1
GO
```   

## <a name="resources-to-learn-more"></a>Recursos para saber mais:

[Tecnologias OLTP in-memory para um desempenho mais rápido do T-SQL](http://msdn.microsoft.com/library/mt694156.aspx)   
Encontre uma demonstração de desempenho usando o OLTP in-memory em: [in-memory-oltp-perf-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)   
[Vídeo de 17 minutos explicando o OLTP in-memory e apresentando a demonstração](https://www.youtube.com/watch?v=l5l5eophmK4) (a demonstração está em 8:25)   
[Script para habilitar o OLTP in-memory e definir as opções recomendadas](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/enable-in-memory-oltp.sql)   
[Documentação principal do OLTP in-memory](in-memory-oltp-in-memory-optimization.md)   
[Benefícios de desempenho e de utilização de recursos do OLTP in-memory no Banco de Dados SQL do Azure](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)  
[Melhorando o desempenho da tabela temporária e da variável de tabela usando a otimização de memória](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/21/improving-temp-table-and-table-variable-performance-using-memory-optimization/)   
[Otimizar o desempenho usando tecnologias in-memory no Banco de Dados SQL](https://docs.microsoft.com/azure/sql-database/sql-database-in-memory)  
[Tabelas temporais com controle da versão do sistema com tabelas com otimização de memória](../tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)  
[OLTP in-memory – Padrões comuns de carga de trabalho e considerações de migração](http://msdn.microsoft.com/library/dn673538.aspx). 
