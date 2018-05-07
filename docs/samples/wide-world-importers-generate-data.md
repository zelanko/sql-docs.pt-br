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
ms.openlocfilehash: be472ed5594a523497244c25264e16530e2a12ac
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="wideworldimporters-data-generation"></a>Geração de dados de WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
As versões lançadas de bancos de dados WideWorldImporters e WideWorldImportersDW contém dados iniciando de 2013 1 de janeiro, até o dia em que esses bancos de dados foram gerados.

Ao usar os bancos de dados de exemplo, isso pode ser útil incluir dados de amostra mais recentes.

## <a name="data-generation-in-wideworldimporters"></a>Geração de dados de WideWorldImporters

Para gerar dados de exemplo até a data atual, siga estas etapas:

1. Se você não ainda tiver feito isso, instale uma versão limpa do banco de dados de WideWorldImporters. Para obter instruções de instalação, **WideWorldImporters instalação e configuração**.
2. Execute a seguinte instrução no banco de dados:

```
    EXECUTE DataLoadSimulation.PopulateDataToCurrentDate
        @AverageNumberOfCustomerOrdersPerDay = 60,
        @SaturdayPercentageOfNormalWorkDay = 50,
        @SundayPercentageOfNormalWorkDay = 0,
        @IsSilentMode = 1,
        @AreDatesPrinted = 1;
```

Essa instrução adiciona dados de compra e de vendas de exemplo no banco de dados, até a data atual. Ele produz o progresso dos dados de geração de dia a dia. Pode levar cerca de 10 minutos para cada ano que precisa de dados. Há algumas diferenças nos dados gerados entre as execuções, pois já existe um fator aleatório na geração de dados.

Para aumentar ou diminuir a quantidade de dados gerado, em termos de pedidos por dia, altere o valor para o parâmetro `@AverageNumberOfCustomerOrdersPerDay`. Os parâmetros `@SaturdayPercentageOfNormalWorkDay` e `@SundayPercentageOfNormalWorkDay` são usados para determinar o volume de pedidos para a semana.

## <a name="importing-generated-data-in-wideworldimportersdw"></a>Importação de dados gerados no WideWorldImportersDW

Para importar dados de exemplo até a data atual no banco de dados OLAP WideWorldImportersDW, siga estas etapas:

1. Execute a lógica de geração de dados no banco de dados OLTP WideWorldImporters, seguindo as etapas acima.
2. Se você não ainda tiver feito isso, instale uma versão limpa do banco de dados WideWorldImportersDW. Para obter instruções de instalação, **WideWorldImporters instalação e configuração**.
3. Propagar novamente o banco de dados OLAP, executando a seguinte instrução no banco de dados:

    ```sql
    EXECUTE [Application].Configuration_ReseedETL
    ```

4. Execute o pacote do SSIS **ETL.ispac diário** para importar os dados para o banco de dados OLAP. Para obter instruções sobre como executar o trabalho ETL, consulte **fluxo de trabalho de ETL de WideWorldImporters**.

## <a name="generating-data-in-wideworldimportersdw-for-performance-testing"></a>Geração de dados em WideWorldImportersDW para teste de desempenho

WideWorldImportersDW tem a capacidade de aumentar o tamanho dos dados, para fins de testes de desempenho, por exemplo com columnstore clusterizado arbitrariamente.

Um dos desafios é manter o tamanho do download pequeno o suficiente para baixar facilmente, mas grande suficiente para demonstrar os recursos de desempenho do SQL Server. Por exemplo, benefícios significativos para índices columnstore ocorrem somente quando estiver trabalhando com um número maior de linhas. 

O procedimento `Application.Configuration_PopulateLargeSaleTable` pode ser usado para aumentar significativamente o número de linhas no `Fact.Sale` tabela. Observe que as linhas são inseridas no ano de 2012 para evitar conflito com dados existentes do World Wide Importers começando em 1 de janeiro de 2013.

### <a name="procedure-details"></a>Detalhes de procedimento

#### <a name="name"></a>Nome: 

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Parâmetros:

  `@EstimatedRowsFor2012` **bigint** (com um padrão de 12000000)

#### <a name="result"></a>Resultado:

Aproximadamente o número necessário de linhas é inserido no `Fact.Sale` tabela no ano de 2012. O procedimento limita artificialmente o número de linhas por dia para 50000. Essa limitação pode ser alterada, mas há evitar overinflations acidentais da tabela.

Além disso, o procedimento se aplica a indexação de columnstore clusterizado, se não tiver sido aplicada já.
