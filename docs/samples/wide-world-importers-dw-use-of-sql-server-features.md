---
title: Banco de dados OLAP WideWorldImporters - uso do SQL Server | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 08/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azure-sqldw-latest||>=aps-pdw-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9c4d9cc92bb9571bbda48f40f74b38bf8d918991
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39532916"
---
# <a name="wideworldimportersdw-use-of-sql-server-features-and-capabilities"></a>Uso de WideWorldImportersDW de recursos e recursos do SQL Server
[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md](../includes/appliesto-ss-xxxx-asdw-pdw-md.md)]
WideWorldImportersDW foi projetado para demonstrar muitos dos principais recursos do SQL Server que são adequados para data warehousing e análise. O exemplo a seguir é uma lista de recursos do SQL Server, recursos e uma descrição de como eles são usados em WideWorldImportersDW.

## <a name="polybase"></a>PolyBase

[Aplica-se ao SQL Server (2016 e posterior)]

O PolyBase é usado para combinar informações de vendas de WideWorldImportersDW com um conjunto de dados público sobre dados demográficos para entender quais cidades podem ser de interesse para expansão adicional de vendas.

Para habilitar o uso do PolyBase no banco de dados de exemplo, verifique se que ele está instalado e execute o seguinte procedimento armazenado no banco de dados:

    EXEC [Application].[Configuration_ApplyPolybase]

Isso criará uma tabela externa `dbo.CityPopulationStatistics` que faz referência a um conjunto de dados público que contém dados de população para cidades dos Estados Unidos, hospedado no armazenamento de BLOBs do Azure. Você é incentivado a examinar o código no procedimento armazenado para entender o processo de configuração. Se você quiser hospedar seus próprios dados no armazenamento de BLOBs do Azure e mantê-lo seguro do acesso ao público geral, você precisará realizar etapas adicionais de configuração. A consulta a seguir retorna os dados do conjunto de dados externo:

    SELECT CityID, StateProvinceCode, CityName, YearNumber, LatestRecordedPopulation FROM dbo.CityPopulationStatistics;

Para entender quais cidades podem ser interessantes para expansão adicional, a consulta a seguir examina a taxa de crescimento de cidades e retorna as cidades de 100 principais maior com um crescimento significativo, e onde a Wide World Importers não tem uma presença de vendas. A consulta envolver uma junção entre a tabela remota `dbo.CityPopulationStatistics` e a tabela local `Dimension.City`e um filtro que envolvam a tabela local `Fact.Sales`.

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

Índices de Columnstore clusterizado (CCI) são usados com todas as tabelas de fatos para reduzir o volume de armazenamento e melhorar o desempenho da consulta. Com o uso de CCI, o armazenamento de base para as tabelas de fatos usa a compactação de coluna.

Índices não clusterizados são usados na parte superior do índice columnstore clusterizado, para facilitar a chave primária e restrições de chave estrangeira. Essas restrições foram adicionadas fora de uma vasta gama de cuidado: o processo de ETL fontes de dados do banco de dados WideWorldImporters, que tem restrições para impor a integridade. Remover restrições de chave primárias e estrangeiras e seus índices de suporte, seria reduzir o volume de armazenamento das tabelas de fato.

**Tamanho dos dados**

O banco de dados de exemplo limitou o tamanho dos dados, para que seja fácil baixar e instalar o exemplo. No entanto, para ver os benefícios de desempenho real dos índices columnstore, você iria querer usar um conjunto de dados maior.

Você pode executar a instrução a seguir para aumentar o tamanho do `Fact.Sales` tabela ao inserir outra linha de 12 milhões de dados de exemplo. Essas linhas são todos inseridas para o ano de 2012, de modo que não há nenhuma interferência com o processo de ETL.

    EXECUTE [Application].[Configuration_PopulateLargeSaleTable]

Essa instrução levará cerca de 5 minutos para ser executado. Para inserir mais de 12 milhões de linhas, passe o número desejado de linhas a ser inserido como um parâmetro para esse procedimento armazenado.

Para comparar o desempenho da consulta com e sem columnstore, você pode remover e/ou recrie o índice columnstore clusterizado.

Para descartar o índice:

    DROP INDEX [CCX_Fact_Order] ON [Fact].[Order]

Para recriar:

    CREATE CLUSTERED COLUMNSTORE INDEX [CCX_Fact_Order] ON [Fact].[Order]

## <a name="partitioning"></a>Particionamento

(Versão completa do exemplo)

Tamanho dos dados em um Data Warehouse pode ficar muito grande. Portanto, é prática recomendada é usar o particionamento para gerenciar o armazenamento de grandes tabelas no banco de dados.

Todas as tabelas de fatos maiores são particionadas por ano. A única exceção é `Fact.Stock Holdings`, que não é baseado em data e tem tamanho de dados limitado em comparação com outras tabelas de fatos.

A função de partição usada em tabelas particionadas tudo é `PF_Date`, e o esquema de partição que está sendo usado é `PS_Date`.

## <a name="in-memory-oltp"></a>OLTP na memória

(Versão completa do exemplo)

WideWorldImportersDW usa as tabelas com otimização de memória SCHEMA_ONLY para as tabelas de preparo. Todos os `Integration.` * `_Staging` tabelas são as tabelas com otimização de memória SCHEMA_ONLY.

A vantagem das tabelas SCHEMA_ONLY é que eles não são registrados e não exigem qualquer acesso ao disco. Isso melhora o desempenho do processo de ETL. Desde que essas tabelas não estiver conectadas, seus conteúdos serão perdidos, se houver uma falha. No entanto, a fonte de dados ainda estiver disponível, portanto, o processo de ETL pode simplesmente ser reiniciado se ocorrer uma falha.
