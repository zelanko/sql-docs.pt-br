---
title: Criar e pontuar um modelo de previsão no Python
titleSuffix: SQL Server Machine Learning Services
description: Crie um modelo de previsão simples no Python usando SQL Server Serviços de Machine Learning e, em seguida, preveja um resultado usando novos dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/14/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cb564d7dc8564b31a90a09f53aedaba953519f76
ms.sourcegitcommit: c7a202af70fd16467a498688d59637d7d0b3d1f3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313670"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-python-with-sql-server-machine-learning-services"></a>Início Rápido: Criar e pontuar um modelo de previsão em Python com SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste guia de início rápido, você criará e treinará um modelo de previsão usando o Python, salvará o modelo em uma tabela em sua instância de SQL Server e, em seguida, usará o modelo para prever valores de novos dados usando [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md).

Você criará e executará dois procedimentos armazenados em execução no SQL. A primeira usa o conjunto de dados de flor de íris clássico e gera um modelo de Bayes simples para prever uma espécie de íris com base nas características da flor. O segundo procedimento é para Pontuação-ele chama o modelo gerado no primeiro procedimento para gerar um conjunto de previsões com base em novos dados. Ao colocar o código em um procedimento armazenado, as operações são contidas, reutilizáveis e podem ser chamadas por outros procedimentos armazenados e aplicativos cliente.

Ao concluir este guia de início rápido, você aprenderá:

> [!div class="checklist"]
> - Como inserir código Python em um procedimento armazenado
> - Como passar entradas para seu código por meio de entradas no procedimento armazenado
> - Como os procedimentos armazenados são usados para colocar os modelos em operação

## <a name="prerequisites"></a>Pré-requisitos

- Este início rápido requer acesso a uma instância do SQL Server com [SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) com a linguagem Python instalada.

- Você também precisa de uma ferramenta para executar consultas SQL que contêm scripts Python. Você pode executar esses scripts usando qualquer ferramenta de consulta ou gerenciamento de banco de dados, desde que ele possa se conectar a uma instância de SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Este início rápido usa o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

- Os dados de exemplo usados neste exercício são os dados de exemplo da íris. Siga as instruções em [dados de demonstração da íris](demo-data-iris-in-sql.md) para criar o banco de dado de exemplo **irissql**.

## <a name="create-a-stored-procedure-that-generates-models"></a>Criar um procedimento armazenado que gera modelos

Nesta etapa, você criará um procedimento armazenado que gera um modelo para prever resultados.

1. Abra uma nova janela de consulta no SSMS conectado ao banco de dados **irissql** . 

    ```sql
    USE irissql
    GO
    ```

