---
title: "Li&#231;&#227;o 2: Exibir e explorar os dados (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: d3835d6d-e68b-486d-81a0-81b717cc6134
caps.latest.revision: 32
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 26
---
# Li&#231;&#227;o 2: Exibir e explorar os dados (Passo a passo de ponta a ponta sobre a ci&#234;ncia de dados)
A exploração de dados é uma parte importante da modelagem de dados e envolve a análise de resumos dos objetos de dados a serem usados nas análises, bem como a visualização de dados. Nesta lição, você aprenderá a explorar os objetos de dados e gerar plotagens, usando as funções [!INCLUDE[tsql](../../includes/tsql-md.md)] e do R incluídas no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
Em seguida, você vai gerar plotagens para visualizar os dados, usando novas funções fornecidas pelo pacotes instalados com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].  
  
> [!TIP]  
> Já domina o R?  
>   
> Agora que você baixou todos os dados e preparou o ambiente, sinta-se à vontade para executar o script do R completo no RStudio ou em outro ambiente e explorar a funcionalidade por conta própria. Basta abrir o arquivo RSQL_Walkthrough.R e realçar e executar linhas individuais ou executar todo o script como uma demonstração.  
>   
> Para obter mais explicações sobre as funções RevoScaleR e dicas de como trabalhar com dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no R, continue o tutorial. Ele usa exatamente o mesmo script.  
  
## <a name="verify-downloaded-data-using-sql"></a>Verificar os dados baixados usando o SQL  
Primeiro, reserve um minuto para determinar se os dados foram carregados corretamente.  
  
1.  Conecte-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    Você pode usar uma variedade de ferramentas para se conectar e exibir bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]    
    -   Gerenciador de Servidores no Visual Studio  
  
2.  Expanda o banco de dados criado. A imagem a seguir mostra os novos bancos de dados, tabelas e funções no **Gerenciador de Servidores.**  
  
    ![new database objects created by script](../../advanced-analytics/r-services/media/rsql-e2e-ssms-newobjects.PNG "new database objects created by script")  
  
3.  Você também pode executar consultas simples nos dados. Por exemplo, no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], clique com o botão direito do mouse na tabela e selecione **Selecionar as 1.000 primeiras linhas** para gerar e executar esta consulta:  
  
    ```  
    SELECT TOP 1000 * FROM [dbo].[nyctaxi_sample]  
    ```  
    Se você não vir quaisquer dados na tabela, veja a seção [Solução de problemas](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md) no tópico anterior.
      
4.  Para exibir o esquema e os tipos dos dados, você pode usar as exibições de gerenciamento do sistema no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    ```  
    SELECT TABLE_CATALOG, TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, COLUMN_DEFAULT  
    FROM [TaxiSample].INFORMATION_SCHEMA.COLUMNS  
    WHERE TABLE_NAME = N'nyctaxi_sample';  
    ```  
  
    > [!TIP]  
    > Para obter detalhes sobre como a tabela de dados foi criada, também é possível examinar o script `create-db-tb-upload-data.sql`.  
  
### <a name="generate-summaries-using-sql"></a>Gerar resumos usando o SQL  
Um dos pontos fortes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que o torna um bom complemento para o R é a capacidade de executar cálculos baseados em conjunto com muita rapidez.  O código que criou a tabela deste passo a passo também aplicou um [índice columnstore](../Topic/Columnstore%20Indexes%20Guide.md) para fazer cálculos ainda mais rápidos.   
  
```  
SELECT DISTINCT [passenger_count]  
    , ROUND (SUM ([fare_amount]),0) as TotalFares   
    , ROUND (AVG ([fare_amount]),0) as AvgFares  
FROM [dbo].[nyctaxi_sample]  
GROUP BY [passenger_count]   
ORDER BY  AvgFares desc  
```  

Nas próximas etapas, você usará o R para gerar alguns resumos e plotagens mais sofisticados, usando os dados no SQL Server.  
  
## <a name="next-steps"></a>Próximas etapas  
[Exibir e resumir dados usando o R &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/view-and-summarize-data-using-r-data-science-end-to-end-walkthrough.md)  
  
[Criar gráficos e plotagens usando o R &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/create-graphs-and-plots-using-r-data-science-end-to-end-walkthrough.md)  
  
## <a name="previous-lesson"></a>Lição anterior  
[Lição 1: Preparar os dados &#40;Passo a passo de ponta a ponta sobre a ciência de dados&#41;](../../advanced-analytics/r-services/lesson-1-prepare-the-data-data-science-end-to-end-walkthrough.md)  
  
## <a name="see-also"></a>Consulte também  
[Guia de Índices columnstore](../Topic/Columnstore%20Indexes%20Guide.md)  
  
  
  
