---
title: Usar um modelo de Python no SQL Server para treinamento e previsões | Microsoft Docs
description: Crie e treine um modelo usando o Python e o conjunto de dados íris clássico. Salvar o modelo para o SQL Server e, em seguida, usá-lo para gerar os resultados previstos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/18/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 839bcecdeaf7b5e2a7ea1297fe941353bffed20e
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461832"
---
# <a name="use-a-python-model-in-sql-server-for-training-and-scoring"></a>Usar um modelo de Python no SQL Server para treinamento e pontuação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste exercício de Python, saiba um padrão comum para a criação, treinamento e usando um modelo no SQL Server. Este exercício cria dois procedimentos armazenados. O primeiro deles gera um modelo de Naïve Bayes para prever uma espécie de íris com base nas características da flor. É o segundo procedimento para pontuação. Ele chama o modelo gerado no primeiro procedimento para um conjunto de previsões de saída. Percorrendo este exercício, você aprenderá técnicas básicas que são fundamentais para executar o código do Python em uma instância do mecanismo de banco de dados do SQL Server.

Dados de exemplo usados neste exercício são o [conjunto de dados íris](demo-data-iris-in-sql.md) na **irissql** banco de dados.

## <a name="create-a-model-using-a-sproc"></a>Criar um modelo usando um sproc

1. Abra uma nova janela de consulta no Management Studio, conectado para o **irissql** banco de dados. 

    ```sql
    USE irissql
    GO
    ```

2. Execute o seguinte código em uma nova janela de consulta para criar o procedimento armazenado que cria e treina um modelo. Modelos que são armazenados para reutilização no SQL Server são serializados como um fluxo de bytes e armazenados em uma coluna varbinary (max) em uma tabela de banco de dados. Depois de criar o modelo, treinado, serializado e salvos em um banco de dados, ele pode ser chamado por outros procedimentos ou pela função PREVER T-SQL em cargas de trabalho de pontuação.

   Esse código usa pickle para serializar o modelo e o scikit para fornecer o algoritmo Naïve Bayes. O modelo será treinado usando dados de colunas de 0 a 4 dos **iris_data** tabela. Os parâmetros que você pode ver na segunda parte do procedimento articulam entradas de dados e saídas de modelo. 

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]]))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

3. Verifique se que o procedimento armazenado existe. Se o script T-SQL da etapa anterior for executado sem erro, um novo procedimento armazenado chamado **generate_iris_model** é criado e adicionado para o **irissql** banco de dados. Você pode encontrar os procedimentos armazenados no Management Studio **Pesquisador de objetos**, em **programação**.

## <a name="execute-the-sproc-to-create-and-train-models"></a>Execute o sproc para criar e treinar modelos

