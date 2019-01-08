---
title: Guia de início rápido para prever de modelo usando R – Machine Learning do SQL Server
description: Neste início rápido, saiba mais sobre a pontuação usando um modelo predefinido em dados de R e SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 7175b99eb20710f5dd08689bd055d3a4ec93ae92
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046730"
---
# <a name="quickstart-predict-from-model-using-r-in-sql-server"></a>Guia de início rápido: Previsão de modelo usando R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Neste início rápido, use o modelo criado no início rápido anterior para pontuar previsões em relação aos dados atualizados. Para realizar _pontuação_ usando novos dados, obter um dos modelos treinados da tabela e, em seguida, chame um novo conjunto de dados no qual basear as previsões. A pontuação é um termo, às vezes, usado na ciência de dados para significar a geração de previsões, as probabilidades ou outros valores com base nos novos dados inseridos em um modelo treinado.

## <a name="prerequisites"></a>Prerequisites

Neste início rápido é uma extensão da [criar um modelo preditivo](quickstart-r-create-predictive-model.md).

## <a name="create-the-table-of-new-data"></a>Criar a tabela de dados novos

Primeiro, crie uma tabela com novos dados. 

```sql
CREATE TABLE dbo.NewMTCars(
    hp INT NOT NULL
    , wt DECIMAL(10,3) NOT NULL
    , am INT NULL
)
GO

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (110, 2.634)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (72, 3.435)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (220, 5.220)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (120, 2.800)
GO
```

## <a name="predict-manual-transmission"></a>Prever transmissão manual

Agora, seu `dbo.GLM_models` tabela pode conter vários modelos de R, todos criados com diferentes parâmetros ou algoritmos ou treinados em diferentes subconjuntos de dados.

Para obter previsões com base em um modelo específico, você deve escrever um script SQL que faz o seguinte:

1. Obtém o modelo desejado
2. Obtém os novos dados de entrada
3. Chama uma função de previsão de R que é compatível com o modelo

Neste exemplo, usaremos o modelo chamado `default model`.

```sql
DECLARE @glmmodel varbinary(max) = 
    (SELECT model FROM dbo.GLM_models WHERE model_name = 'default model');

EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(glmmodel));
            new <- data.frame(NewMTCars);
            predicted.am <- predict(current_model, new, type = "response");
            str(predicted.am);
            OutputDataSet <- cbind(new, predicted.am);
            '
    , @input_data_1 = N'SELECT hp, wt FROM dbo.NewMTCars'
    , @input_data_1_name = N'NewMTCars'
    , @params = N'@glmmodel varbinary(max)'
    , @glmmodel = @glmmodel
WITH RESULT SETS ((new_hp INT, new_wt DECIMAL(10,3), predicted_am DECIMAL(10,3)));
```

O script acima executa as seguintes etapas:

+ Use uma instrução SELECT para obter um único modelo de tabela e passe-o como um parâmetro de entrada.

+ Depois de recuperar o modelo da tabela, chame a função `unserialize` no modelo.

+ Aplicar a função `predict` com os argumentos apropriados para o modelo e fornecer os novos dados de entrada.

+ No exemplo, o `str` função será adicionada durante a fase de teste para verificar o esquema dos dados que está sendo retornados de R. Você pode remover a instrução mais tarde.

+ Os nomes de coluna usados no script R não são necessariamente passados para a saída do procedimento armazenado. Aqui, usamos a cláusula WITH RESULTS para definir alguns novos nomes de coluna.

**Resultados**

![Conjunto de resultados para prever properbility de transmissão manual](./media/r-predict-am-resultset.png)

Também é possível usar o [PREDICT no Transact-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) para gerar um valor previsto ou pontuação com base em um modelo armazenado.

## <a name="next-steps"></a>Próximas etapas

A integração de R com o SQL Server torna mais fácil implantar soluções de R em grande escala, aproveitando os melhores recursos de R e de bancos de dados relacionais, para manipulação de dados de alto desempenho e rápida análise de R. 

Continue aprendendo sobre soluções que usam R com o SQL Server por meio de cenários de ponta a ponta criados pelas equipes de desenvolvimento Microsoft Data Science e R Services.

> [!div class="nextstepaction"]
> [Tutoriais do SQL Server R](sql-server-r-tutorials.md)
