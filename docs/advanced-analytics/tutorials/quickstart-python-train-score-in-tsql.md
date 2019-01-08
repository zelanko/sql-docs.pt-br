---
title: Guia de início rápido para modelos de Python para treinamento e previsões usando procedimentos armazenados – Machine Learning do SQL Server
description: Incorpore código Python em procedimentos armazenados do SQL Server para criar, treinar e usar um modelo de Python com o conjunto de dados íris clássico. Salvar um modelo treinado no SQL Server e, em seguida, usá-lo para gerar os resultados previstos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: e8bacc383eba1148c1b357c344bc483e824df99b
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046735"
---
# <a name="quickstart-create-train-and-use-a-python-model-with-stored-procedures-in-sql-server"></a>Guia de início rápido: Criar, treinar e usar um modelo de Python com procedimentos armazenados no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste início rápido usando o Python, você criará e executará os dois procedimentos armazenados. O primeiro usa o conjunto de dados de flor de íris clássico e gera um modelo de Naïve Bayes para prever uma espécie de íris com base nas características da flor. É o segundo procedimento para pontuação. Ele chama o modelo gerado no primeiro procedimento para um conjunto de previsões de saída. Colocando o código em um procedimento armazenado, as operações são independentes, reutilizáveis e que pode ser chamado por outros procedimentos armazenados e os aplicativos cliente. 

Ao concluir este início rápido, você aprenderá:

> [!div class="checklist"]
> * Como incorporar código Python em um procedimento armazenado
> * Como passar entradas para seu código por meio de entradas no procedimento armazenado
> * Como os procedimentos armazenados são usados para operacionalizar os modelos

## <a name="prerequisites"></a>Prerequisites

Um início rápido anterior, [Python Verifique se existe no SQL Server](quickstart-python-verify.md), fornece informações e links para configurar o ambiente do Python necessário para este início rápido.

Os dados de exemplo usados neste exercício são o [ **irissql** ](demo-data-iris-in-sql.md) banco de dados.

## <a name="create-a-stored-procedure-that-generates-models"></a>Criar um procedimento armazenado que gera modelos

Um padrão comum no desenvolvimento do SQL Server é organizar programáveis operações em procedimentos armazenados distintos. Nesta etapa, você criará um procedimento armazenado que gera um modelo para prever resultados. 

1. Abra uma nova janela de consulta no Management Studio, conectado para o **irissql** banco de dados. 

    ```sql
    USE irissql
    GO
    ```

2. Copie o código a seguir para criar um novo procedimento armazenado. 

   Quando executado, esse procedimento chama [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) para iniciar uma sessão de Python. 
   
   Entradas exigidas pelo seu código de Python são passadas como parâmetros de entrada sobre esse procedimento armazenado. Saída será um modelo treinado, com base em Python **scikit-Saiba** biblioteca para o algoritmo de aprendizado de máquina. 

   Esse código usa [ **pickle** ](https://docs.python.org/2/library/pickle.html) para serializar o modelo. O modelo será treinado usando dados de colunas de 0 a 4 dos **iris_data** tabela. 
   
   Os parâmetros que você pode ver na segunda parte do procedimento articulam entradas de dados e saídas de modelo. Tanto quanto possível, você deseja que o código do Python em execução em um procedimento armazenado para definiram claramente as entradas e saídas que são mapeados para o procedimento armazenado de entradas e saídas passadas em tempo de execução. 

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model varbinary(max) OUTPUT)
    AS
    BEGIN
    EXEC sp_execute_external_script @language = N'Python',
    @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]].values.ravel()))
    '
    , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
    , @input_data_1_name = N'iris_data'
    , @params = N'@trained_model varbinary(max) OUTPUT'
    , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