1. Depois que o procedimento armazenado é criado, execute o seguinte código abaixo para executá-lo. A instrução específica para executar um procedimento armazenado é `EXEC` na quinta linha.

   Esse script em particular exclui um modelo existente de mesmo nome ("Bayesiana ingênua") para liberar espaço para novos criados executando novamente o mesmo procedimento. Sem exclusão do modelo, ocorrerá um erro informando que o objeto já existe. 

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes '
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. Exiba os resultados na área de saída. O script inclui uma instrução SELECT, mostrando que o modelo existe. É outra maneira de retornar uma lista de modelos `SELECT * FROM iris_models` na **irissql**.

    **Resultados**

    |   | (nenhum nome de coluna |
    |---|-----------------|
    | 1 | Naive Bayes     | 


## <a name="create-and-execute-a-sproc-for-generating-predictions"></a>Criar e executar um sproc para gerar previsões

Agora que você criou, treinado e salvo de um modelo, passar para a próxima etapa: criar um procedimento armazenado que gera previsões. Você fará isso por chamada sp_execute_external_script para iniciar o Python e, em seguida, passar no script de Python que carrega um modelo serializado criado no último exercício e, em seguida, ele fornece entradas de dados para a pontuação.

1. Execute o seguinte código para criar o procedimento armazenado que executa a pontuação. Em tempo de execução, esse procedimento carregar um modelo binário, use colunas `[1,2,3,4]` assim como as entradas e especificar colunas `[0,5,6]` como saída.

    ```sql
    CREATE PROCEDURE predict_species (@model varchar(100))
    AS
    BEGIN
    DECLARE @nb_model varbinary(max) = (SELECT model FROM iris_models WHERE model_name = @model);
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'
    import pickle
    irismodel = pickle.loads(nb_model)
    species_pred = irismodel.predict(iris_data[[1,2,3,4]])
    iris_data["PredictedSpecies"] = species_pred
    OutputDataSet = iris_data[[0,5,6]] 
    print(OutputDataSet)
    '
    , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@nb_model varbinary(max)'
    , @nb_model = @nb_model
    WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));
    END;
    GO
    ```

2. Execute o procedimento armazenado, fornecendo o nome do modelo "Bayesiana ingênua" para que o procedimento sabe qual modelo usar. 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    Quando você executa o procedimento armazenado, ele retorna um Frame do Python. Esta linha de T-SQL Especifica o esquema para os resultados retornados: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`. Você pode inserir os resultados em uma nova tabela ou retorná-los a um aplicativo.

    ![Conjunto de resultados de execução de procedimento armazenado](media/train-score-using-python-NB-model-results.png)

    Os resultados são 150 previsões sobre espécies usando flores características como entradas. Para a maioria das observações, a espécie prevista corresponde a espécie real.

    Este exemplo foi feito simple usando o conjunto de dados de íris de Python para treinamento e pontuação. Uma abordagem mais típica seria envolver a execução de uma consulta SQL para obter os novos dados e passá-lo em Python como `InputDataSet`. 

## <a name="conclusion"></a>Conclusão

Neste exercício, você aprendeu a criar procedimentos armazenados para tarefas diferentes, onde cada procedimento armazenado usado o procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para iniciar um processo de Python. Entradas para o processo de Python são passadas ao script sp_execute_external como parâmetros. O próprio script de Python e a variáveis de dados em um banco de dados do SQL Server são passadas como entradas.

Se você está acostumado a trabalhar em Python, você talvez esteja acostumado a carregamento de dados, criando alguns resumos e gráficos, em seguida, treinar um modelo e gera algumas classificações em 250 linhas de código a mesma. Este artigo é diferente de abordagens tradicionais, organizando operações em procedimentos separados. Essa prática é útil em vários níveis.

Um benefício é que você pode separar os processos em etapas reprodutíveis que podem ser modificados usando parâmetros. Tanto quanto possível, você deseja que o código do Python que são executados em um procedimento armazenado para tenham definido claramente entradas e saídas que são mapeados para o procedimento armazenado de entradas e saídas que podem ser transmitidas em tempo de execução. Neste exercício, o código do Python que cria um modelo (denominado "Naive Bayes" neste exemplo) é passado como entrada para um segundo procedimento armazenado que chama o modelo em um processo de pontuação.

Um segundo benefício é que o treinamento e pontuação de processos pode ser otimizada, aproveitando os recursos do SQL Server, como o processamento paralelo, governança de recursos, ou usando algoritmos em [revoscalepy](../python/what-is-revoscalepy.md) ou [MicrosoftML ](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) que dão suporte a streaming e execução paralela. Separando o treinamento e pontuação, você pode direcionar otimizações para cargas de trabalho específicas.

## <a name="next-steps"></a>Próximas etapas

Tutoriais anteriores se concentrou em execução local. No entanto, você também pode executar código Python em uma estação de trabalho do cliente, usando o SQL Server como o contexto de computação remota. Para obter mais informações sobre como configurar uma estação de trabalho cliente que se conecta ao SQL Server, consulte [configurar as ferramentas de cliente do Python](../python/setup-python-client-tools-sql.md).

+ [Criar um modelo de revoscalepy de um cliente do Python](use-python-revoscalepy-to-create-model.md)
