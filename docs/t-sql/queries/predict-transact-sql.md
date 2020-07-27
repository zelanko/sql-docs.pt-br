---
title: PREDICT (Transact-SQL)
titleSuffix: SQL machine learning
ms.custom: ''
ms.date: 06/26/2020
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PREDICT clause
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||>=azure-sqldw-latest||=sqlallproducts-allversions'
ms.openlocfilehash: 039441b0029a5c2d92e16f7bc35bc496c6cd440c
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918590"
---
# <a name="predict-transact-sql"></a>PREDICT (Transact-SQL)

[!INCLUDE [sqlserver2017-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2017-asdb-asdbmi-asa.md)]

Gera um valor previsto ou pontuações com base em um modelo armazenado. Para obter mais informações, confira [Pontuação nativa usando a função PREDICT T-SQL](../../machine-learning/predictions/native-scoring-predict-transact-sql.md).

## <a name="syntax"></a>Sintaxe

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

```syntaxsql
PREDICT  
(  
  MODEL = @model | model_literal,  
  DATA = object AS <table_alias>
  [, RUNTIME = ONNX ]
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

MODEL = @model | model_literal  
```

::: moniker-end

::: moniker range=">=azure-sqldw-latest||=sqlallproducts-allversions"

```syntaxsql
PREDICT  
(  
  MODEL = <model_object>,
  DATA = object AS <table_alias>
  [, RUNTIME = ONNX ]
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

<model_object> ::=
  {
    model_literal
    | model_variable
    | ( scalar_subquery )
  }
```

::: moniker-end

### <a name="arguments"></a>Argumentos

**MODELO**

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=sqlallproducts-allversions"
O parâmetro `MODEL` é usado para especificar o modelo usado para previsão ou pontuação. O modelo é especificado como uma variável, uma literal ou uma expressão escalar.

`PREDICT` é compatível com modelos treinados usando os pacotes [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) e [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md).
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
O parâmetro `MODEL` é usado para especificar o modelo usado para previsão ou pontuação. O modelo é especificado como uma variável, uma literal ou uma expressão escalar.

