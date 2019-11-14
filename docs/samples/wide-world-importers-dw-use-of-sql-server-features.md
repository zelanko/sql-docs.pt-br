---
title: Principais recursos no banco de dados DW WideWorldImporters
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 08/04/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: dfce2ce4a6f13a25687d668268f532893c1404e0
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056289"
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>WideWorldImportersDW o uso de recursos e funcionalidades do SQL Server
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
O WideWorldImportersDW foi projetado para demonstrar muitos dos principais recursos do SQL Server que são adequados para data warehousing e análise. Veja a seguir uma lista de recursos e funcionalidades do SQL Server e uma descrição de como eles são usados no WideWorldImportersDW.

## <a name="polybase"></a>PolyBase

[Aplica-se a SQL Server (2016 e posterior)]

O polybase é usado para combinar informações de vendas do WideWorldImportersDW com um conjunto de dados públicos sobre os demográficos para entender quais cidades podem ser de interesse para uma expansão mais detalhada das vendas.

Para habilitar o uso do polybase no banco de dados de exemplo, verifique se ele está instalado e execute o seguinte procedimento armazenado no banco de dados:

    EXEC [Application].[Configuration_ApplyPolyBase]

Isso criará uma tabela externa `dbo.CityPopulationStatistics` que faz referência a um conjunto de dados público que contém dados de população para cidades na Estados Unidos, hospedados no armazenamento de BLOBs do Azure. Você é incentivado a examinar o código no procedimento armazenado para entender o processo de configuração. Se você quiser hospedar seus próprios dados no armazenamento de BLOBs do Azure e mantê-los protegidos do acesso público geral, será necessário realizar etapas de configuração adicionais. A consulta a seguir retorna os dados desse conjunto de dados externos:

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

Para entender quais cidades podem ser de interesse para expansão adicional, a consulta a seguir analisa a taxa de crescimento das cidades e retorna as 100 maiores cidades com crescimento significativo e onde a Wide World Importers não tem uma presença de vendas. A consulta envolve uma junção entre a tabela remota `dbo.CityPopulationStatistics` e a tabela local `Dimension.City`e um filtro que envolve a tabela local `Fact.Sales`.

    WITH PotentialCities
    AS
    (
        SELECT cps.CityName,
               cps.StateProvinceCode,
               MAX(cps.LatestRecordedPopulation) AS PopulationIn2016,
               (MAX(cps.LatestRecordedPopulation) - MIN(cps.LatestRecordedPopulation)) * 100.0
                   / MIN(cps.LatestRecordedPopulation) AS GrowthRate
        FROM dbo.CityPopulationStatistics AS cps
        WHERE cps.LatestRecordedPopulation IS NOT NULL
        AND cps.LatestRecordedPopulation <> 0
        GROUP BY cps.CityName, cps.StateProvinceCode
    ),
    InterestingCities
    AS
    (
        SELECT DISTINCT pc.CityName,
                        pc.StateProvinceCode,
                        pc.PopulationIn2016,
                        FLOOR(pc.GrowthRate) AS GrowthRate
        FROM PotentialCities AS pc
        INNER JOIN Dimension.City AS c
        ON pc.CityName = c.City
        WHERE GrowthRate > 2.0
        AND NOT EXISTS (SELECT 1 FROM Fact.Sale AS s WHERE s.[City Key] = c.[City Key])
    )
    SELECT TOP(100) CityName, StateProvinceCode, PopulationIn2016, GrowthRate
    FROM InterestingCities
    ORDER BY PopulationIn2016 DESC;

## <a name="clustered-columnstore-indexes"></a>Índices columnstore clusterizados

(Versão completa do exemplo)

Os CCI (índices Columnstore clusterizados) são usados com todas as tabelas de fatos, para reduzir a superfície de armazenamento e melhorar o desempenho da consulta. Com o uso de CCI, o armazenamento base para as tabelas de fatos usa a compactação de coluna.

Os índices não clusterizados são usados na parte superior do índice columnstore clusterizado, para facilitar as restrições de chave primária e chave estrangeira. Essas restrições foram adicionadas de uma abundância de cautela – o processo de ETL origina os dados do banco de WideWorldImporters, que tem restrições para impor a integridade. Remover as restrições de chave primária e estrangeira, e seus índices de suporte, reduziria a superfície de armazenamento das tabelas de fatos.

**Tamanho dos dados**

O banco de dados de exemplo tem um tamanho de dado limitado, para facilitar o download e a instalação do exemplo. No entanto, para ver os benefícios reais de desempenho de índices columnstore, você desejaria usar um conjunto de dados maior.

Você pode executar a instrução a seguir para aumentar o tamanho da tabela de `Fact.Sales` inserindo outras 12 milhões linhas de dados de exemplo. Essas linhas são todas inseridas para o ano 2012, de modo que não há nenhuma interferência com o processo de ETL.

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

Essa instrução levará cerca de 5 minutos para ser executada. Para inserir mais de 12 milhões linhas, passe o número desejado de linhas para inserir como um parâmetro para esse procedimento armazenado.

Para comparar o desempenho de consulta com e sem o columnstore, você pode remover e/ou recriar o índice columnstore clusterizado.

Para descartar o índice:

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

Para recriar:

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>Particionamento

(Versão completa do exemplo)

O tamanho dos dados em uma data warehouse pode crescer muito grande. Portanto, é recomendável usar o particionamento para gerenciar o armazenamento das tabelas grandes no banco de dados.

Todas as tabelas de fatos maiores são particionadas por ano. A única exceção é `Fact.Stock Holdings`, que não é baseada em data e tem um tamanho de dados limitado em comparação com as outras tabelas de fatos.

A função de partição usada para todas as tabelas particionadas é `PF_Date`e o esquema de partição que está sendo usado é `PS_Date`.

## <a name="in-memory-oltp"></a>OLTP na memória

(Versão completa do exemplo)

O WideWorldImportersDW usa SCHEMA_ONLY tabelas com otimização de memória para as tabelas de preparo. Todas as `Integration.`*tabelas `_Staging` são SCHEMA_ONLY tabelas com otimização de memória.

A vantagem das tabelas SCHEMA_ONLY é que elas não são registradas e não exigem nenhum acesso ao disco. Isso melhora o desempenho do processo ETL. Como essas tabelas não são registradas, seu conteúdo será perdido se houver uma falha. No entanto, a fonte de dados ainda está disponível, portanto, o processo de ETL pode ser simplesmente reiniciado se ocorrer uma falha.
