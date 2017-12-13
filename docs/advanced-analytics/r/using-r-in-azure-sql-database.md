---
title: Usando o R no banco de dados SQL do Azure | Microsoft Docs
ms.custom: 
ms.date: 12/08/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: cb43b2c1edb6ce03acd2e3e64eb077ca96c62304
ms.sourcegitcommit: 05e2814fac4d308196b84f1f0fbac6755e8ef876
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2017
---
# <a name="using-r-in-azure-sql-database"></a>Usando o R no banco de dados SQL do Azure

Em outubro de 2017, a equipe de desenvolvimento do SQL Server anunciou planos para permitir a execução de R código no banco de dados usando procedimentos armazenados, semelhantes aos serviços do R no SQL Server 2016. 

Para manter atualizado sobre o agendamento de lançamento e eventos futuros, consulte o [blog do SQL Server](https://blogs.technet.microsoft.com/dataplatforminsider/) ou [blog do Microsoft R Server](https://blogs.msdn.microsoft.com/rserver/).

> [!IMPORTANT]
> No momento, a visualização de suporte de R está disponível no banco de dados SQL Azure no Oeste Central dos EUA e recursos estão limitados em comparação com os recursos de R e execução no SQL Server 2016 ou 2017 de código do Python.

## <a name="whats-included"></a>O que está incluído

A funcionalidade de R no banco de dados pode ser usada nos seguintes níveis de serviço de banco de dados e níveis de desempenho:
 
- Camada de serviço Premium – P1, P2, P4, P6, P11, P15
- Premium serviço RS camada – PRS1, PRS2, PRS4, PRS6
- Pool Elástico Premium – 125 eDTUs ou maior
- Pool de RS Elástico Premium – 125 eDTUs ou maior

A versão de visualização inclui esses pacotes:

+   Microsoft R Open com R versão 3.3.3
+   Funções e pacotes de base R são pré-instaladas
+   Microsoft R Server 9.2, incluindo o pacote RevoScaleR

Na versão de visualização atual, você pode executar as seguintes tarefas:

+ Treinamento de modelos, usando todos os dados que couber na memória
+   Pontuação de modelos, usando todos os dados que couber na memória
+   Paralelismo trivial para execução do Script de R (usando o @parallel parâmetro em sp_execute_external_script)
+   Fluxo de execução para a execução do Script de R (usando @r_RowsPerRead parâmetro em sp_execute_external_script)
+   Executar um único script R de uma só vez


As tarefas a seguir não têm suporte na versão de visualização do R no banco de dados do SQL Azure:

+ Não é possível habilitar a execução de script R em bancos de dados específicos.
+ DMVs fornecido para o monitor de CPU e uso de memória de scripts R não estão disponíveis.
+ Não há pacotes de terceiros podem ser instalados. Não há suporte para a instrução Criar biblioteca externa.

## <a name="example"></a>Exemplo

No banco de dados de SQL do Azure, todos os comandos de R são executados do T-SQL, usando o procedimento armazenado [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). 

O exemplo a seguir demonstra como testar o recurso de visualização, usando o conjunto de dados iris incluído no r base.

### <a name="step-1-create-the-data-tables"></a>Etapa 1. Criar as tabelas de dados

Comece criando duas tabelas: uma para armazenar os dados de origem extraídos de R e outra para armazenar o modelo treinado.

```sql
DROP TABLE IF EXISTS iris_data, iris_models;
GO
CREATE TABLE iris_data (
        id INT NOT NULL IDENTITY PRIMARY KEY
        , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
        , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
        , "Species" VARCHAR(100) NULL
);
CREATE TABLE iris_models (
    model_name VARCHAR(30) NOT NULL PRIMARY KEY,
    model VARBINARY(max) NOT NULL,
    native_model VARBINARY(MAX) NOT NULL
);
GO
```

### <a name="step-2-populate-table-with-data-from-the-iris-dataset"></a>Etapa 2. Preencha a tabela com dados do conjunto de dados iris

Depois que as tabelas foram criadas, execute o seguinte código para inserir dados de treinamento na tabela. O procedimento armazenado sp_execute_external_script chama R e retorna o conjunto de dados iris como um quadro de dados, usando o esquema especificado na instrução INSERT INTO.

```sql
INSERT INTO iris_data
("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
EXEC sp_execute_external_script @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

### <a name="step-3-create-the-stored-procedure-that-generates-the-model"></a>Etapa 3. Criar o procedimento armazenado que gera o modelo

O procedimento armazenado a seguir executa o trabalho, na verdade, criar e treinar o modelo, que pode ser salvo em qualquer um dos dois formatos binários.

```sql
CREATE PROCEDURE generate_iris_model (@trained_model VARBINARY(MAX) OUTPUT, @native_trained_model VARBINARY(MAX) OUTPUT
AS
BEGIN
  EXEC sp_execute_external_script @language = N'R'
    , @script = N'
    iris_model <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris_rx_data);
    trained_model <- as.raw(serialize(iris_model, connection=NULL));
    native_trained_model <- rxSerializeModel(iris_model, realtimeScoringOnly = TRUE)
    '
  , @input_data_1 = N'SELECT "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@trained_model VARBINARY(MAX) OUTPUT, @native_trained_model VARBINARY(MAX) OUTPUT'
    , @trained_model = @trained_model OUTPUT
```

+ O **saída** palavra-chave em parâmetros de entrada indica que os valores devem ser passados e usados para a saída também.
+ A linha que começa com `iris_model` define um modelo de árvore de decisão para prever espécies com base em atributos de flor.
+ A chamada para `serialize` salva o modelo em um formato binário adequado para armazenamento no SQL Server. 
+ Como alternativa, com modelos com base em algoritmos de RevoScaleR, você pode usar o [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) função, que salva o modelo em um novo formato binário nativo. Os modelos salvos nesse formato podem ser carregados para pontuação com a função de previsão no SQL Server.

### <a name="step-4-train-and-save-the-model"></a>Etapa 4. Treinar e salvar o modelo

Tendo criado o procedimento armazenado, chamá-lo para processar dados de entrada e cria um modelo. O código a seguir também salva o modelo na tabela **iris_models**, de modo que você pode usá-lo posteriormente para prever a espécie de flor.

```sql
DECLARE @model VARBINARY(MAX), @native_modelVARBINARY(MAX);
EXEC generate_iris_model @model OUTPUT, @native_model OUTPUT;
DELETE FROM iris_models WHERE model_name = 'iris.dtree';
INSERT INTO iris_models (model_name, model, native_model) VALUES('iris.dtree', @model, @native_model);
SELECT model_name, datalength(model)/1024. AS model_size_kb, datalength(native_model)/1024. AS native_model_size_kb FROM iris_models;
GO
```

### <a name="step-5-create-a-stored-procedure-for-scoring"></a>Etapa 5. Criar um procedimento armazenado para pontuação

Em seguida, crie um procedimento armazenado para pontuação. Esse procedimento armazenado carrega um modelo especificado da tabela e cria pontuações com base em dados de entrada.

```sql
CREATE PROCEDURE predict_iris_species (@model varchar(100))
AS
BEGIN
  DECLARE @rx_model VARBINARY(MAX) = (SELECT model FROM iris_models WHERE model_name = @model);
  EXEC sp_execute_external_script @language = N'R'
  , @script = N'
    irismodel<-unserialize(rx_model);
    OutputDataSet <-rxPredict(irismodel, iris_rx_data, extraVarsToWrite = c("Species", "id"));
      '
  , @input_data_1 = N'SELECT "id", "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@rx_model varbinary(max)'
  , @rx_model = @rx_model
  WITH RESULT SETS ( ("setosa_Pred" FLOAT, "versicolor_Pred" FLOAT, "virginica_Pred" FLOAT, "Species.Actual" VARCHAR(100), "id" INT));
END;
GO
```

Este armazenado procedimento usa o [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) função, mas você também pode usar a função de previsão nativa em T-SQL conforme mostrado [aqui](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-general-availability-of-native-scoring-using-predict-function-in-azure-sql-database/). Uso da função de previsão exige que você use um [ **rx** modelo](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler) e salve o modelo usando [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel).

### <a name="step-6-use-the-stored-procedure-to-generate-predictions"></a>Etapa 6. Use o procedimento armazenado para gerar previsões

Para gerar pontuações do modelo, execute o procedimento armazenado. Você pode inserir os valores em uma tabela ou retornar as previsões para um aplicativo de chamada.

```sql
EXEC predict_iris_species 'iris.dtree';
GO
```

## <a name="related-resources"></a>Recursos relacionados

O Marketplace do Azure também fornece várias máquinas virtuais que incluem 2017 do SQL Server:

+ [Provisionar uma máquina virtual para o aprendizado de máquina do Azure](provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

Confira também nessas máquinas virtuais que vêm pré-configurados com uma variedade de ferramentas de aprendizado de máquina conhecida:

+ [Máquinas virtuais de ciência de dados](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)
+ [Máquina Virtual de aprendizado](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)

