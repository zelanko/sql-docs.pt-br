---
title: Usar o modelo de Python no SQL para treinamento e pontuação | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 02ffd5a25c076ef5a65a6e3a998aae485e37d982
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39085018"
---
# <a name="use-python-model-in-sql-for-training-and-scoring"></a>Usar o modelo de Python no SQL para treinamento e pontuação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

No [lição anterior](wrap-python-in-tsql-stored-procedure.md), você aprendeu o padrão comum para usar o Python junto com o SQL. Você aprendeu que o Python, código de saída de um Frame claramente definida e pode, opcionalmente, gerar diversas variáveis escalares ou binárias. Você aprendeu que o procedimento armazenado SQL deve ser projetado para passar o tipo de dados para o Python e lidar com os resultados.

Nesta seção, você deve usa esse mesmo padrão para treinar o modelo nos dados que você adicionou ao SQL Server e salva o modelo em uma tabela do SQL Server:

+ Criar um procedimento armazenado que chama uma função de aprendizado de máquina do Python.
+ O procedimento armazenado precisa de dados do SQL Server para usar no treinamento do modelo.
+ O procedimento armazenado gera um modelo treinado como uma variável binária. 
+ Você pode salvar o modelo treinado, inserindo o modelo de variável em uma tabela. 

## <a name="create-the-stored-procedure-and-train-a-python-model"></a>Criar o procedimento armazenado e treine um modelo de Python

1. Execute o seguinte código no SQL Server Management Studio para criar o procedimento armazenado que cria um modelo.

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

2. Se esse comando for executado sem erro, um novo procedimento armazenado é criado e adicionado ao banco de dados. Você pode encontrar os procedimentos armazenados no Management Studio **Pesquisador de objetos**, em **programação**.

3. Agora execute o procedimento armazenado.

    ```sql
    EXEC generate_iris_model
    ```

    Você deve receber um erro, porque você ainda não forneceu que requer a entrada do procedimento armazenado.

    "Procedimento ou função 'generate_iris_model' espera o parâmetro '\@trained_model', que não foi fornecido."

4. Para gerar o modelo com as entradas necessárias e salve-o em uma tabela requer algumas instruções adicionais:

    ```sql
    DECLARE @model varbinary(max);
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values('Naive Bayes', @model);
    ```

5. Agora, tente executar o código de geração de modelo mais uma vez. 

    Você deve receber o erro: "violação de restrição de chave primária não é possível inserir chave duplicada no objeto 'dbo.iris_models'. O valor de chave duplicada é (Naive Bayes) ".

    Isso ocorre porque o nome do modelo foi fornecido, digitando manualmente no "Bayesiana ingênua" como parte da instrução INSERT. Supondo que você planeja criar muitos modelos, com diferentes parâmetros ou algoritmos diferentes em cada execução, você deve considerar como configurar um esquema de metadados para que você pode nomear automaticamente os modelos e muito mais facilmente identificação-los.

6. Para solucionar esse erro, você pode fazer algumas pequenas modificações para o wrapper SQL. Este exemplo gera um nome exclusivo do modelo por meio do acréscimo de data e hora atuais:

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes ' + CAST(GETDATE()as varchar)
    SELECT @new_model_name 
    EXEC generate_iris_model @model OUTPUT;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    ```

7. Para exibir os modelos, execute uma instrução SELECT simples.

    ```sql
    SELECT * FROM iris_models;
    GO
    ```

    **Resultados**

    |nome_do_modelo | modelo |
    |------|------|
    | Naive Bayes | 0x800363736B6C656172... |
    | Naive Bayes de 01 de janeiro de 2018 39 9H | 0x800363736B6C656172... |
    | Naive Bayes 01 de Feb de 2018 51 10h | 0x800363736B6C656172... |

## <a name="generate-scores-from-the-model"></a>Gerar pontuações do modelo

Por fim, vamos carregar esse modelo da tabela em uma variável e passá-lo de volta para o Python para gerar pontuações.

1. Execute o seguinte código para criar o procedimento armazenado que executa a pontuação. 

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
    OutputDataSet = iris_data.query( ''PredictedSpecies != SpeciesId'' )[[0, 5, 6]]
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

    O procedimento armazenado obtém o modelo de Naïve Bayes da tabela e usa as funções associadas ao modelo para gerar pontuações. Neste exemplo, o procedimento armazenado obtém o modelo da tabela usando o nome do modelo. No entanto, dependendo de qual tipo de metadados que você está salvando com o modelo, você pode também obter o modelo mais recente, ou o modelo com a precisão mais alta.

2. Execute as seguintes linhas para passar o nome do modelo "Bayesiana ingênua" para o procedimento armazenado que executa o código de pontuação. 

    ```sql
    EXEC predict_species 'Naive Bayes';
    GO
    ```

    Quando você executa o procedimento armazenado, ele retorna um Frame do Python. Esta linha de T-SQL Especifica o esquema para os resultados retornados: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`

    Você pode inserir os resultados em uma nova tabela ou retorná-los a um aplicativo.

    Este exemplo foi feito simple, usando os dados do conjunto de dados íris Python para pontuação. (Consulte a linha `iris_data[[1,2,3,4]])`.) No entanto, normalmente você executaria uma consulta SQL para obter os novos dados e passá-lo em Python como `InputDataSet`. 

### <a name="remarks"></a>Remarks

Se você está acostumado a trabalhar em Python, você talvez esteja acostumado a carregamento de dados, criando alguns resumos e gráficos, em seguida, treinar um modelo e gera algumas classificações em 250 linhas de código a mesma.

No entanto, se sua meta é colocar o processo (criação de modelo, pontuação, etc.) no SQL Server, é importante considerar maneiras que você pode separar o processo em etapas reprodutíveis que podem ser modificadas usando parâmetros. Tanto quanto possível, você deseja que o código do Python que são executados em um procedimento armazenado para tenham definido claramente entradas e saídas que são mapeados para o procedimento armazenado de entradas e saídas.

Além disso, você geralmente pode melhorar o desempenho, separando o processo de exploração de dados dos processos de treinamento de um modelo ou geração de pontuações. 

Processos de treinamento e pontuação geralmente podem ser otimizados, aproveitando os recursos do SQL Server, como o processamento paralelo, ou usando algoritmos na [revoscalepy](../python/what-is-revoscalepy.md) ou [MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) esse suporte de streaming e execução paralela, em vez de usar bibliotecas padrão do Python. 

## <a name="next-lesson"></a>Próxima lição

Na última lição, você pode executar código Python de um cliente remoto, usando o SQL Server como o contexto de computação. Esta etapa é opcional, se você não tiver um cliente Python ou não pretende executar Python fora de um procedimento armazenado.

+ [Criar um modelo de revoscalepy de um cliente do Python](use-python-revoscalepy-to-create-model.md)
