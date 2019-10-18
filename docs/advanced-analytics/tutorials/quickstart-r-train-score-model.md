---
title: Criar e pontuar um modelo de previsão em R
titleSuffix: SQL Server Machine Learning Services
description: Crie um modelo de previsão simples em R usando SQL Server Serviços de Machine Learning e, em seguida, preveja um resultado usando novos dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9acfe1e546c332801e9a5c1a7d97758053d9a0f4
ms.sourcegitcommit: 8cb26b7dd40280a7403d46ee59a4e57be55ab462
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72542118"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-r-with-sql-server-machine-learning-services"></a>Início rápido: criar e pontuar um modelo de previsão em R com SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste guia de início rápido, você criará e treinará um modelo de previsão usando o R, salvará o modelo em uma tabela em sua instância de SQL Server e, em seguida, usará o modelo para prever valores de novos dados usando [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md).

Você criará e executará dois procedimentos armazenados em execução no SQL. A primeira usa o conjunto de **mtcars** incluído no R e gera um GLM (modelo linear simples) que prevê a probabilidade de um veículo ter sido ajustado com uma transmissão manual. O segundo procedimento é para Pontuação-ele chama o modelo gerado no primeiro procedimento para gerar um conjunto de previsões com base em novos dados. Ao colocar o código R em um procedimento armazenado do SQL, as operações são contidas em SQL, são reutilizáveis e podem ser chamadas por outros procedimentos armazenados e aplicativos cliente.

> [!TIP]
> Se você precisar de um atualizador em modelos lineares, experimente este tutorial que descreve o processo de ajuste de um modelo usando [modelos lineares](/machine-learning-server/r/how-to-revoscaler-linear-model) RxLinMod: ajuste

Ao concluir este guia de início rápido, você aprenderá:

> [!div class="checklist"]
> - Como inserir código R em um procedimento armazenado
> - Como passar entradas para seu código por meio de entradas no procedimento armazenado
> - Como os procedimentos armazenados são usados para colocar os modelos em operação

## <a name="prerequisites"></a>Pré-requisitos