1. Copie no código a seguir para criar um novo procedimento armazenado.

   Quando executado, esse procedimento chama [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para iniciar uma sessão do Python. 
   
   As entradas necessárias para seu código Python são passadas como parâmetros de entrada neste procedimento armazenado. A saída será um modelo treinado, com base na Biblioteca Python **scikit-Learn** para o algoritmo de aprendizado de máquina. 

   Esse código usa [**pickle**](https://docs.python.org/2/library/pickle.html) para serializar o modelo. O modelo será treinado usando dados das colunas 0 a 4 da tabela **iris_data** . 
   
   Os parâmetros que você vê na segunda parte do procedimento articulam entradas de dados e saídas de modelo. Tanto quanto possível, você quer que o código Python em execução em um procedimento armazenado tenha entradas e saídas claramente definidas que mapeiam para entradas de procedimento armazenado e saídas passadas em tempo de execução.

    ```sql
    CREATE PROCEDURE generate_iris_model (@trained_model VARBINARY(max) OUTPUT)
    AS
    BEGIN
        EXECUTE sp_execute_external_script @language = N'Python'
            , @script = N'
    import pickle
    from sklearn.naive_bayes import GaussianNB
    GNB = GaussianNB()
    trained_model = pickle.dumps(GNB.fit(iris_data[["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]], iris_data[["SpeciesId"]].values.ravel()))
    '
            , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
            , @input_data_1_name = N'iris_data'
            , @params = N'@trained_model varbinary(max) OUTPUT'
            , @trained_model = @trained_model OUTPUT;
    END;
    GO
    ```

1. Verifique se o procedimento armazenado existe. 

   Se o script T-SQL da etapa anterior foi executado sem erro, um novo procedimento armazenado chamado **generate_iris_model** será criado e adicionado ao banco de dados **irissql** . Você pode encontrar procedimentos armazenados no **pesquisador de objetos**do SSMS, em **programação**.

## <a name="execute-the-procedure-to-create-and-train-models"></a>Executar o procedimento para criar e treinar modelos

Nesta etapa, você executa o procedimento para executar o código inserido, criando um modelo treinado e serializado como uma saída. 

Os modelos que são armazenados para reutilização em SQL Server são serializados como um fluxo de bytes e armazenados em uma coluna VARBINARY (MAX) em uma tabela de banco de dados. Depois que o modelo é criado, treinado, serializado e salvo em um banco de dados, ele pode ser chamado por outros procedimentos ou pela função de [previsão do T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) nas cargas de trabalho de pontuação.

1. Execute o script a seguir para executar o procedimento. A instrução específica para executar um procedimento armazenado é `EXECUTE` na quarta linha.

   Esse script específico exclui um modelo existente de mesmo nome ("Naive Bayes") para liberar espaço para os novos criados executando novamente o mesmo procedimento. Sem a exclusão do modelo, ocorre um erro informando que o objeto já existe. O modelo é armazenado em uma tabela chamada **iris_models**, provisionado quando você criou o banco de dados **irissql** .

    ```sql
    DECLARE @model varbinary(max);
    DECLARE @new_model_name varchar(50)
    SET @new_model_name = 'Naive Bayes'
    EXECUTE generate_iris_model @model OUTPUT;
    DELETE iris_models WHERE model_name = @new_model_name;
    INSERT INTO iris_models (model_name, model) values(@new_model_name, @model);
    GO
    ```

1. Verifique se o modelo foi inserido.

    ```sql
    SELECT * FROM dbo.iris_models
    ```

    **Resultados**

    | model_name  | modelo |
    |---|-----------------|
    | Naive Bayes | 0x800363736B6C6561726E2E6E616976655F62617965730A... | 

## <a name="create-and-execute-a-stored-procedure-for-generating-predictions"></a>Criar e executar um procedimento armazenado para gerar previsões

Agora que você criou, treinau e salvou um modelo, passe para a próxima etapa: Criando um procedimento armazenado que gera previsões. Você fará isso chamando `sp_execute_external_script` para executar um script Python que carrega o modelo serializado e fornece novas entradas de dados a serem pontuadas.

1. Execute o código a seguir para criar o procedimento armazenado que executa a pontuação. Em tempo de execução, esse procedimento carregará um modelo binário, usará colunas `[1,2,3,4]` como entradas e especificar colunas `[0,5,6]` como saída.

   ```sql
   CREATE PROCEDURE predict_species (@model VARCHAR(100))
   AS
   BEGIN
       DECLARE @nb_model VARBINARY(max) = (
               SELECT model
               FROM iris_models
               WHERE model_name = @model
               );
   
       EXECUTE sp_execute_external_script @language = N'Python'
           , @script = N'
   import pickle
   irismodel = pickle.loads(nb_model)
   species_pred = irismodel.predict(iris_data[["Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width"]])
   iris_data["PredictedSpecies"] = species_pred
   OutputDataSet = iris_data[["id","SpeciesId","PredictedSpecies"]] 
   print(OutputDataSet)
   '
           , @input_data_1 = N'select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "SpeciesId" from iris_data'
           , @input_data_1_name = N'iris_data'
           , @params = N'@nb_model varbinary(max)'
           , @nb_model = @nb_model
       WITH RESULT SETS((
                   "id" INT
                 , "SpeciesId" INT
                 , "SpeciesId.Predicted" INT
                   ));
   END;
   GO
   ```

2. Execute o procedimento armazenado, fornecendo o nome do modelo "Naive Bayes" para que o procedimento saiba qual modelo usar.

   ```sql
   EXECUTE predict_species 'Naive Bayes';
   GO
   ```

   Quando você executa o procedimento armazenado, ele retorna um data. frame do Python. Essa linha de T-SQL especifica o esquema para os resultados retornados: `WITH RESULT SETS ( ("id" int, "SpeciesId" int, "SpeciesId.Predicted" int));`. Você pode inserir os resultados em uma nova tabela ou retorná-los a um aplicativo.

   ![Conjunto de resultados da execução do procedimento armazenado](media/train-score-using-python-NB-model-results.png)

   Os resultados são 150 previsões sobre espécies usando características floral como entradas. Para a maioria das observações, as espécies previstas correspondem à espécie real.

   Este exemplo foi simplificado com o uso do conjunto de pontos do Python íris para treinamento e pontuação. Uma abordagem mais comum envolveria a execução de uma consulta SQL para obter os novos dados e passá-lo para o Python como `InputDataSet`.

## <a name="conclusion"></a>Conclusão

Neste exercício, você aprendeu a criar procedimentos armazenados dedicados a tarefas diferentes, em que cada procedimento armazenado usou o procedimento armazenado do sistema `sp_execute_external_script` para iniciar um processo do Python. As entradas para o processo do Python são passadas para `sp_execute_external` como parâmetros. O próprio script do Python e as variáveis de dados em um banco SQL Server dados são passados como entradas.

Em geral, você deve planejar apenas o uso do SSMS com código Python elegante ou um código Python simples que retorna a saída baseada em linha. Como uma ferramenta, o SSMS dá suporte a linguagens de consulta como T-SQL e retorna conjuntos de linhas mescladas. Se o código gerar uma saída Visual como um dispersão ou histograma, você precisará de uma ferramenta ou aplicativo de usuário final que possa renderizar a imagem.

Para alguns desenvolvedores de Python que são usados para escrever um tratamento de script completo, uma variedade de operações, organizar tarefas em procedimentos separados pode parecer desnecessário. Mas o treinamento e a pontuação têm casos de uso diferentes. Separando-os, você pode colocar cada tarefa em um agendamento e permissões de escopo diferentes para cada operação.

Da mesma forma, você também pode aproveitar os recursos de origem do SQL Server, como processamento paralelo, governança de recursos ou escrevendo seu script para usar algoritmos em [microsoftml](../python/ref-py-microsoftml.md) que dão suporte a streaming e execução paralela. Ao separar o treinamento e a pontuação, você pode direcionar otimizações para cargas de trabalho específicas.

Um benefício final é que os processos podem ser modificados usando parâmetros. Neste exercício, o código Python que criou o modelo (chamado "Naive Bayes" neste exemplo) foi passado como uma entrada para um segundo procedimento armazenado que chama o modelo em um processo de pontuação. Este exercício usa apenas um modelo, mas você pode imaginar como a parametrização do modelo em uma tarefa de Pontuação tornaria esse script mais útil.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre SQL Server Serviços de Machine Learning, consulte:

- [O que é SQL Server Serviços de Machine Learning (Python e R)?](../what-is-sql-server-machine-learning.md)
