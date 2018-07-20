---
title: Guia de início rápido para criar um modelo de previsão usando o R no SQL Server Machine Learning | Microsoft Docs
description: Neste início rápido, saiba como criar um modelo em R usando dados do SQL Server para plotar previsões.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7ca2fcac5bef63a4abf2449b56c25a600b9255c3
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086818"
---
# <a name="quickstart-create-a-predictive-model-using-r-in-sql-server"></a>Início rápido: Criar um modelo de previsão usando R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste início rápido, você aprenderá a treinar um modelo usando R e, em seguida, salvar o modelo em uma tabela no SQL Server. O modelo é um modelo de regressão simples que prevê a distância de parada de um carro com base na velocidade. Você usará o `cars` conjunto de dados incluído com o R, porque ele é pequeno e fácil de entender.

## <a name="prerequisites"></a>Prerequisites

Um início rápido anterior, [Olá, mundo em R e SQL](rtsql-using-r-code-in-transact-sql-quickstart.md), fornece informações e links para configurar o ambiente de R necessários para este início rápido.

## <a name="create-the-source-data"></a>Criar os dados de origem

Primeiro, crie uma tabela para salvar os dados de treinamento.

```sql
CREATE TABLE CarSpeed ([speed] int not null, [distance] int not null)
INSERT INTO CarSpeed
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'car_speed <- cars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'car_speed'
```

+ Algumas pessoas gostam de usar tabelas temporárias, mas lembre-se de que alguns clientes do R desconectar sessões entre os lotes.

+ Vários conjuntos de dados, pequenos e grandes, estão incluídos com o tempo de execução de R. Para obter uma lista de conjuntos de dados instalados com o R, digite `library(help="datasets")` em um prompt de comando de R.

## <a name="create-a-regression-model"></a>Criar um modelo de regressão

Os dados de velocidade do carro contêm duas colunas, ambas numéricas, `dist` e `speed`. Há várias observações de alguns velocidades. Com base nesses dados, você criará um modelo de regressão linear que descreve alguma relação entre a velocidade do carro e a distância necessário para parar um carro.

Os requisitos de um modelo linear são simples:

+ Definir uma fórmula que descreve a relação entre a variável dependente `speed` e a variável independente `distance`

+ Fornecer dados de entrada para usar no treinamento do modelo

> [!TIP]
> Se você precisar de um lembrete sobre modelos lineares, recomendamos que este tutorial, que descreve o processo de ajuste de um modelo usando o rxLinMod: [modelos lineares de ajuste](https://docs.microsoft.com/r-server/r/how-to-revoscaler-linear-model)

Para realmente criar o modelo, você define a fórmula dentro de seu código R e passa os dados como um parâmetro de entrada.

```sql
DROP PROCEDURE IF EXISTS generate_linear_model;
GO
CREATE PROCEDURE generate_linear_model
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'lrmodel <- rxLinMod(formula = distance ~ speed, data = CarsData);
        trained_model <- data.frame(payload = as.raw(serialize(lrmodel, connection=NULL)));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model varbinary(max)));
END;
GO
```

+ O primeiro argumento para o rxLinMod é o parâmetro *fórmula*, que define a distância como dependente da velocidade.
+ Os dados de entrada são armazenados na variável `CarsData`, preenchido pela consulta SQL. Se você não atribuir um nome específico aos seus dados de entrada, o nome da variável padrão seria _InputDataSet_.

## <a name="create-a-table-for-storing-the-model"></a>Criar uma tabela para armazenar o modelo

Em seguida, armazene o modelo para que você possa treinar novamente ou usá-lo para previsão. A saída de um pacote de R que cria um modelo é geralmente um **objeto binário**. Portanto, a tabela em que você armazena o modelo deve fornecer uma coluna do tipo **varbinary**.

```sql
CREATE TABLE stopping_distance_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null);
```

## <a name="save-the-model"></a>Salvar o modelo

Para salvar o modelo, execute a seguinte instrução Transact-SQL para chamar o procedimento armazenado, gerar o modelo e salvá-lo em uma tabela.

```sql
INSERT INTO stopping_distance_models (model)
EXEC generate_linear_model;
```

Observe que, se você executar esse código uma segunda vez, você receber esse erro:

```
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

Uma opção para evitar esse erro é atualizar o nome de cada novo modelo. Por exemplo, seria possível alterar o nome para algo mais descritivo e incluir o tipo de modelo, o dia da criação e assim por diante.

```sql
UPDATE stopping_distance_models
SET model_name = 'rxLinMod ' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="output-additional-variables"></a>Variáveis de saída adicionais

Normalmente, a saída do R do procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) é limitada a um único quadro de dados. (Essa limitação poderá ser removida no futuro.)

No entanto, é possível retornar saídas de outros tipos, como escalares, além do quadro de dados.

Por exemplo, suponha que você deseja treinar um modelo, mas exibir imediatamente uma tabela de coeficientes do modelo. Seria possível criar a tabela de coeficientes como o principal conjunto de resultados e transmitir o modelo treinado em uma variável SQL. Você imediatamente poderia usar novamente o modelo ao chamar a variável, ou pode salvar o modelo em uma tabela, conforme mostrado aqui.

```sql
DECLARE @model varbinary(max), @modelname varchar(30)
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
        speedmodel <- rxLinMod(distance ~ speed, CarsData)
        modelbin <- serialize(speedmodel, NULL)
        OutputDataSet <- data.frame(coefficients(speedmodel));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @params = N'@modelbin varbinary(max) OUTPUT'
    , @modelbin = @model OUTPUT
    WITH RESULT SETS (([Coefficient] float not null));

-- Save the generated model
INSERT INTO [dbo].[stopping_distance_models] (model_name, model)
VALUES ('latest model', @model)
```

**Resultados**

![rslq_basictut_coefficients](media/rslq-basictut-coefficients.PNG)

### <a name="summary"></a>Resumo

Lembre-se dessas regras para trabalhar com parâmetros SQL e variáveis do R em `sp_execute_external_script`:

+ Todos os parâmetros SQL mapeados para o script R devem ser listados por nome na  _\@params_ argumento.
+ A saída de um desses parâmetros, adicione a palavra-chave OUTPUT na  _\@params_ lista.
+ Depois de listar os parâmetros mapeados, forneça o mapeamento, linha por linha, dos parâmetros SQL para variáveis do R, imediatamente após o  _\@params_ lista.

## <a name="next-steps"></a>Próximas etapas

Agora que você tem um modelo, o guia de início rápido final, você aprenderá a gerar previsões com base nele e plotar os resultados.

> [!div class="nextstepaction"]
> [Guia de início rápido: Prever e plotar com base no modelo](../tutorials/rtsql-predict-and-plot-from-model.md)