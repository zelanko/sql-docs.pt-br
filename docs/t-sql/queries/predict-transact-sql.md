---
title: PREVER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PREDICT clause
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 529cb229b6658085d0f2122604a4ed638f66a84c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="predict-transact-sql"></a>PREVER (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Gera um valor previsto ou pontuações com base em um modelo armazenado.  

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

O `MODEL` parâmetro é usado para especificar o modelo usado para previsão ou pontuação. O modelo é especificado como uma variável ou um literal ou uma expressão escalar.

O objeto de modelo pode ser criado usando o R ou Python ou outra ferramenta.

**dados**

O parâmetro de dados é usado para especificar os dados usados para previsão ou pontuação. Dados são especificados na forma de uma fonte de tabela na consulta. Fonte de tabela pode ser uma tabela, o alias de tabela, alias CTE, exibição ou função com valor de tabela.

**parâmetros**

O parâmetro de parâmetros é usado para especificar os parâmetros opcionais definidas pelo usuário usados para pontuação ou previsão.

O nome de cada parâmetro é específico para o tipo de modelo. Por exemplo, a função rxPredict RevoScaleR aceita o parâmetro  _@computeResiduals bit_ para dar suporte ao cálculo de restos quando um modelo de regressão logística de pontuação. Você pode passar o nome do parâmetro e valor para o `PREDICT` função.

> [OBSERVAÇÃO] Essa opção não há suporte para a versão de pré-lançamento do SQL Server 2017 e está incluída para fins de compatibilidade com versões posteriores.

**COM ( \<result_set_definition >)**

A cláusula WITH é usada para especificar o esquema da saída retornada pelo `PREDICT` função.

Além das colunas retornadas pelo `PREDICT` função em si, todas as colunas que fazem parte dos dados de entrada estão disponíveis para uso na consulta.

### <a name="return-values"></a>Valores de retorno

Nenhum esquema predefinida está disponível. SQL Server não valida o conteúdo do modelo e não validar os valores da coluna retornada.  
- O `PREDICT` função passa pelas colunas como entrada  
- O `PREDICT` função também gera novas colunas, mas o número de colunas e seus tipos de dados depende do tipo de modelo que foi usado para previsão.  

As mensagens de erro relacionadas aos dados, o modelo ou o formato de coluna são retornados pela função de previsão subjacente associada ao modelo.  
- Para RevoScaleR, a função equivalente é [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)  
- Para MicrosoftML, a função equivalente é [rxPredict.mlModel](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxpredict)  

Não é possível exibir a estrutura de modelo interno usando `PREDICT`. Se você quiser entender o conteúdo do modelo em si, carregar o objeto de modelo, desserializá-la e usar código R apropriado para analisar o modelo.

## <a name="remarks"></a>Comentários

O `PREDICT` função é suportada em todas as edições do SQL Server, incluindo o Linux.

Não é necessário que o R, Python ou outra máquina aprendizado idioma ser instalado no servidor para usar o `PREDICT` função. Você pode treinar o modelo em outro ambiente e salvá-lo em uma tabela do SQL Server para uso com `PREDICT`, ou ligue para o modelo de outra instância do SQL Server que tem o modelo de salvo.

### <a name="supported-algorithms"></a>Algoritmos com suporte

O modelo que você usa deve ter sido criado usando um dos algoritmos com suporte do pacote RevoScaleR. Para obter uma lista de modelos com suporte no momento, consulte [em tempo real de pontuação](../../advanced-analytics/real-time-scoring.md).

### <a name="permissions"></a>Permissões

Nenhuma permissão é necessária para `PREDICT`; no entanto, o usuário precisa `EXECUTE` permissão no banco de dados e a permissão para consultar quaisquer dados que são usados como entradas. O usuário também deve ser capaz de ler o modelo de uma tabela, se o modelo foi armazenado em uma tabela.

## <a name="examples"></a>Exemplos

Os exemplos a seguir demonstram a sintaxe para chamar `PREDICT`.

### <a name="call-a-stored-model-and-use-it-for-prediction"></a>Chamar um modelo armazenado e usá-lo para previsão

Este exemplo chama um modelo de regressão logística existente armazenado na tabela [models_table]. Ele obtém o último modelo treinado, usando uma instrução SELECT e, em seguida, passa o modelo binário para a função de previsão. Os valores de entrada representarem recursos; a saída representa a classificação atribuída pelo modelo.

```sql
DECLARE @logit_model varbinary(max) = "SELECT TOP 1 @model from [models_table]";
DECLARE @input_qry = "SELECT ID, [Gender], [Income] from NewCustomers";

SELECT PREDICT [class]
FROM PREDICT( MODEL = @logit_model,  DATA = @input_qry
WITH (class string);
```

### <a name="using-predict-in-a-from-clause"></a>Uso de previsão em uma cláusula FROM

Este exemplo faz referência a `PREDICT` funcionar no `FROM` cláusula de um `SELECT` instrução:

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

O alias **d** especificado para a fonte de tabela no _dados_ parâmetro é usado para fazer referência a colunas que pertencem a dbo.mytable. O alias **p** especificado para o **PREVER** função é usada para referenciar as colunas retornadas pela função de previsão.

### <a name="combining-predict-with-an-insert-statement"></a>A combinação de PREVER com uma instrução INSERT

Um dos casos de uso comuns para a previsão é gerar uma pontuação para dados de entrada e, em seguida, inserir os valores previstos em uma tabela. O exemplo a seguir pressupõe que o aplicativo de chamada usa um procedimento armazenado para inserir uma linha que contém o valor previsto em uma tabela:

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

Se o procedimento usa várias linhas por meio de um parâmetro com valor de tabela, em seguida, ele pode ser escrito da seguinte maneira:

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

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>Criar um modelo de R e gerar pontuações usando parâmetros de modelo opcional

> [!NOTE]
> Não há suporte para o uso do argumento parâmetros na versão Release Candidate 1.

Este exemplo supõe que você tenha criado um modelo de regressão logística ajustado com uma matriz de covariância, usando uma chamada para RevoScaleR como este:

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

Se você armazenar o modelo no SQL Server em formato binário, você pode usar a função de previsão para gerar não apenas previsões, mas as informações adicionais com suporte pelo tipo de modelo, como erro ou intervalos de confiança.

O código a seguir mostra a chamada equivalente de R para rxPredict:

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

A chamada equivalente usando o `PREDICT` função também fornece a pontuação (previsto valor), erro e intervalos de confiança:

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```



