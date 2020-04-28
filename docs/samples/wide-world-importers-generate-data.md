---
title: Gerar dados em exemplos de SQL WideWorldImporters
description: Use essas instruções SQL para gerar e importar dados de exemplo até a data atual para os bancos de WideWorldImporters de exemplo.
ms.date: 04/04/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 01bca0b4e0c8d98d0a31451686f0396af99ed430
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "79112317"
---
# <a name="wideworldimporters-data-generation"></a>Geração de dados WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
As versões de lançamento dos bancos de dados WideWorldImporters e WideWorldImportersDW têm dado de 1º de janeiro de 2013, até o dia em que os bancos de dados foram gerados.

Ao usar esses bancos de dados de exemplo, talvez você queira incluir mais informações de exemplo recentes.

## <a name="data-generation-in-wideworldimporters"></a>Geração de dados no WideWorldImporters

Para gerar dados de exemplo até a data atual:

1. Se você ainda não fez isso, instale uma versão limpa do banco de dados WideWorldImporters. Para obter instruções de instalação, consulte [instalação e configuração](wide-world-importers-oltp-install-configure.md).
2. Execute a seguinte instrução no banco de dados:

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    Essa instrução adiciona dados de exemplo de vendas e de compra ao banco de dado, até a data atual. Ele exibe o progresso da geração de dados por dia. A geração de dados pode levar cerca de 10 minutos para cada ano que precisa de dados. Devido a um fator aleatório na geração de dados, há algumas diferenças nos dados que são gerados entre as execuções.

    Para aumentar ou diminuir a quantidade de dados gerados para pedidos por dia, altere o valor do parâmetro `@AverageNumberOfCustomerOrdersPerDay`. Use os parâmetros `@SaturdayPercentageOfNormalWorkDay` e `@SundayPercentageOfNormalWorkDay` para determinar o volume do pedido para os dias de fim de semana.

## <a name="import-generated-data-in-wideworldimportersdw"></a>Importar dados gerados no WideWorldImportersDW

Para importar dados de exemplo até a data atual no banco de WideWorldImportersDW OLAP:

1. Execute a lógica de geração de dados no WideWorldImporters OLTP usando as etapas na seção anterior.
2. Se você ainda não fez isso, instale uma versão limpa do banco de dados WideWorldImportersDW. Para obter instruções de instalação, consulte [instalação e configuração](wide-world-importers-oltp-install-configure.md).
3. Refaça a propagação do banco de dados OLAP executando a seguinte instrução no banco de dados:

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. Execute o pacote de SQL Server Integration Services de *ETL. Ispac diário* para importar os dados para o banco de dado OLAP. Para saber como executar o trabalho de ETL, confira [WIDEWORLDIMPORTERS ETL Workflow](wide-world-importers-perform-etl.md).

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>Gerar dados no WideWorldImportersDW para testes de desempenho

O WideWorldImportersDW pode aumentar arbitrariamente o tamanho dos dados para testes de desempenho. Por exemplo, ele pode aumentar o tamanho dos dados a serem usados com a indexação columnstore clusterizado.

Um dos desafios é manter o tamanho do download pequeno o suficiente para ser baixado facilmente, mas grande o suficiente para demonstrar SQL Server recursos de desempenho. Por exemplo, benefícios significativos para índices columnstore são obtidos somente quando você trabalha com números maiores de linhas. 

Você pode usar o `Application.Configuration_PopulateLargeSaleTable` procedimento para aumentar o número de linhas na `Fact.Sale` tabela. As linhas são inseridas no ano civil de 2012 para evitar a colisão com dados existentes de importadores da World Wide que começam em 1º de janeiro de 2013.

### <a name="procedure-details"></a>Detalhes do procedimento

#### <a name="name"></a>Nome

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Parâmetros

  `@EstimatedRowsFor2012`**bigint** (com um padrão de 12 milhões)

#### <a name="result"></a>Result

Aproximadamente o número necessário de linhas é inserido na `Fact.Sale` tabela no ano de 2012. O procedimento limita artificialmente o número de linhas a 50.000 por dia. Você pode alterar essa limitação, mas a limitação ajuda a evitar a sobreinflaçãos acidentais da tabela.

O procedimento também aplicará a indexação columnstore clusterizado se ainda não tiver sido aplicada.
