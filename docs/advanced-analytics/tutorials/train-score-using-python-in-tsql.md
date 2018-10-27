---
title: Modelos do Python no SQL Server para treinamento e previsões usando procedimentos armazenados | Microsoft Docs
description: Incorpore código Python em procedimentos armazenados do SQL Server para criar, treinar e usar um modelo de Python com o conjunto de dados íris clássico. Salvar um modelo treinado no SQL Server e, em seguida, usá-lo para gerar os resultados previstos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/23/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 3cdab7ab26166392724ee278cbaf76afd68b9472
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50099859"
---
# <a name="create-train-and-use-a-python-model-with-stored-procedures-in-sql-server"></a>Criar, treinar e usar um modelo de Python com procedimentos armazenados no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esse exercício demonstra a integração do Python com o SQL Server quando você adiciona o [serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) recurso para uma instância do mecanismo de banco de dados. Na instância, você pode encapsular o código do Python dentro de um [procedimento armazenado](../../relational-databases/stored-procedures/stored-procedures-database-engine.md) operacionalizar seu script para cargas de trabalho de produção. A capacidade de incorporar o código em um procedimento armazenado tem benefícios tangíveis em como projetar, testar e gerenciar tarefas de aprendizado de máquina e ciência de dados. Ele torna seu script e modelos acessíveis para qualquer aplicativo que pode se conectar ao SQL Server.

Neste exercício de Python, você criará e executará os dois procedimentos armazenados. O primeiro usa o conjunto de dados de flor de íris clássico e gera um modelo de Naïve Bayes para prever uma espécie de íris com base nas características da flor. É o segundo procedimento para pontuação. Ele chama o modelo gerado no primeiro procedimento para um conjunto de previsões de saída. Colocando o código em um procedimento armazenado, as operações são independentes, reutilizáveis e que pode ser chamado por outros procedimentos armazenados e os aplicativos cliente. 

Ao concluir este tutorial, você aprenderá:

> [!div class="checklist"]
> * Como incorporar código Python em um procedimento armazenado
> * Como passar entradas para seu código por meio de entradas no procedimento armazenado
> * Como os procedimentos armazenados são usados para operacionalizar os modelos

## <a name="prerequisites"></a>Prerequisites

Dados de exemplo usados neste exercício são o [ **irissql** ](demo-data-iris-in-sql.md) banco de dados.

Você também precisa de um editor T-SQL, tais como [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-2017).

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
    trained_model = pickle.dumps(GNB.fit(iris_data[[0,1,2,3]], iris_data[[4]]))
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

Para alguns desenvolvedores de Python que são usados para escrever script completo manipular uma variedade de operações, organizar tarefas em procedimentos separados pode parecer desnecessário. Mas, treinamento e pontuação têm diferentes casos de uso. Separando-os, você pode colocar cada tarefa na agenda diferente e permissões no escopo para a operação.

Da mesma forma, você também pode aproveitar recursos de obtenção de recursos do SQL Server, como o processamento paralelo, governança de recursos, ou escrevendo em seu script para usar algoritmos em [revoscalepy](../python/what-is-revoscalepy.md) ou [MicrosoftML](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) que suporte de streaming e a execução paralela. Separando o treinamento e pontuação, você pode direcionar otimizações para cargas de trabalho específicas.

Uma vantagem final é que os processos podem ser modificados usando parâmetros. Neste exercício, o código do Python que criou o modelo (chamado "Bayesiana ingênua" neste exemplo) foi passado como entrada para um segundo procedimento armazenado que chamar o modelo em um processo de pontuação. Este exercício usa apenas um modelo, mas você pode imaginar como parametrizar o modelo em uma tarefa de pontuação seria tornar esse script mais úteis.


## <a name="next-steps"></a>Próximas etapas

Tutoriais anteriores se concentrou em execução local. No entanto, você também pode executar código Python em uma estação de trabalho do cliente, usando o SQL Server como o contexto de computação remota. Para obter mais informações sobre como configurar uma estação de trabalho cliente que se conecta ao SQL Server, consulte [configurar as ferramentas de cliente do Python](../python/setup-python-client-tools-sql.md).

+ [Criar um modelo de revoscalepy de um cliente do Python](use-python-revoscalepy-to-create-model.md)