3. Verifique se que o procedimento armazenado existe. 

   Se o script T-SQL da etapa anterior for executado sem erro, um novo procedimento armazenado chamado **generate_iris_model** é criado e adicionado para o **irissql** banco de dados. Você pode encontrar os procedimentos armazenados no Management Studio **Pesquisador de objetos**, em **programação**.

## <a name="execute-the-procedure-to-create-and-train-models"></a>Execute o procedimento para criar e treinar modelos

Nesta etapa, execute o procedimento para executar o código incorporado, criando um modelo treinado e serializado como saída. Modelos que são armazenados para reutilização no SQL Server são serializados como um fluxo de bytes e armazenados em uma coluna varbinary (max) em uma tabela de banco de dados. Depois que o modelo é criado, treinado, serializado e salvos em um banco de dados, ele pode ser chamado por outros procedimentos ou pelo [PREVER T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) função em cargas de trabalho de pontuação.

1. Copie o código a seguir para executar o procedimento. A instrução específica para executar um procedimento armazenado é `EXEC` na quinta linha.

   Esse script em particular exclui um modelo existente de mesmo nome ("Bayesiana ingênua") para liberar espaço para novos criados executando novamente o mesmo procedimento. Sem exclusão do modelo, ocorrerá um erro informando que o objeto já existe. O modelo é armazenado em uma tabela chamada **iris_models**, provisionado quando você criou o **irissql** banco de dados.

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXEC generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

2. Verifique se o modelo foi inserido é outra maneira de retornar uma lista de modelos

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **Resultados**

    | nome_do_modelo  | modelo |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>Criar e executar um procedimento armazenado para gerar previsões

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

Neste exercício, você aprendeu a criar procedimentos armazenados dedicados para tarefas diferentes, onde cada procedimento armazenado usado o procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para iniciar um processo de Python. Entradas para o processo de Python são passadas ao script sp_execute_external como parâmetros. O próprio script de Python e a variáveis de dados em um banco de dados do SQL Server são passadas como entradas.

Em geral, você só deve planejar usando o SSMS com o código do Python bem acabado ou código Python simples que retorna a saída com base em linha. Como uma ferramenta, o SSMS dá suporte a linguagens como T-SQL de consulta e retorna conjuntos de linhas bidimensionais. Se seu código gera a saída do visual como um gráfico disperso ou histograma, você precisa de um aplicativo de ferramenta ou do usuário final que pode renderizar a imagem.

Para alguns desenvolvedores de Python que são usados para escrever script completo manipular uma variedade de operações, organizar tarefas em procedimentos separados pode parecer desnecessário. Mas, treinamento e pontuação têm diferentes casos de uso. Separando-os, você pode colocar cada tarefa na agenda diferente e permissões no escopo para a operação.

Da mesma forma, você também pode aproveitar recursos de obtenção de recursos do SQL Server, como o processamento paralelo, governança de recursos, ou escrevendo em seu script para usar algoritmos em [revoscalepy](../python/ref-py-revoscalepy.md) ou [microsoftml](../python/ref-py-microsoftml.md) que suporte de streaming e a execução paralela. Separando o treinamento e pontuação, você pode direcionar otimizações para cargas de trabalho específicas.

Uma vantagem final é que os processos podem ser modificados usando parâmetros. Neste exercício, o código do Python que criou o modelo (chamado "Bayesiana ingênua" neste exemplo) foi passado como entrada para um segundo procedimento armazenado que chamar o modelo em um processo de pontuação. Este exercício usa apenas um modelo, mas você pode imaginar como parametrizar o modelo em uma tarefa de pontuação seria tornar esse script mais úteis.

## <a name="next-steps"></a>Próximas etapas

Se você for novo no Python de desenvolvedor SQL, examine as etapas e ferramentas para trabalhar com o código do Python localmente, com a capacidade de mudar a execução de sessões locais para uma instância remota do SQL Server.

> [!div class="nextstepaction"]
> [Configurar uma estação de trabalho de cliente do Python](../python/setup-python-client-tools-sql.md).

