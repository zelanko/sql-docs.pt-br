---
title: 'Início Rápido: Treinar um modelo em R'
description: Neste guia de início rápido, você criará e treinará um modelo de previsão usando o T. Você salvará o modelo em uma tabela em sua instância do SQL Server e, em seguida, usará o modelo para prever valores com base em novos dados usando os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b6be97041912027cf284ff34c2c826a37edabe93
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76831726"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-r-with-sql-server-machine-learning-services"></a>Início Rápido: Criar e pontuar um modelo de previsão no R com os Serviços de Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste guia de início rápido, você criará e treinará um modelo de previsão usando o T. Você salvará o modelo em uma tabela em sua instância do SQL Server e, em seguida, usará o modelo para prever valores com base em novos dados usando os [Serviços de Machine Learning do SQL Server](../what-is-sql-server-machine-learning.md).

Você criará e executará dois procedimentos armazenados em execução no SQL. O primeiro usa o conjunto de dados **mtcars** incluído com o R e gera um GLM (modelo linear generalizado) simples que prevê a probabilidade de um veículo ter sido equipado com uma transmissão manual. O segundo procedimento é para pontuação – ele chama o modelo gerado no primeiro procedimento para gerar um conjunto de previsões com base em novos dados. Ao colocar o código R em um procedimento armazenado do SQL, as operações são contidas em SQL, são reutilizáveis e podem ser chamadas por outros procedimentos armazenados e aplicativos cliente.

> [!TIP]
> Se você precisar de uma atualização sobre modelos lineares, experimente este tutorial, que descreve o processo de ajuste de um modelo usando o rxLinMod:  [Ajustando modelos lineares](/machine-learning-server/r/how-to-revoscaler-linear-model)

Ao concluir este início rápido, você aprenderá:

> [!div class="checklist"]
> - Como inserir código R em um procedimento armazenado
> - Como passar entradas para seu código por meio de entradas no procedimento armazenado
> - Como os procedimentos armazenados são usados para operacionalizar os modelos

## <a name="prerequisites"></a>Pré-requisitos

- Este início rápido requer acesso a uma instância do SQL Server que tenha os [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md) com a linguagem R instalada.

  A instância do SQL Server pode ser local ou em uma máquina virtual do Azure. Esteja ciente de que o recurso de script externo está desabilitado por padrão, portanto, talvez seja necessário [habilitar o script externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificar se o **serviço SQL Server Launchpad** está em execução antes de você começar.

- Você também precisa de uma ferramenta para executar consultas SQL que contenham scripts R. Você pode executar esses scripts usando qualquer ferramenta de consulta ou de gerenciamento de banco de dados, desde que ele possa se conectar a uma instância do SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Esse início rápido usa o [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="create-the-model"></a>Criar o modelo

Para criar o modelo, você criará dados de origem para treinamento, criará o modelo e o treinará usando esses dados e, em seguida, armazenará o modelo em um Banco de Dados SQL, no qual ele poderá ser usado para gerar previsões com novos dados.

### <a name="create-the-source-data"></a>Criar os dados de origem

1. Abra o SSMS, conecte-se à instância do SQL Server e abra uma nova janela de consulta.

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

1. Insira os dados do conjunto de dados interno `mtcars`.

   ```SQL
   INSERT INTO dbo.MTCars
   EXEC sp_execute_external_script @language = N'R'
       , @script = N'MTCars <- mtcars;'
       , @input_data_1 = N''
       , @output_data_1_name = N'MTCars';
   ```

   > [!TIP]
   > Vários conjuntos de dados, pequenos e grandes, estão incluídos com o runtime de R. Para obter uma lista de conjuntos de dados instalados com o R, digite `library(help="datasets")` em um prompt de comando de R.

### <a name="create-and-train-the-model"></a>Criar e treinar o modelo

Os dados de velocidade do carro contêm duas colunas, ambas numéricas: potência (`hp`) e peso (`wt`). Com base nesses dados, você criará um GLM (modelo linear generalizado) que estimará a probabilidade de um veículo ter sido equipado com uma transmissão manual.

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

- O primeiro argumento para o `glm` é o parâmetro *formula*, que define `am` como dependente de `hp + wt`.
- Os dados de entrada são armazenados na variável `MTCarsData`, que é preenchida pela consulta SQL. Se você não atribuir um nome específico para seus dados de entrada, o nome da variável padrão será _InputDataSet_.

### <a name="store-the-model-in-the-sql-database"></a>Armazenar o modelo no Banco de Dados SQL

Em seguida, armazene o modelo em um Banco de Dados SQL para que você possa usá-lo para previsão ou retreiná-lo. 

1. Criar uma tabela para armazenar o modelo.

   A saída de um pacote de R que cria um modelo é geralmente um objeto binário. Portanto, a tabela em que você armazena o modelo deve fornecer uma coluna do tipo **varbinary(max)** .

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
   > Se você executar esse código uma segunda vez, obterá este erro: "Violação da restrição PRIMARY KEY... Não é possível inserir a chave duplicada no objeto dbo.stopping_distance_models". Uma opção para evitar esse erro é atualizar o nome de cada modelo novo. Por exemplo, você pode alterar o nome para algo mais descritivo e incluir o tipo de modelo, o dia em que ele foi criado e assim por diante.

     ```sql
     UPDATE GLM_models
     SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
     WHERE model_name = 'default model'
     ```

## <a name="score-new-data-using-the-trained-model"></a>Pontuar novos dados usando o modelo treinado

*Pontuação* é um termo usado na ciência de dados para significar a geração de previsões, probabilidades ou outros valores com base em novos dados inseridos em um modelo treinado. Você usará o modelo criado na seção anterior para pontuar previsões comparando-as a novos dados.

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

### <a name="predict-manual-transmission"></a>Prever se a transmissão existente é manual

Para obter previsões com base em um modelo específico, escreva um script de SQL que faz o seguinte:

1. Obtém o modelo desejado
1. Obtém os novos dados de entrada
1. Chama uma função de previsão de R que é compatível com o modelo

Ao longo do tempo, a tabela pode conter vários modelos de R, todos criados com diferentes parâmetros ou algoritmos ou treinados em diferentes subconjuntos de dados. Neste exemplo, vamos usar o modelo chamado `default model`.

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

O script acima realiza as seguintes etapas:

- Use uma instrução SELECT para obter um único modelo da tabela e passá-lo como parâmetro de entrada.

- Depois de recuperar o modelo da tabela, chame a função `unserialize` no modelo.

- Aplique a função `predict` com os devidos argumentos para o modelo e forneça os novos dados de entrada.

> [!NOTE]
> No exemplo, a função `str` é adicionada durante a fase de teste para verificar o esquema dos dados sendo retornados do R. É possível remover essa instrução mais tarde.
>
> Os nomes de coluna usados no script R não são necessariamente passados para a saída do procedimento armazenado. Aqui, a cláusula WITH RESULTS é usada para definir alguns novos nomes de coluna.

**Resultados**

![Conjunto de resultados para prever a probabilidade de a transmissão ser manual](./media/r-predict-am-resultset.png)

Também é possível usar a instrução [PREDICT (Transact-SQL)](../../t-sql/queries/predict-transact-sql.md) para gerar um valor previsto ou uma pontuação com base em um modelo armazenado.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre os Serviços de Machine Learning do SQL Server, confira:

- [O que são os Serviços de Machine Learning do SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
