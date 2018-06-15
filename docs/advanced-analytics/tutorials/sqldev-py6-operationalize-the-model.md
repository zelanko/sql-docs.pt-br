---
title: Etapa 6 colocar o modelo de Python usando o SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: aedd6beeb720c24a6960950abc6a29c1bf89a5fa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203468"
---
# <a name="step-6-operationalize-the-python-model-using-sql-server"></a>Etapa 6: Colocar o modelo de Python usando o SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte de um tutorial, [análise Python no banco de dados para desenvolvedores em SQL](sqldev-in-database-python-for-sql-developers.md). 

Nesta etapa, você aprenderá a *operacionalizar* os modelos treinados e salvo na etapa anterior.

Nesse cenário, operacionalização significa Implantando o modelo para produção para pontuação. A integração com o SQL Server torna isso muito fácil, porque você pode inserir o código Python em um procedimento armazenado. Para obter as previsões do modelo com base em novas entradas, basta chamar o procedimento armazenado a partir de um aplicativo e passa novos dados.

Esta lição demonstra dois métodos para criar previsões com base em um modelo de Python: pontuação e linha por linha de pontuação do lote.

- **A pontuação do lote:** para fornecer várias linhas de dados de entrada, passe uma consulta SELECT como um argumento para o procedimento armazenado. O resultado é uma tabela de observações correspondente aos casos de entrada.
- **Pontuação individuais:** passar um conjunto de valores de parâmetros individuais como entrada.  O procedimento armazenado retorna uma única linha ou valor.

Todo o código Python necessário para a pontuação é fornecido como parte dos procedimentos armazenados.

| Nome do procedimento armazenado | Lote ou único | Origem de modelo|
|----|----|----|
|PredictTipRxPy|lote| modelo de revoscalepy|
|PredictTipSciKitPy|lote |scikit-Saiba modelo|
|PredictTipSingleModeRxPy|única linha| modelo de revoscalepy|
|PredictTipSingleModeSciKitPy|única linha| scikit-Saiba modelo|

## <a name="batch-scoring"></a>A pontuação do lote

Os primeiros dois procedimentos armazenados ilustram a sintaxe básica para quebra automática de uma chamada de previsão Python em um procedimento armazenado. Ambos os procedimentos armazenados exigem uma tabela de dados como entradas.

