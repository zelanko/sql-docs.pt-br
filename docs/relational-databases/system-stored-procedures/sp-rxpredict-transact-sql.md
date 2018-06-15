---
title: sp_rxPredict | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
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
author: jeannt
ms.author: jeannt
manager: craigg
ms.openlocfilehash: ede8232f36f42cc2b9758bdee8f50457ebd58dfe
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32998803"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Gera um valor previsto com base em um modelo armazenado.

Fornece a pontuação em modelos de aprendizado de máquina quase em tempo real. `sp_rxPredict` é um procedimento armazenado fornecido como um wrapper para o `rxPredict` funcionar em [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler) e [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package). Ele está escrito em C++ e é otimizado especificamente para operações de pontuação. Ele dá suporte a ambos os R ou modelos de aprendizado de máquina do Python.

**Este tópico aplica-se a**:  
- SQL Server 2017  
- SQL Server 2016 R Services com a atualização para o Microsoft R Server  

## <a name="syntax"></a>Sintaxe

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>Argumentos

**modelo**

Um modelo pré-treinado em um formato com suporte. 

**input**

Uma consulta SQL válida

### <a name="return-values"></a>Valores retornados

Uma coluna de classificação é retornada, bem como quaisquer colunas de passagem da fonte de dados de entrada.
Adicionais classificar colunas, como o intervalo de confiança, pode ser retornado se o algoritmo oferece suporte à geração de tais valores.

## <a name="remarks"></a>Remarks

Para habilitar o uso do procedimento armazenado, SQLCLR deve ser habilitado na instância.

> [!NOTE]
> Considere as implicações de segurança antes de habilitar essa opção.

O usuário precisa `EXECUTE` no banco de dados.

### <a name="supported-platforms"></a>Plataformas com suporte

Requer uma das seguintes edições:  
- Serviços de aprendizado de máquina do SQL Server de 2017 (inclui o Microsoft R Server 9.1.0)  
- Aprendizado de máquina do Microsoft Server  
- SQL Server R Services 2016, com uma atualização da instância do R Services para Microsoft R Server 9.1.0 ou posterior  

### <a name="supported-algorithms"></a>Algoritmos compatíveis

Para obter uma lista dos algoritmos com suporte, consulte [em tempo real de pontuação](../../advanced-analytics/real-time-scoring.md).

Os seguintes tipos de modelo são **não** com suporte:  
- Modelos que contém outros tipos de transformações de R sem suporte  
- Modelos usando o `rxGlm` ou `rxNaiveBayes` algoritmos em RevoScaleR  
- Modelos PMML  
- Modelos criados usando outras bibliotecas de R de CRAN ou outros repositórios  
- Modelos que contêm qualquer outro tipo de transformação de R diferente das listadas aqui  

## <a name="examples"></a>Exemplos

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

Além de ser uma consulta SQL válida, os dados de entrada em *@inputData* deve incluir colunas compatíveis com as colunas no modelo armazenado.

`sp_rxPredict` suporta somente os seguintes tipos de coluna de .NET: double, float, short, ushort, long, ulong e cadeia de caracteres. Talvez seja necessário filtrar tipos sem suporte em seus dados de entrada antes de usá-lo para a pontuação em tempo real. 

  Para obter informações sobre tipos SQL correspondentes, consulte [mapeamento de tipo CLR SQL](https://msdn.microsoft.com/library/bb386947.aspx) ou [mapeamento de dados de parâmetro CLR](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).

