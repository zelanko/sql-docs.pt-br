---
title: PREDICT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2019
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
monikerRange: '>=sql-server-2017||=azuresqldb-current||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c97363e7f13c3b42cf447ecf69929171544f3a6b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72907255"
---
# <a name="predict-transact-sql"></a>PREDICT (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

Gera um valor previsto ou pontuações com base em um modelo armazenado. Para obter mais informações, confira [Pontuação nativa usando a função PREDICT T-SQL](../../advanced-analytics/sql-native-scoring.md).

## <a name="syntax"></a>Sintaxe

```
PREDICT  
(  
  MODEL = @model | model_literal,  
  DATA = object AS <table_alias>  
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

### <a name="arguments"></a>Argumentos

**modelo**

O parâmetro `MODEL` é usado para especificar o modelo usado para previsão ou pontuação. O modelo é especificado como uma variável, uma literal ou uma expressão escalar.

O objeto de modelo pode ser criado usando R, Python ou outra ferramenta.

**data**

O parâmetro DATA é usado para especificar os dados usados para previsão ou pontuação. Os dados são especificados na forma de uma origem de tabela na consulta. A origem de tabela pode ser uma tabela, um alias de tabela, um alias de CTE (Expressão de Tabela Comum), uma exibição ou uma função com valor de tabela.

**parameters**

O parâmetro PARAMETERS é usado para especificar os parâmetros opcionais definidos pelo usuário usados para pontuação ou previsão.

O nome de cada parâmetro é específico para o tipo de modelo. Por exemplo, a função [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) em RevoScaleR é compatível com o parâmetro `@computeResiduals`, que indica se os residuais devem ser calculados ao pontuar um modelo de regressão logística. Se você estiver chamando um modelo compatível, será possível transmitir esse nome de parâmetro e um valor TRUE ou FALSE para a função `PREDICT`.

**WITH ( <result_set_definition> )**

A cláusula WITH é usada para especificar o esquema da saída retornada pela função `PREDICT`.

Além das colunas retornadas pela própria função `PREDICT`, todas as colunas que fazem parte dos dados de entrada estão disponíveis para serem usadas na consulta.

### <a name="return-values"></a>Valores retornados

Não está disponível nenhum esquema predefinido. O SQL Server não valida o conteúdo do modelo e não valida os valores de coluna retornados.

- A função `PREDICT` passa pelas colunas como entrada.
- A função `PREDICT` também gera novas colunas, mas o número de colunas e seus tipos de dados dependem do tipo de modelo que foi usado para previsão.

As mensagens de erro relacionadas aos dados, ao modelo ou ao formato de coluna são retornadas pela função de previsão subjacente associada ao modelo.

- Para RevoScaleR, a função equivalente é [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)  
- Para MicrosoftML, a função equivalente é [rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict)  

Não é possível exibir a estrutura interna do modelo usando `PREDICT`. Se você quiser entender o conteúdo do modelo em si, carregue o objeto de modelo, desserialize-o e use o código R apropriado para analisar o modelo.

## <a name="remarks"></a>Comentários

A função `PREDICT` tem suporte em todas as edições do SQL Server 2017 ou posterior, no Windows e no Linux. O `PREDICT` também é compatível com o Banco de Dados Azure SQL na nuvem. Todos esses suportes estão ativos independentemente de outros recursos de aprendizado de máquina estarem habilitados.

Não é necessário que R, Python ou outra linguagem de aprendizado de máquina esteja instalada no servidor para usar a função `PREDICT`. Você pode treinar o modelo em outro ambiente e salvá-lo em uma tabela do SQL Server para ser usado com `PREDICT`, ou chamar o modelo de outra instância do SQL Server que tenha o modelo salvo.

### <a name="supported-algorithms"></a>Algoritmos compatíveis

O modelo usado precisa ter sido criado usando um dos algoritmos compatíveis do pacote RevoScaleR. Para obter uma lista de modelos compatíveis no momento, confira [Pontuação em tempo real](../../advanced-analytics/real-time-scoring.md).

### <a name="permissions"></a>Permissões

Não é necessária nenhuma permissão para `PREDICT`, no entanto, o usuário precisa da permissão `EXECUTE` no banco de dados e da permissão para consultar os dados que serão usados como entradas. O usuário também precisará ler o modelo em uma tabela se o modelo estiver armazenado em uma tabela.

## <a name="examples"></a>Exemplos

Os exemplos a seguir demonstram a sintaxe para chamar `PREDICT`.

### <a name="using-predict-in-a-from-clause"></a>Uso PREDICT em uma cláusula FROM

Este exemplo referencia a função `PREDICT` na cláusula `FROM` de uma instrução `SELECT`:

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

O alias **d** especificado para a origem de tabela no parâmetro `DATA` é usado para referenciar as colunas que pertencem a dbo.mytable. O alias **p** especificado para a função **PREVER** é usado para referenciar as colunas retornadas pela função PREDICT.

### <a name="combining-predict-with-an-insert-statement"></a>Combinando PREDICT com uma instrução INSERT

Um dos casos de uso comuns para a previsão é gerar uma pontuação para dados de entrada e, em seguida, inserir os valores previstos em uma tabela. O exemplo a seguir considera que o aplicativo de chamada usa um procedimento armazenado para inserir uma linha que contém o valor previsto em uma tabela:

```sql
CREATE PROCEDURE InsertLoanApplication
(@p1 varchar(100), @p2 varchar(200), @p3 money, @p4 int)
AS
BEGIN
  DECLARE @model varbinary(max) = (select model
  FROM scoring_model
  WHERE model_name = 'ScoringModelV1');
  WITH d as ( SELECT * FROM (values(@p1, @p2, @p3, @p4)) as t(c1, c2, c3, c4) )

  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = d) WITH(score float) as p;
END;
```

Se o procedimento usar várias linhas por meio de um parâmetro com valor de tabela, ele poderá ser escrito da seguinte maneira:

```sql
CREATE PROCEDURE InsertLoanApplications (@new_applications dbo.loan_application_type)
AS
BEGIN
  DECLARE @model varbinary(max) = (SELECT model_bin FROM scoring_models WHERE model_name = 'ScoringModelV1');
  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = @new_applications as d)
  WITH (score float) as p;
END;
```

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>Criando um modelo R e gerando pontuações usando parâmetros de modelo opcionais

Este exemplo considera que você tenha criado um modelo de regressão logística ajustado com uma matriz de covariância, usando uma chamada para RevoScaleR como esta:

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

Se você armazenar o modelo no SQL Server em formato binário, será possível usar a função PREDICT para gerar não apenas previsões, mas também as informações adicionais compatíveis com o tipo de modelo, como erro ou intervalos de confiança.

O código a seguir mostra a chamada equivalente de R para [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict):

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

A chamada equivalente usando a função `PREDICT` também fornece a pontuação (valor previsto), o erro e os intervalos de confiança:

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```

## <a name="next-steps"></a>Próximas etapas

- [Pontuação nativa usando a função PREDICT T-SQL](../../advanced-analytics/sql-native-scoring.md)
