---
title: "Geração de dados | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: samples
ms.technology:
- " database-engine "
ms.topic: article
ms.assetid: f387273b-8b5f-4687-b033-09499ea2d68f
caps.latest.revision: 
author: BarbKess
ms.author: barbkess
manager: craigg
robots: noindex,nofollow
ms.workload: Inactive
ms.openlocfilehash: 20db5f20256fb4b545482b29b0c5cc41c6ba231e
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2018
---
# <a name="wideworldimporters-data-generation"></a>Geração de dados de WideWorldImporters
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
As versões lançadas de bancos de dados WideWorldImporters e WideWorldImportersDW contém dados iniciando de 2013 1º de janeiro, até o dia em que esses bancos de dados foram gerados.

Se os bancos de dados de exemplo são usados em uma data posterior, para fins de demonstração ou ilustração, pode ser benéfico incluir dados de amostra mais recentes no banco de dados.

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

Essa instrução adiciona dados de compra e de vendas de exemplo no banco de dados, até a data atual. Ele produz o progresso dos dados de geração de dia a dia. Levará rougly 10 minutos para cada ano que precisa de dados. Observe que há algumas diferenças nos dados gerados entre as execuções, pois já existe um fator aleatório na geração de dados.

Para aumentar ou diminuir a quantidade de dados gerado, em termos de pedidos por dia, altere o valor para o parâmetro `@AverageNumberOfCustomerOrdersPerDay`. Os parâmetros `@SaturdayPercentageOfNormalWorkDay` e `@SundayPercentageOfNormalWorkDay` são usados para determinar o volume de pedidos para a semana.

## <a name="importing-generated-data-in-wideworldimportersdw"></a>Importação de dados gerados no WideWorldImportersDW

Para importar dados de exemplo até a data atual no banco de dados OLAP WideWorldImportersDW, siga estas etapas:

1. Execute a lógica de geração de dados no banco de dados OLTP WideWorldImporters, seguindo as etapas acima.
2. Se você não ainda tiver feito isso, instale uma versão limpa do banco de dados WideWorldImportersDW. Para obter instruções de instalação, **WideWorldImporters instalação e configuração**.
3. Propagar novamente o banco de dados OLAP, executando a seguinte instrução no banco de dados:

```
    EXECUTE [Application].Configuration_ReseedETL
```

4. Execute o pacote do SSIS **ETL.ispac diário** para importar os dados para o banco de dados OLAP. Para obter instruções sobre como executar o trabalho ETL, consulte **fluxo de trabalho de ETL de WideWorldImporters**.

## <a name="generating-data-in-wideworldimportersdw-for-performance-testing"></a>Geração de dados em WideWorldImportersDW para teste de desempenho

WideWorldImportersDW tem a capacidade de aumentar o tamanho dos dados, para fins de testes de desempenho, por exemplo com columnstore clusterizado arbitrariamente.

Um dos desafios ao enviar um exemplo de como a World Wide Importers é manter o tamanho do download pequeno o suficiente para ser distribuível mas grande o suficiente para demonstrar os recursos de desempenho do SQL Server. Uma área em que isso é um desafio específico é ao trabalhar com índices columnstore. Benefícios significativos vir somente quando estiver trabalhando com um número maior de linhas. 

O procedimento `Application.Configuration_PopulateLargeSaleTable` pode ser usado para aumentar significativamente o número de linhas no `Fact.Sale` tabela. Observe que as linhas são inseridas no ano de 2012 para evitar conflito com dados existentes do World Wide Importers começando em 1º de janeiro de 2013.

### <a name="procedure-details"></a>Detalhes de procedimento

#### <a name="name"></a>Nome: 

    Application.Configuration_PopulateLargeSaleTable

#### <a name="parameters"></a>Parâmetros:

  `@EstimatedRowsFor2012` **bigint** (com um padrão de 12000000)

#### <a name="result"></a>Resultado:

Aproximadamente o número necessário de linhas é inserido no `Fact.Sale` tabela no ano de 2012. O procedimento limita artificialmente o número de linhas por dia para 50000. Isso pode ser alterado, mas há evitar overinflations accidential da tabela.

Além disso, o procedimento se aplica a indexação de columnstore clusterizado, se não tiver sido aplicada já.