Na Instância Gerenciada de SQL do Azure, `PREDICT` é compatível com modelos no formato [ONNX (Open Neural Network Exchange)](https://onnx.ai/get-started.html) ou modelos treinados usando os pacotes [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) e [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md).
::: moniker-end

::: moniker range=">=azure-sqldw-latest||=sqlallproducts-allversions"
O parâmetro `MODEL` é usado para especificar o modelo usado para previsão ou pontuação. O modelo é especificado como uma variável, como uma expressão literal ou escalar ou como uma subconsulta escalar.

No Azure Synapse Analytics, `PREDICT` é compatível com modelos no formato [ONNX (Open Neural Network Exchange)](https://onnx.ai/get-started.html).
::: moniker-end

**DADOS**

O parâmetro DATA é usado para especificar os dados usados para previsão ou pontuação. Os dados são especificados na forma de uma origem de tabela na consulta. A origem de tabela pode ser uma tabela, um alias de tabela, um alias de CTE (Expressão de Tabela Comum), uma exibição ou uma função com valor de tabela.

**RUNTIME = ONNX**

> [!IMPORTANT]
> O argumento `RUNTIME = ONNX` está disponível somente na [Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview) e no [SQL do Azure no Edge](/azure/sql-database-edge/onnx-overview).

Indica o mecanismo de machine learning usado para a execução do modelo. O valor do parâmetro `RUNTIME` sempre será `ONNX`. O parâmetro é necessário para o SQL do Azure no Edge. Na Instância Gerenciada de SQL do Azure, o parâmetro é opcional e usado somente com modelos ONNX.

**WITH ( <result_set_definition> )**

A cláusula WITH é usada para especificar o esquema da saída retornada pela função `PREDICT`.

Além das colunas retornadas pela própria função `PREDICT`, todas as colunas que fazem parte dos dados de entrada estão disponíveis para serem usadas na consulta.

### <a name="return-values"></a>Valores retornados

Nenhum esquema predefinido está disponível. O conteúdo do modelo e os valores de coluna retornados não são validados.

- A função `PREDICT` passa pelas colunas como entrada.
- A função `PREDICT` também gera novas colunas, mas o número de colunas e seus tipos de dados dependem do tipo de modelo que foi usado para previsão.

As mensagens de erro relacionadas aos dados, ao modelo ou ao formato de coluna são retornadas pela função de previsão subjacente associada ao modelo.

::: moniker range=">=sql-server-2017||>=sql-server-linux-2017||=sqlallproducts-allversions"
## <a name="remarks"></a>Comentários

A função `PREDICT` tem suporte em todas as edições do SQL Server 2017 ou posterior, no Windows e no Linux. Os [Serviços de Machine Learning](../../machine-learning/sql-server-machine-learning-services.md) não precisam ser habilitados para usar o `PREDICT`.
::: moniker-end

### <a name="supported-algorithms"></a>Algoritmos compatíveis

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=sqlallproducts-allversions"
O modelo usado deverá ter sido criado com um dos algoritmos compatíveis com os pacotes [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) ou [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md). Para obter uma lista de modelos atualmente compatíveis, confira [Pontuação nativa usando a função PREDICT T-SQL](../../machine-learning/predictions/native-scoring-predict-transact-sql.md).
::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"
Os algoritmos que podem ser convertidos em um formato de modelo [ONNX](https://onnx.ai/) são compatíveis.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Os algoritmos que podem ser convertidos em um formato de modelo [ONNX](https://onnx.ai/) e os modelos criados usando um dos algoritmos dos pacotes [RevoScaleR](../../machine-learning/r/ref-r-revoscaler.md) ou [revoscalepy](../../machine-learning/python/ref-py-revoscalepy.md) são compatíveis. Para obter uma lista de algoritmos atualmente compatíveis com RevoScaleR e revoscalepy, confira [Pontuação nativa usando a função PREDICT T-SQL](../../machine-learning/predictions/native-scoring-predict-transact-sql.md).
::: moniker-end

### <a name="permissions"></a>Permissões

Não é necessária nenhuma permissão para `PREDICT`, no entanto, o usuário precisa da permissão `EXECUTE` no banco de dados e da permissão para consultar os dados que serão usados como entradas. O usuário também precisará ler o modelo em uma tabela se o modelo estiver armazenado em uma tabela.

## <a name="examples"></a>Exemplos

Os exemplos a seguir demonstram a sintaxe para chamar `PREDICT`.

### <a name="using-predict-in-a-from-clause"></a>Uso PREDICT em uma cláusula FROM

Este exemplo referencia a função `PREDICT` na cláusula `FROM` de uma instrução `SELECT`:

::: moniker range=">=sql-server-2017||=azuresqldb-current||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @model,
    DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

:::moniker-end

::: moniker range=">=azure-sqldw-latest||=sqlallproducts-allversions"

```sql
DECLARE @model varbinary(max) = (SELECT test_model FROM scoring_model WHERE model_id = 1);

SELECT d.*, p.Score
FROM PREDICT(MODEL = @model,
    DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

::: moniker-end

O alias **d** especificado para a origem da tabela no parâmetro `DATA` é usado para referenciar as colunas que pertencem a `dbo.mytable`. O alias **p** especificado para a função `PREDICT` é usado para referenciar as colunas retornadas pela função `PREDICT`.

- O modelo é armazenado como uma coluna `varbinary(max)` na tabela chamada **Modelos**. Informações adicionais, como **ID** e **descrição**, serão salvas na tabela para identificar o modo.
- O alias **d** especificado para a origem da tabela no parâmetro `DATA` é usado para referenciar as colunas que pertencem a `dbo.mytable`. Os nomes da coluna de dados de entrada devem corresponder aos nomes das entradas para o modelo.
- O alias **p** especificado para a função `PREDICT` é usado para referenciar a coluna prevista retornada pela função `PREDICT`. O nome da coluna deve ser igual ao nome de saída para o modelo.
- Todas as colunas de dados de entrada, bem como as colunas previstas estão disponíveis para exibição na instrução SELECT.

::: moniker range=">=azure-sqldw-latest||=sqlallproducts-allversions"

A consulta de exemplo anterior pode ser escrita novamente de maneira a criar uma exibição especificando `MODEL` como uma subconsulta escalar:

```sql
CREATE VIEW predictions
AS
SELECT d.*, p.Score
FROM PREDICT(MODEL = (SELECT test_model FROM scoring_model WHERE model_id = 1),
             DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

:::moniker-end

### <a name="combining-predict-with-an-insert-statement"></a>Combinando PREDICT com uma instrução INSERT

Um caso de uso comum para a previsão é gerar uma pontuação para dados de entrada e inserir os valores previstos em uma tabela. O seguinte exemplo presume que o aplicativo de chamada usa um procedimento armazenado para inserir uma linha que contém o valor previsto em uma tabela:

```sql
DECLARE @model varbinary(max) = (SELECT model FROM scoring_model WHERE model_name = 'ScoringModelV1');

INSERT INTO loan_applications (c1, c2, c3, c4, score)
SELECT d.c1, d.c2, d.c3, d.c4, p.score
FROM PREDICT(MODEL = @model, DATA = dbo.mytable AS d) WITH(score float) AS p;
```

- Os resultados de `PREDICT` são armazenados em uma tabela chamada PredictionResults. 
- O modelo é armazenado como uma coluna `varbinary(max)` na tabela chamada **Modelos**. Informações adicionais, como ID e descrição, poderão ser salvas na tabela para identificar o modelo.
- O alias **d** especificado para a origem da tabela no parâmetro `DATA` é usado para referenciar as colunas em `dbo.mytable`. Os nomes da coluna de dados de entrada devem corresponder ao nome das entradas para o modelo.
- O alias **p** especificado para a função `PREDICT` é usado para referenciar a coluna prevista retornada pela função `PREDICT`. O nome da coluna deve ser igual ao nome de saída para o modelo.
- Todas as colunas de entrada, bem como a coluna prevista estão disponíveis para exibição na instrução SELECT.

## <a name="next-steps"></a>Próximas etapas

- [Pontuação nativa usando a função PREDICT T-SQL](../../machine-learning/predictions/native-scoring-predict-transact-sql.md)
::: moniker range="=azure-sqldw-latest||=azuresqldb-mi-current||=sqlallproducts-allversions"
-   [Saiba mais sobre os modelos ONNX](/azure/machine-learning/concept-onnx#get-onnx-models)
::: moniker-end
