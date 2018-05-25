---
title: WideWorldImporters gerar dados - banco de dados de exemplo SQL | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ace1f771ef3a77a6f7db0072442affe181d7872
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="wideworldimporters-data-generation"></a>Geração de dados de WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
As versões lançadas de bancos de dados WideWorldImporters e WideWorldImportersDW tem dados de 1 de janeiro de 2013, até o dia em que os bancos de dados foram gerados.

Quando você usa esses bancos de dados de exemplo, talvez queira incluir dados de exemplo mais recentes.

## <a name="data-generation-in-wideworldimporters"></a>Geração de dados de WideWorldImporters

Para gerar dados de exemplo até a data atual:

1. Se você ainda não tiver feito isso, instale uma versão limpa do banco de dados de WideWorldImporters. Para obter instruções de instalação, consulte [instalação e configuração](wide-world-importers-oltp-install-configure.md).
2. Execute a seguinte instrução no banco de dados:

    ```
        EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
            @AverageNumberOfCustomerOrdersPerDay = 60,
            @SaturdayPercentageOfNormalWorkDay = 50,
            @SundayPercentageOfNormalWorkDay = 0,
            @IsSilentMode = 1,
            @AreDatesPrinted = 1;
    ```

    Essa instrução adiciona dados de compra e de vendas de exemplo para o banco de dados, até a data atual. Ele exibe o progresso da geração de dados por dia. Geração de dados pode levar cerca de 10 minutos para cada ano que precisa de dados. Devido a um fator aleatório na geração de dados, existem algumas diferenças nos dados que são gerados entre as execuções.

    Para aumentar ou diminuir a quantidade de dados gerados de pedidos por dia, altere o valor para o parâmetro `@AverageNumberOfCustomerOrdersPerDay`. Use os parâmetros `@SaturdayPercentageOfNormalWorkDay` e `@SundayPercentageOfNormalWorkDay` para determinar o volume de pedidos para a semana.

## <a name="import-generated-data-in-wideworldimportersdw"></a>Dados de importação gerado em WideWorldImportersDW

Para importar dados de exemplo até a data atual no banco de dados OLAP WideWorldImportersDW:

1. Execute a lógica de geração de dados no banco de dados OLTP WideWorldImporters usando as etapas na seção anterior.
2. Se você ainda não tiver feito isso, instale uma versão limpa do banco de dados WideWorldImportersDW. Para obter instruções de instalação, consulte [instalação e configuração](wide-world-importers-oltp-install-configure.md).
3. Propagar novamente o banco de dados OLAP, executando a seguinte instrução no banco de dados:

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. Execute o *ETL.ispac diário* pacote do SQL Server Integration Services para importar os dados para o banco de dados OLAP. Para saber como executar o trabalho ETL, consulte [fluxo de trabalho de ETL WideWorldImporters](wide-world-importers-perform-etl.md).

## <a name="generate-data-in-wideworldimportersdw-for-performance-testing"></a>Gerar dados no WideWorldImportersDW para teste de desempenho

WideWorldImportersDW arbitrariamente pode aumentar o tamanho dos dados para teste de desempenho. Por exemplo, ele pode aumentar o tamanho de dados a ser usado com a indexação de columnstore clusterizado.

Um dos desafios é manter o tamanho do download pequeno o suficiente para baixar facilmente, mas grande suficiente para demonstrar os recursos de desempenho do SQL Server. Por exemplo, os benefícios significativos para índices columnstore são obtidos somente quando você trabalha com um número maior de linhas. 

Você pode usar o `Application.Configuration_PopulateLargeSaleTable` procedimento para aumentar o número de linhas no `Fact.Sale` tabela. As linhas são inseridas no ano de 2012 para evitar conflito com os dados existentes do World Wide Importers que começa em 1 de janeiro de 2013.

### <a name="procedure-details"></a>Detalhes de procedimento

#### <a name="name"></a>Nome

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Parâmetros

  `@EstimatedRowsFor2012` **bigint** (com um padrão de 12000000)

#### <a name="result"></a>Resultado

Aproximadamente o número necessário de linhas é inserido no `Fact.Sale` tabela no ano de 2012. O procedimento limita artificialmente o número de linhas a serem 50.000 por dia. Você pode alterar essa limitação, mas a limitação ajuda a evitar overinflations acidentais da tabela.

O procedimento também se aplica a columnstore clusterizado indexação se já não tiver sido aplicada.