- Este início rápido requer acesso a uma instância do SQL Server com [SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) com a linguagem R instalada.

  Sua instância de SQL Server pode estar em uma máquina virtual do Azure ou no local. Apenas esteja ciente de que o recurso de script externo está desabilitado por padrão, portanto, talvez seja necessário [habilitar o script externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificar se **SQL Server Launchpad serviço** está em execução antes de iniciar.

- Você também precisa de uma ferramenta para executar consultas SQL que contenham scripts R. Você pode executar esses scripts usando qualquer ferramenta de consulta ou gerenciamento de banco de dados, desde que ele possa se conectar a uma instância de SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Este início rápido usa o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-the-model"></a>Criar o modelo

Para criar o modelo, você criará dados de origem para treinamento, criará o modelo e o treinará usando os dados e, em seguida, armazenará o modelo em um banco de dados SQL, no qual ele pode ser usado para gerar previsões com novas fontes.

### <a name="create-the-source-data"></a>Criar os dados de origem

1. Abra o SSMS, conecte-se à sua instância do SQL Server e abra uma nova janela de consulta.

1. Crie uma tabela para salvar os dados de treinamento.

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

1. Insira os dados do `mtcars` do DataSet interno.

   ```SQL
   INSERT INTO dbo.MTCars
   EXEC sp_execute_external_script @language = N'R'
       , @script = N'MTCars <- mtcars;'
       , @input_data_1 = N''
       , @output_data_1_name = N'MTCars';
   ```

   > [!TIP]
   > Muitos conjuntos de valores, pequenos e grandes, estão incluídos no tempo de execução de R. Para obter uma lista de conjuntos de itens instalados com o R, digite `library(help="datasets")` em um prompt de comando do R.

### <a name="create-and-train-the-model"></a>Criar e treinar o modelo

Os dados de velocidade do carro contêm duas colunas, tanto numeric: potência (`hp`) quanto peso (`wt`). A partir desses dados, você criará um modelo linear generalizado (GLM) que estima a probabilidade de um veículo ter sido ajustado com uma transmissão manual.

Para criar o modelo, você define a fórmula dentro do código R e passa os dados como um parâmetro de entrada.

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

- O primeiro argumento para `glm` é o parâmetro de *fórmula* , que define `am` como dependente de `hp + wt`.
- Os dados de entrada são armazenados na variável `MTCarsData`, que é populada pela consulta SQL. Se você não atribuir um nome específico aos dados de entrada, o nome da variável padrão será _InputDataSet_.

### <a name="store-the-model-in-the-sql-database"></a>Armazenar o modelo no banco de dados SQL

Em seguida, armazene o modelo em um banco de dados SQL para que você possa usá-lo para previsão ou retreiná-lo. 

1. Crie uma tabela para armazenar o modelo.

   A saída de um pacote R que cria um modelo é geralmente um objeto binário. Portanto, a tabela na qual você armazena o modelo deve fornecer uma coluna de tipo **varbinary (max)** .

   ```sql
   CREATE TABLE GLM_models (
       model_name varchar(30) not null default('default model') primary key,
       model varbinary(max) not null
   );
   ```

1. Execute a seguinte instrução Transact-SQL para chamar o procedimento armazenado, gerar o modelo e salvá-lo na tabela que você criou.

   ```sql
   INSERT INTO GLM_models(model)
   EXEC generate_GLM;
   ```

   > [!TIP]
   > Se você executar esse código uma segunda vez, receberá este erro: "violação da restrição de chave primária... Não é possível inserir a chave duplicada no objeto dbo. stopping_distance_models ". Uma opção para evitar esse erro é atualizar o nome de cada novo modelo. Por exemplo, você pode alterar o nome para algo mais descritivo e incluir o tipo de modelo, o dia em que você o criou e assim por diante.

     ```sql
     UPDATE GLM_models
     SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
     WHERE model_name = 'default model'
     ```

## <a name="score-new-data-using-the-trained-model"></a>Pontuar novos dados usando o modelo treinado

A *Pontuação* é um termo usado na ciência de dados para significar a geração de previsões, probabilidades ou outros valores com base em novos dados inseridos em um modelo treinado. Você usará o modelo criado na seção anterior para pontuar previsões em relação a novos dados.

### <a name="create-a-table-of-new-data"></a>Criar uma tabela de novos dados

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

### <a name="predict-manual-transmission"></a>Prever a transmissão manual

Para obter previsões com base em seu modelo, escreva um script SQL que faça o seguinte:

1. Obtém o modelo desejado
1. Obtém os novos dados de entrada
1. Chama uma função de previsão de R que é compatível com esse modelo

Com o tempo, a tabela pode conter vários modelos de R, todos criados usando parâmetros ou algoritmos diferentes ou treinados em diferentes subconjuntos de dados. Neste exemplo, vamos usar o modelo chamado `default model`.

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

- Use uma instrução SELECT para obter um único modelo da tabela e passá-lo como um parâmetro de entrada.

- Depois de recuperar o modelo da tabela, chame a função `unserialize` no modelo.

- Aplique a função `predict` com os argumentos apropriados ao modelo e forneça os novos dados de entrada.

> [!NOTE]
> No exemplo, a função `str` é adicionada durante a fase de teste para verificar o esquema de dados que está sendo retornado do R. Você pode remover a instrução mais tarde.
>
> Os nomes de coluna usados no script R não são necessariamente passados para a saída do procedimento armazenado. Aqui, a cláusula WITH RESULTs é usada para definir alguns novos nomes de coluna.

**Da**

![Conjunto de resultados para prever properbility de transmissão manual](./media/r-predict-am-resultset.png)

Também é possível usar a instrução [Predict (Transact-SQL)](../../t-sql/queries/predict-transact-sql.md) para gerar um valor previsto ou uma pontuação com base em um modelo armazenado.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre SQL Server Serviços de Machine Learning, consulte:

- [O que é SQL Server Serviços de Machine Learning (Python e R)?](../what-is-sql-server-machine-learning.md)
