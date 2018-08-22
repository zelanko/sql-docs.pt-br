---
title: sp_rxPredict | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8f46403afef0e2f6cf967561a8fd24ec6409fe93
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "40434856"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Gera um valor previsto para uma determinada entrada com base em um modelo armazenado em um formato binário em um banco de dados do SQL Server de aprendizado de máquina.

Fornece a pontuação em R e Python modelos do machine learning em tempo quase real. `sp_rxPredict` é um procedimento armazenado fornecido como um wrapper para o `rxPredict` função R no [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) e [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)e o [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) função Python [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package). Ele é escrito em C + + e é otimizado especificamente para operações de pontuação.

**Este artigo se aplica a**:  
- SQL Server 2017  
- SQL Server 2016 R Services com [atualizados os componentes do R](https://docs.microsoft.com/sql/advanced-analytics/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server)

## <a name="syntax"></a>Sintaxe

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>Argumentos

**modelo**

Um modelo previamente treinado em um formato com suporte. 

**input**

Uma consulta SQL válida

### <a name="return-values"></a>Valores retornados

Uma coluna de classificação é retornada, bem como quaisquer colunas de passagem da fonte de dados de entrada.
Adicional classificar colunas, como o intervalo de confiança, pode ser retornado se o algoritmo oferece suporte à geração de tais valores.

## <a name="remarks"></a>Remarks

Para habilitar o uso do procedimento armazenado, deve ser habilitado para SQLCLR na instância.

> [!NOTE]
> Considere as implicações de segurança antes de você habilitar essa opção.

O usuário precisa `EXECUTE` permissão no banco de dados.

### <a name="supported-platforms"></a>Plataformas compatíveis
 
- Serviços de aprendizado de máquina do SQL Server 2017 (inclui o R Server 9.2)  
- SQL Server 2017 Machine Learning Server (autônomo) 
- SQL Server R Services 2016, com a atualização da instância do R Services para Microsoft R Server 9.1.0 ou posterior  

### <a name="supported-algorithms"></a>Algoritmos compatíveis

Para obter uma lista dos algoritmos com suporte, consulte [pontuação em tempo real](../../advanced-analytics/real-time-scoring.md).

Os seguintes tipos de modelo estão **não** com suporte:  
- Modelos que contenham outros tipos de transformações de R sem suporte  
- Os modelos usando o `rxGlm` ou `rxNaiveBayes` algoritmos de RevoScaleR  
- Modelos PMML  
- Modelos criados usando outras bibliotecas de R do CRAN ou outros repositórios  
- Modelos que contenham qualquer outro tipo de transformação de R diferente dos listados aqui  

## <a name="examples"></a>Exemplos

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

Além de ser uma consulta SQL válida, os dados de entrada em *@inputData* deve incluir colunas compatíveis com as colunas no modelo armazenado.

`sp_rxPredict` suporta apenas os seguintes tipos de coluna de .NET: double, float, short, ushort, long, ulong e cadeia de caracteres. Talvez você precise filtrar os tipos sem suporte em seus dados de entrada antes de usá-lo para pontuação em tempo real. 

  Para obter informações sobre tipos SQL correspondentes, consulte [mapeamento de tipo de SQL-CLR](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) ou [Mapeando dados de parâmetro CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

