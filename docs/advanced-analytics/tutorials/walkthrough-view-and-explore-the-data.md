---
title: Exibir e explorar os dados usando SQL (passo a passo) | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: 308f28e85c63ce9ede4fe24fd92dc2628a7d53e6
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/04/2018
---
# <a name="view-and-explore-the-data-using-sql-walkthrough"></a>Exibir e explorar os dados usando SQL (passo a passo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A exploração de dados é uma parte importante da modelagem de dados e envolve a análise de resumos dos objetos de dados a serem usados nas análises, bem como a visualização de dados. Nesta lição, você pode explorar os objetos de dados e gerar gráficos, usando os dois [!INCLUDE[tsql](../../includes/tsql-md.md)] e funções R incluídas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

Em seguida, gerar gráficos para visualizar os dados, usando novas funções fornecidas pelo pacotes instalados com [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

> [!TIP]
> Já domina o R?
>   
> Agora que você baixou todos os dados e preparou o ambiente, sinta-se à vontade para executar o script do R completo no RStudio ou em outro ambiente e explorar a funcionalidade por conta própria. Basta abrir o arquivo RSQL_Walkthrough.R e realçar e executar linhas individuais ou executar todo o script como uma demonstração.
>   
> Para obter mais explicações sobre as funções RevoScaleR e dicas de como trabalhar com dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no R, continue o tutorial. Ele usa exatamente o mesmo script.

## <a name="verify-downloaded-data-using-sql-server"></a>Verifique se os dados baixados usando o SQL Server

Primeiro, reserve um minuto para determinar se os dados foram carregados corretamente.

1. Conecte-se ao seu [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância usando a ferramenta de gerenciamento de favoritos do banco de dados, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Gerenciador de servidores no Visual Studio ou o código do Visual Studio.

2. Selecione o banco de dados que você criou e expandir para ver o novo banco de dados, tabelas e funções.
  
    ![rsql_e2e_ssms_newobjects](media/rsql-e2e-ssms-newobjects.PNG)
  
3.  Para verificar se os dados carregados corretamente, a tabela e selecione **selecionar 1000 linhas SUPERIORES**. A opção de menu executa esta consulta:

    ```SQL
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]
    ```
    Se você não vir quaisquer dados na tabela, veja a seção [Solução de problemas](walkthrough-prepare-the-data.md) no tópico anterior.

4. Esta tabela de dados foi otimizada para cálculos baseados em conjunto por meio da adição de um [índice columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md). Execute esta instrução para gerar um resumo rápido na tabela.

    ```SQL
    SELECT DISTINCT [passenger_count]
        , ROUND (SUM ([fare_amount]),0) as TotalFares
        , ROUND (AVG ([fare_amount]),0) as AvgFares
    FROM [dbo].[nyctaxi_sample]
    GROUP BY [passenger_count]
    ORDER BY  AvgFares DESC
    ````
    Na próxima lição, você gerará alguns resumos mais complexos usando R.

## <a name="next-lesson"></a>Próxima lição

[Resumir dados usando R](walkthrough-view-and-summarize-data-using-r.md)

## <a name="previous-lesson"></a>Lição anterior

[Preparar os dados usando o PowerShell](walkthrough-prepare-the-data.md)
