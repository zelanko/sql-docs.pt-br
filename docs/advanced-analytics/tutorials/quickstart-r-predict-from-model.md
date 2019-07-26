---
title: Início rápido para prever do modelo usando o R
description: Neste guia de início rápido, saiba mais sobre a pontuação usando um modelo predefinido em R e SQL Server dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: aa3a65020f2900bc4d9e0b5c5fd5a200f3334435
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469332"
---
# <a name="quickstart-predict-from-model-using-r-in-sql-server"></a>Início Rápido: Prever do modelo usando R no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste guia de início rápido, use o modelo que você criou no guia de início rápido anterior para pontuar previsões em relação aos dados atualizados. Para executar a _Pontuação_ usando novos dados, obtenha um dos modelos treinados da tabela e, em seguida, chame um novo conjunto de dados no qual basear previsões. A pontuação é um termo, às vezes, usado em ciência de dados para significar a geração de previsões, probabilidades ou outros valores com base em novos dados inseridos em um modelo treinado.

## <a name="prerequisites"></a>Pré-requisitos

Este guia de início rápido é uma extensão de [criar um modelo de previsão](quickstart-r-create-predictive-model.md).

## <a name="create-the-table-of-new-data"></a>Criar a tabela de novos dados

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

## <a name="predict-manual-transmission"></a>Prever a transmissão manual

Agora, sua `dbo.GLM_models` tabela pode conter vários modelos de R, todos criados usando parâmetros ou algoritmos diferentes ou treinados em diferentes subconjuntos de dados.

Para obter previsões com base em um modelo específico, você deve escrever um script SQL que faça o seguinte:

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

+ No exemplo, a `str` função é adicionada durante a fase de teste para verificar o esquema de dados que está sendo retornado do R. Você pode remover a instrução mais tarde.

+ Os nomes de coluna usados no script R não são necessariamente passados para a saída do procedimento armazenado. Aqui, usamos a cláusula WITH RESULTs para definir alguns novos nomes de coluna.

**Resultados**

![Conjunto de resultados para prever properbility de transmissão manual](./media/r-predict-am-resultset.png)

Também é possível usar a [previsão no Transact-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) para gerar um valor previsto ou uma pontuação com base em um modelo armazenado.

## <a name="next-steps"></a>Próximas etapas

A integração de R com o SQL Server torna mais fácil implantar soluções de R em grande escala, aproveitando os melhores recursos de R e de bancos de dados relacionais, para manipulação de dados de alto desempenho e rápida análise de R. 

Continue aprendendo sobre soluções usando o R com SQL Server por meio de cenários de ponta a ponta criados pelas equipes de desenvolvimento do Microsoft Data Science e do R Services.

> [!div class="nextstepaction"]
> [Tutoriais do SQL Server R](sql-server-r-tutorials.md)
