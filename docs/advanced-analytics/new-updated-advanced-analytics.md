---
title: Atualizado - Advanced Analytics para documentos do SQL Server | Microsoft Docs
description: "Trechos de código de exibição de conteúdo atualizado recentemente alterada na documentação de, para Advanced Analytics para o Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/17/2017
ms.author: genemi
ms.workload: advanced-analytics
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 79f979ecda1ff0851978d19ef28fa3cf909f9a43
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Novos e atualizados recentemente: Advanced Analytics para o SQL Server



A Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/) todos os dias. Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **23-05-2017** &nbsp; até &nbsp; **17-07-2017**
- *Área de assunto:* &nbsp; **Advanced Analytics para o SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Problemas comuns com a execução do Script externo](common-issues-external-script-execution.md)
2. [Coleta de dados para a solução de problemas de aprendizado de máquina](data-collection-ml-troubleshooting-process.md)
3. [Tutoriais do SQL Server Python](tutorials/sql-server-python-tutorials.md)
4. [Tutoriais do SQL Server R](tutorials/sql-server-r-tutorials.md)




&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma grande atualização recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-introducing-revoscalepypythonwhat-is-revoscalepymd"></a>1. &nbsp;[Apresentando revoscalepy](python/what-is-revoscalepy.md)

*Atualizado: 23-06-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Próximo](#TitleNum_2))

<!-- Source markdown line 112.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cab7330ac9944508aaa360e00cbc2e866455776d 33f4e0e2421fa79fc11931dc7f29bff4432c6f5a  (PR=2171  ,  Filename=what-is-revoscalepy.md  ,  Dirpath=docs\advanced-analytics\python\  ,  MergeCommitSha40=7d2dbe0bdc4cbd05f11eacf938b35a9c35ace2e7) -->



**Usando revoscalepy com MicrosoftML**


As funções do Python para MicrosoftML são integradas com as fontes de dados que são fornecidas no revoscalepy e contextos de computação. Portanto, você pode usar um algoritmo de MicrosoftML para definir e treinar um modelo em Python e usar as funções de revoscalepy para executar o código Python localmente ou em um contexto de computação do SQl Server.

Importar apenas os módulos em seu código Python e, em seguida, fazer referência as funções individuais, que você precisa.

```
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**Requisitos**


Para executar o código Python no SQL Server, você deve ter instalado o SQL Server 2017 junto com o recurso **serviços de aprendizado de máquina**e habilitado a linguagem Python. Versões anteriores do SQL Server não dão suporte a integração do Python.

> [!NOTE]
> Distribuições de código aberto do Python não dão suporte para contextos de computação do SQL Server. No entanto, se você precisar publicar e consumir aplicativos Python do Windows, você pode instalar o servidor de aprendizado de máquina do Microsoft sem instalar o SQL Server. Para obter mais informações, consulte [criar Standalone R Server-... /r/Create-a-standalone-r-Server.MD)

**Obter mais ajuda**





&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-step-5-train-and-save-a-model-using-t-sqltutorialssqldev-py5-train-and-save-a-model-using-t-sqlmd"></a>2. &nbsp;[Etapa 5: treinar e salvar um modelo usando o T-SQL](tutorials/sqldev-py5-train-and-save-a-model-using-t-sql.md)

*Atualizado em: 2017-06-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [próxima](#TitleNum_3))

<!-- Source markdown line 121.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5c1cbe92282b96105ffdb69efa803f58dc0ac7e2 e4077a2154a90de468c435efa5b2225125d5b0e7  (PR=1904  ,  Filename=sqldev-py5-train-and-save-a-model-using-t-sql.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=dbf91e0d6f8257227cfe8ac6d13c484d0a566f57) -->



1. Em [! INCLUIR [ssManStudio-... /.. /Includes/ssmanstudio-MD.MD)], abra uma nova janela de consulta e execute a seguinte instrução para criar o procedimento armazenado _TrainTipPredictionModelRxPy_.  Este modelo será baseado nos dados de treinamento que você preparou. Como o procedimento armazenado já inclui uma definição dos dados de entrada, você não precisa fornecer uma consulta de entrada.

    ```SQL
    DROP PROCEDURE IF EXISTS TrainTipPredictionModelRxPy;
    GO

    CREATE PROCEDURE [dbo].[TrainTipPredictionModelRxPy] (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script 
      @language = N'Python',
      @script = N'
    import numpy
    import pickle
    import pandas
    from revoscalepy.functions.RxLogit import rx_logit_ex
    
    ## Create a logistic regression model using rx_logit_ex function from revoscalepy package
    logitObj = rx_logit_ex("tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance", data = InputDataSet);
    
    ## Serialize model
    trained_model = pickle.dumps(logitObj)
    ',
    @input_data_1 = N'
    select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance, 
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
    from nyctaxi_sample_training
    ',
    @input_data_1_name = N'InputDataSet',
    @params = N'@trained_model varbinary(max) OUTPUT',
    @trained_model = @trained_model OUTPUT;
    ;
    END;
    ```



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-step-6-operationalize-the-modeltutorialssqldev-py6-operationalize-the-modelmd"></a>3. &nbsp;[Etapa 6: colocar o modelo](tutorials/sqldev-py6-operationalize-the-model.md)

*Atualizado em: 2017-06-01* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [próxima](#TitleNum_4))

<!-- Source markdown line 236.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1eb50ac902d4e80bafb1dd7fdf8f607dcdf0d33f 57d5abdc6119db1ecd81587d625054a5bbfb5fc8  (PR=1904  ,  Filename=sqldev-py6-operationalize-the-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=dbf91e0d6f8257227cfe8ac6d13c484d0a566f57) -->



Esta é a definição do procedimento armazenado que executa a pontuação usando o **revoscalepy** modelo.

```
CREATE PROCEDURE [dbo].[PredictTipSingleModeRxPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
    SELECT * FROM [dbo].[fnEngineerFeatures-- 
      @passenger_count,
      @trip_distance,
      @trip_time_in_secs,
      @pickup_latitude,
      @pickup_longitude,
      @dropoff_latitude,
      @dropoff_longitude)
    '
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);
  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      import pandas;
      from revoscalepy.functions.RxPredict import rx_predict_ex;
```




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-use-python-with-revoscalepy-to-create-a-modeltutorialsuse-python-revoscalepy-to-create-modelmd"></a>4. &nbsp;[Uso Python com revoscalepy para criar um modelo](tutorials/use-python-revoscalepy-to-create-model.md)

*Atualizado em: 2017-06-21* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3))

<!-- Source markdown line 119.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0886939f86fe12d7ff7b339689a02c7fc75e0786 23dd469349a05d535063aab3c14aec152ed2cd7b  (PR=2141  ,  Filename=use-python-revoscalepy-to-create-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=76839e39427e24688609353b8708d59fee772d28) -->



**Examine o código**


Vamos examinar o código e destacar algumas etapas principais.

**Definindo um dados de origem e contexto de computação**


Isso é uma parte importante do uso de **revoscalepy** e seu pacote de R relacionado **RevoScaleR**. Uma fonte de dados é diferente de um contexto de computação. O _fonte de dados_ define os dados usados em seu código. O _contexto de computação_ define onde o código será executado.

> [!NOTE]
> Suporte para alguns tipos de fonte de dados com suporte no RevoScaleR pode ser limitado na versão de pré-lançamento. Para obter mais informações sobre as funções incluídas na versão mais recente, consulte [What ' s revoscalepy-... /Python/What-is-revoscalepy.MD).

Geral de processo para criar e usar uma fonte de dados e computação contexto é o seguinte:

1. Criar variáveis de Python, tais como _sqlQuery_ e _connectionString_, que definem a fonte e os dados que você deseja usar. Passar essas variáveis para o **RxSqlServerData** construtor para implementar o **o objeto de fonte de dados** chamado _dataSource_.
2. Criar um objeto de contexto de computação usando o **RxInSqlServer** construtor. Neste exemplo, você passa a mesma cadeia de conexão que você definiu anteriormente, supondo que os dados estão na mesma instância do SQL Server que você usará como o contexto de computação. No entanto, a fonte de dados e o contexto de computação podem estar em servidores diferentes. Resultante **objeto de contexto de computação** chamado _computeContext_.
3. Escolha o contexto de computação ativa. Por padrão, as operações são executadas localmente, o que significa que se você não especificar um contexto de computação diferente, os dados serão obtidos da fonte de dados e ajuste o modelo será executado no ambiente atual do Python.

    Em RevoScaleR, você também pode usar a função `rxSetComputeContext` para alternar entre contextos de computação. A função não foi implementada ainda na versão de visualização de **revoscalepy**, mas você pode especificar o contexto de computação como um argumento para **rx_lin_mod_ex**.





<a name="similars2"/>

&nbsp;

## <a name="similar-articles"></a>Artigos Semelhantes

Esta seção lista os artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, dentro do mesmo repositório GitHub.com: [MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170717-1101  -->

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que têm artigos novos ou atualizados recentemente

- [Novo + Atualizado (4 + 4): documentos de **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + Atualizado (2 + 0): documentos do **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + Atualizado (1 + 2): documentos de **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + Atualizado (6 + 0): documentos do **Mecanismo de Banco de Dados do SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (13 + 2): documentos do **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + Atualizado (1 + 0): documentos do **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + Atualizado (1 + 0): documentos do **Open Database Connectivity (ODBC) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + Atualizado (8 + 4): documentos de **Bancos de Dados Relacionais do SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (2 + 2): documentos do **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + Atualizado (0 + 1): documentos do **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (1 + 0): documentos do **Transact-SQL**](../t-sql/new-updated-t-sql.md)
- [Novo + Atualizado (1 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)


#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas de assunto que não têm nenhum artigo novo ou atualizado recentemente

- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0 + 0): documentos do **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + Atualizado (0 + 0): documentos do **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + Atualizado (0 + 0): documentos do **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Novo + atualizado (0 + 0): documentos do **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)


&nbsp;


