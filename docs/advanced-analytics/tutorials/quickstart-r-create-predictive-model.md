---
title: Guia de início rápido para criar um modelo de previsão usando o R - aprendizagem de máquina do SQL Server
description: Neste início rápido, saiba como criar um modelo em R usando dados do SQL Server para plotar previsões.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: f1eaa39e5f22efbe7bea7a44ac2ce93a5e28205e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962035"
---
# <a name="quickstart-create-a-predictive-model-using-r-in-sql-server"></a>Início Rápido: Criar um modelo de previsão usando R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste início rápido, você aprenderá a treinar um modelo usando R e, em seguida, salvar o modelo em uma tabela no SQL Server. O modelo é um simple modelo linear generalizado (GLM) que prevê a probabilidade de que um veículo ajustá-los com uma transmissão manual. Você usará o `mtcars` conjunto de dados incluído com o R.

## <a name="prerequisites"></a>Pré-requisitos

Um início rápido anterior, [R Verifique se existe no SQL Server](quickstart-r-verify.md), fornece informações e links para configurar o ambiente de R necessários para este início rápido.

## <a name="create-the-source-data"></a>Criar os dados de origem

Primeiro, crie uma tabela para salvar os dados de treinamento.

```sql
CREATE TABLE dbo.MTCars(
    mpg decimal(10, 1) NOT NULL,
    cyl int NOT NULL,
    disp decimal(10, 1) NOT NULL,
    hp int NOT NULL,
    drat decimal(10, 2) NOT NULL,
    wt decimal(10, 3) NOT NULL,
    qsec decimal(10, 2) NOT NULL,
    vs int NOT NULL,
    am int NOT NULL,
    gear int NOT NULL,
    carb int NOT NULL
);
```

Em seguida, insira os dados da compilação no conjunto de dados `mtcars`.

```SQL
INSERT INTO dbo.MTCars
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'MTCars <- mtcars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'MTCars';
```

+ Algumas pessoas gostam de usar tabelas temporárias, mas lembre-se de que alguns clientes do R desconectar sessões entre os lotes.

+ Vários conjuntos de dados, pequenos e grandes, estão incluídos com o tempo de execução de R. Para obter uma lista de conjuntos de dados instalados com o R, digite `library(help="datasets")` em um prompt de comando de R.

## <a name="create-a-model"></a>Criar um modelo

Os dados de velocidade do carro contêm duas colunas, ambas numéricas, potência (`hp`) e o peso (`wt`). A partir desses dados, você criará um modelo linear generalizado (GLM) que estima a probabilidade de que um veículo ajustá-los com uma transmissão manual.

Para criar o modelo, você define a fórmula dentro de seu código R e passa os dados como um parâmetro de entrada.

```sql
DROP PROCEDURE IF EXISTS generate_GLM;
GO
CREATE PROCEDURE generate_GLM
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'carsModel <- glm(formula = am ~ hp + wt, data = MTCarsData, family = binomial);
        trained_model <- data.frame(payload = as.raw(serialize(carsModel, connection=NULL)));'
    , @input_data_1 = N'SELECT hp, wt, am FROM MTCars'
    , @input_data_1_name = N'MTCarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model VARBINARY(max)));
END;
GO
```

+ O primeiro argumento para `glm` é o *fórmula* parâmetro, que define `am` como dependentes `hp + wt`.
+ Os dados de entrada são armazenados na variável `MTCarsData`, preenchido pela consulta SQL. Se você não atribuir um nome específico aos seus dados de entrada, o nome da variável padrão seria _InputDataSet_.

## <a name="create-a-table-for-the-model"></a>Criar uma tabela para o modelo

Em seguida, armazene o modelo para que você possa treinar novamente ou usá-lo para previsão. A saída de um pacote de R que cria um modelo é geralmente um **objeto binário**. Portanto, a tabela onde armazenar o modelo deve fornecer uma coluna de **varbinary (max)** tipo.

```sql
CREATE TABLE GLM_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
```

## <a name="save-the-model"></a>Salvar o modelo

Para salvar o modelo, execute a seguinte instrução Transact-SQL para chamar o procedimento armazenado, gerar o modelo e salvá-lo em uma tabela.

```sql
INSERT INTO GLM_models(model)
EXEC generate_GLM;
```

Observe que, se você executar esse código uma segunda vez, você receber esse erro:

```sql
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

Uma opção para evitar esse erro é atualizar o nome de cada novo modelo. Por exemplo, seria possível alterar o nome para algo mais descritivo e incluir o tipo de modelo, o dia da criação e assim por diante.

```sql
UPDATE GLM_models
SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="next-steps"></a>Próximas etapas

Agora que você tem um modelo, o guia de início rápido final, você aprenderá a gerar previsões com base nele e plotar os resultados.

> [!div class="nextstepaction"]
> [Início Rápido: Prever e plotar com base no modelo](quickstart-r-predict-from-model.md)