- O nome do modelo exato para usar é fornecido como parâmetro de entrada para o procedimento armazenado. O procedimento armazenado carrega o modelo serializado da tabela de banco de dados `nyc_taxi_models`.table, usando a instrução SELECT no procedimento armazenado.
- O modelo serializado é armazenado na variável Python `mod` para processamento adicional usando Python.
- Os novos casos que precisam ser classificados são obtidos de [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta especificada no `@input_data_1`. Conforme os dados da consulta são lidos, as linhas são salvas no quadro de dados padrão, `InputDataSet`.
- Ambos os procedimento armazenado usar funções de `sklearn` para calcular uma métrica de exatidão, AUC (área sob a curva). Métricas de precisão, como AUC só podem ser geradas se você fornecer também o rótulo de destino (o _Oblíquo_ coluna). Previsões não é necessário o rótulo de destino (variável `y`), mas não o cálculo de métricas de precisão.

    Portanto, se você não tem rótulos de destino para os dados a ser pontuado, você pode modificar o procedimento armazenado para remover os cálculos AUC e retornar apenas as probabilidades de dica de recursos (variável `X` no procedimento armazenado).

### <a name="predicttipscikitpy"></a>PredictTipSciKitPy

O procedimento armazenado deve já foram criado para você. Se você não encontrar a ele, execute as seguintes instruções T-SQL para criar os procedimentos armazenados.

Este procedimento armazenado exige um modelo baseado no scikit-Saiba o pacote, pois ela usa funções específicas a esse pacote:

+ O quadro de dados que contém entradas é passado para o `predict_proba` função do modelo de regressão logística, `mod`. O `predict_proba` função (`probArray = mod.predict_proba(X)`) retorna um **float** que representa a probabilidade de que você terá uma dica (de qualquer valor).

```SQL
CREATE PROCEDURE [dbo].[PredictTipSciKitPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models where name = @model);
  EXEC sp_execute_external_script
    @language = N'Python',
    @script = N'
        import pickle;
        import numpy;
        from sklearn import metrics
        
        mod = pickle.loads(lmodel2)
        
        X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
        y = numpy.ravel(InputDataSet[["tipped"]])
        
        probArray = mod.predict_proba(X)
        probList = []
        for i in range(len(probArray)):
          probList.append((probArray[i])[1])
        
        probArray = numpy.asarray(probList)
        fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
        aucResult = metrics.auc(fpr, tpr)
        print ("AUC on testing data is: " + str(aucResult))
        
        OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
        ',  
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttiprxpy"></a>PredictTipRxPy

Esse procedimento armazenado usa as mesmas entradas e cria o mesmo tipo de pontuações que o procedimento anterior, mas usa funções a partir de **revoscalepy** pacote fornecido com o aprendizado de máquina do SQL Server.

> [!NOTE] 
> O código para esse procedimento armazenado alterou ligeiramente entre versões anteriores de lançamento e a versão RTM, para refletir as alterações no pacote de revoscalepy. Consulte o [alterações](#changes) tabela para obter detalhes.

```SQL
CREATE PROCEDURE [dbo].[PredictTipRxPy] (@model varchar(50), @inquery nvarchar(max))
AS
BEGIN
  DECLARE @lmodel2 varbinary(max) = (select model from nyc_taxi_models2 where name = @model);

  EXEC sp_execute_external_script 
    @language = N'Python',
    @script = N'
      import pickle;
      import numpy;
      from sklearn import metrics
      from revoscalepy.functions.RxPredict import rx_predict;
      
      mod = pickle.loads(lmodel2)
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      y = numpy.ravel(InputDataSet[["tipped"]])
      
      probArray = rx_predict(mod, X)
      prob_list = prob_array["tipped_Pred"].values 
      
      probArray = numpy.asarray(probList)
      fpr, tpr, thresholds = metrics.roc_curve(y, probArray)
      aucResult = metrics.auc(fpr, tpr)
      print ("AUC on testing data is: " + str(aucResult))
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',    
    @input_data_1 = @inquery,
    @input_data_1_name = N'InputDataSet',
    @params = N'@lmodel2 varbinary(max)',
    @lmodel2 = @lmodel2
  WITH RESULT SETS ((Score float));
END
GO
```

## <a name="run-batch-scoring-using-a-select-query"></a>Execute a pontuação do lote usando uma consulta SELECT

Os procedimentos armazenados **PredictTipSciKitPy** e **PredictTipRxPy** exigem dois parâmetros de entrada: 

- A consulta que recupera os dados de pontuação
- O nome de um modelo treinado

Ao passar os argumentos para o procedimento armazenado, você pode selecionar um modelo específico ou alterar os dados usados para pontuação.

1. Para usar o **scikit-Saiba** do modelo de pontuação, chame o procedimento armazenado **PredictTipSciKitPy**, passando o nome do modelo e a cadeia de caracteres de consulta como entradas.

    ```SQL
    DECLARE @query_string nvarchar(max) -- Specify input query
      SET @query_string='
      select tipped, fare_amount, passenger_count, trip_time_in_secs, trip_distance,
      dbo.fnCalculateDistance(pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as direct_distance
      from nyctaxi_sample_testing'
    EXEC [dbo].[PredictTipSciKitPy] 'SciKit_model', @query_string;
    ```

    O procedimento armazenado retorna as probabilidades previstas para cada viagem que foi passada como parte da consulta de entrada. 
    
    Se você estiver usando o SSMS (SQL Server Management Studio) para executar consultas, as probabilidades aparecerá como uma tabela no **resultados** painel. O **mensagens** painel produz a métrica de exatidão (AUC ou área na curva) com um valor de aproximadamente 0.56.

2. Para usar o **revoscalepy** do modelo de pontuação, chame o procedimento armazenado **PredictTipRxPy**, passando o nome do modelo e a cadeia de caracteres de consulta como entradas.

    ```SQL
    EXEC [dbo].[PredictTipRxPy] 'revoscalepy_model', @query_string;
    ```

## <a name="single-row-scoring"></a>Pontuação de única linha

Às vezes, em vez de pontuação em lote, talvez você queira passar um único caso, obtendo valores de um aplicativo e retornar um único resultado com base nesses valores. Por exemplo, você pode configurar um Excel planilha, aplicativo web ou relatório para chamar o procedimento armazenado e passe a ele insere digitado ou selecionado por usuários.

Nesta seção, você aprenderá como criar previsões únicas chamando dois procedimentos armazenados:

+ [PredictTipSingleModeSciKitPy](#PredictTipSingleModeSciKitPy) se destina a pontuação de única linha usando o scikit-aprender o modelo.
+ [PredictTipSingleModeRxPy](#PredictTipSingleModeRxPy) se destina a pontuação de única linha usando o modelo revoscalepy.
+ Se você ainda não tiver um modelo treinado ainda, retornar ao [etapa 5](sqldev-py5-train-and-save-a-model-using-t-sql.md)!

Execute os dois modelos como entrada uma série de valores únicos, como contagem de passageiro, distância de viagem e assim por diante. Uma função com valor de tabela, `fnEngineerFeatures`, é usado para converter valores de latitude e longitude de entradas para um novo recurso, direcionar distância. [Lição 4](sqldev-py4-create-data-features-using-t-sql.md) contém uma descrição dessa função com valor de tabela.

Ambos os procedimentos armazenados criar uma pontuação com base no modelo de Python.

> [!NOTE]
> 
> É importante que você forneça todos os recursos de entrada necessários pelo modelo Python quando você chamar o procedimento armazenado de um aplicativo externo. Para evitar erros, talvez seja necessário converter os dados de entrada para um tipo de dados do Python, além de validação de tipo de dados e comprimento de dados.

### <a name="predicttipsinglemodescikitpy"></a>PredictTipSingleModeSciKitPy

Reserve um minuto para examinar o código do procedimento armazenado que executa a pontuação usando o **scikit-Saiba** modelo.

```SQL
CREATE PROCEDURE [dbo].[PredictTipSingleModeSciKitPy] (@model varchar(50), @passenger_count int = 0,
  @trip_distance float = 0,
  @trip_time_in_secs int = 0,
  @pickup_latitude float = 0,
  @pickup_longitude float = 0,
  @dropoff_latitude float = 0,
  @dropoff_longitude float = 0)
AS
BEGIN
  DECLARE @inquery nvarchar(max) = N'
  SELECT * FROM [dbo].[fnEngineerFeatures]( 
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
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      probList = []
      probList.append((mod.predict_proba(X)[0])[1])
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
    ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      @model = @lmodel2,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance,
      @trip_time_in_secs=@trip_time_in_secs,
      @pickup_latitude=@pickup_latitude,
      @pickup_longitude=@pickup_longitude,
      @dropoff_latitude=@dropoff_latitude,
      @dropoff_longitude=@dropoff_longitude
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="predicttipsinglemoderxpy"></a>PredictTipSingleModeRxPy

O seguinte procedimento armazenado executa a pontuação usando o **revoscalepy** modelo.

```SQL
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
    SELECT * FROM [dbo].[fnEngineerFeatures]( 
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
      from revoscalepy.functions.RxPredict import rx_predict;
      
      # Load model and unserialize
      mod = pickle.loads(model)
      
      # Get features for scoring from input data
      X = InputDataSet[["passenger_count", "trip_distance", "trip_time_in_secs", "direct_distance"]]
      
      # Score data to get tip prediction probability as a list (of float)
      
      probArray = rx_predict(mod, X)
      
      probList = []
      prob_list = prob_array["tipped_Pred"].values
      
      # Create output data frame
      OutputDataSet = pandas.DataFrame(data = probList, columns = ["predictions"])
      ',
    @input_data_1 = @inquery,
    @params = N'@model varbinary(max),@passenger_count int,@trip_distance float,
      @trip_time_in_secs int ,
      @pickup_latitude float ,
      @pickup_longitude float ,
      @dropoff_latitude float ,
      @dropoff_longitude float',
      @model = @lmodel2,
      @passenger_count =@passenger_count ,
      @trip_distance=@trip_distance,
      @trip_time_in_secs=@trip_time_in_secs,
      @pickup_latitude=@pickup_latitude,
      @pickup_longitude=@pickup_longitude,
      @dropoff_latitude=@dropoff_latitude,
      @dropoff_longitude=@dropoff_longitude
  WITH RESULT SETS ((Score float));
END
GO
```

### <a name="generate-scores-from-models"></a>Gerar pontuações de modelos

Depois que os procedimentos armazenados foram criados, é fácil de gerar uma pontuação com base em um modelo. Basta abrir uma nova **consulta** janela e digite ou cole parâmetros para cada uma das colunas de recursos. As sete necessários são valores para essas colunas de recurso, em ordem:
    
+ *passenger_count*
+ *trip_distance* v*trip_time_in_secs*
+ *pickup_latitude*
+ *pickup_longitude*
+ *dropoff_latitude*
+ *dropoff_longitude*

1. Para gerar uma previsão usando o **revoscalepy** modelo, execute esta instrução:
  
    ```SQL
    EXEC [dbo].[PredictTipSingleModeRxPy] 'revoscalepy_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

2. Para gerar uma pontuação usando o **scikit-Saiba** modelo, execute esta instrução:

    ```SQL
    EXEC [dbo].[PredictTipSingleModeSciKitPy] 'linear_model', 1, 2.5, 631, 40.763958,-73.973373, 40.782139,-73.977303
    ```

A saída de ambos os procedimentos é uma probabilidade de uma dica que está sendo paga para a viagem táxi com os parâmetros especificados ou recursos.

### <a name="changes"></a> Alterações

Esta seção lista as alterações no código usado neste tutorial. Essas alterações foram feitas para refletir a versão mais recente **revoscalepy** versão. Para obter ajuda da API, consulte [Python função referência da biblioteca](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference).

| Alterar detalhes | Observações|
| ----|----|
| excluído `import pandas` em todas as amostras| pandas agora carregados por padrão|
| função `rx_predict_ex` alterado para `rx_predict`| As versões RTM e pré-lançamento exigem `rx_predict_ex`|
| função `rx_logit_ex` alterado para `rx_logit`| As versões RTM e pré-lançamento exigem `rx_logit_ex`|
| ` probList.append(probArray._results["tipped_Pred"])` alterado para `prob_list = prob_array["tipped_Pred"].values`| atualizações à API|

Se você instalou os serviços de Python usando uma versão de pré-lançamento do SQL Server 2017, recomendamos que você atualize. Você também pode atualizar apenas os componentes de Python e R usando a versão mais recente do servidor de aprendizado de máquina. Para obter mais informações, consulte [usando a associação para atualizar uma instância do SQL Server](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

## <a name="conclusions"></a>Conclusões

Neste tutorial, você aprendeu como trabalhar com o código Python incorporado em procedimentos armazenados. A integração com [!INCLUDE[tsql](../../includes/tsql-md.md)] torna mais fácil implantar Python modelos para previsão e incorporar o treinamento do modelo como parte de um fluxo de trabalho de dados corporativos.

## <a name="previous-step"></a>Etapa anterior

[Etapa 5: Treinar e salvar um modelo de Python](sqldev-py5-train-and-save-a-model-using-t-sql.md)

## <a name="see-also"></a>Consulte também

[Serviços de aprendizado de máquina com Python](../python/sql-server-python-services.md)
