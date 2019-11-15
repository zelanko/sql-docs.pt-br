---
title: Criar vários modelos com rxExecBy
description: Use a função rxExecBy da biblioteca RevoScaleR para criar vários minimodelos em dados de computador armazenados no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: dbba63ae69997c9c5dbdccf49ec590b3f4eba652
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727488"
---
# <a name="creating-multiple-models-using-rxexecby"></a>Criar vários modelos usando rxExecBy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **rxExecBy** no RevoScaleR dá suporte ao processamento paralelo de vários modelos relacionados. Em vez de treinar um modelo grande com base em dados de várias entidades semelhantes, um cientista de dados pode criar rapidamente muitos modelos relacionados, cada um usando dados específicos de uma única entidade. 

Por exemplo, suponha que você esteja monitorando falhas de dispositivo e capturando dados de vários tipos diferentes de equipamento. Ao usar rxExecBy, você pode fornecer um único conjunto de dados grande como entrada, especificar uma coluna na qual estratificar o conjunto de dados, como o tipo de dispositivo e, em seguida, criar vários modelos para dispositivos individuais.

Esse caso de uso é chamado de ["agradavelmente paralelo"](https://en.wikipedia.org/wiki/Embarrassingly_parallel) porque divide um problema grande e complicado em partes componentes para processamento simultâneo.

Os aplicativos típicos dessa abordagem incluem a previsão para medidores inteligentes individuais domésticos, a criação de projeções de receita para linhas de produtos separadas ou a criação de modelos para aprovações de empréstimos feitas sob medida para agências bancárias individuais.

## <a name="how-rxexec-works"></a>Como rxExec funciona

A função rxExecBy no RevoScaleR é projetada para processamento paralelo de alto volume em um grande número de conjuntos de dados pequenos.

1. Você chama a função rxExecBy como parte do código do R e passa um conjunto de dados contendo dados não ordenados.
2. Especifique a partição pela qual os dados devem ser agrupados e classificados.
3. Definir uma função de transformação ou de modelagem que deve ser aplicada a cada partição de dados
4. Quando a função for executada, as consultas de dados serão processadas em paralelo, se o seu ambiente tiver suporte para isso. Além disso, as tarefas de modelagem ou transformação são distribuídas entre núcleos individuais e executadas em paralelo. O contexto de computação com suporte para as operações incluem RxSpark e RxInSQLServer.
5. São retornados vários resultados.

## <a name="rxexecby-syntax-and-examples"></a>Sintaxe e exemplos da rxExecBy

A **rxExecBy** usa quatro entradas, sendo uma delas um conjunto de dados ou um objeto de fonte de dados que pode ser particionado em uma coluna de **chave** especificada. A função retorna uma saída para cada partição. A forma da saída depende da função passada como um argumento. Por exemplo, se você passar uma função de modelagem como rxLinMod, poderá retornar um modelo treinado separado para cada partição do conjunto de dados.

### <a name="supported-functions"></a>Funções suportadas

Modelagem: `rxLinMod`, `rxLogit`, `rxGlm`, `rxDtree`

Pontuação: `rxPredict`,

Transformação ou análise: `rxCovCor`

## <a name="example"></a>Exemplo

O exemplo a seguir demonstra como criar vários modelos usando o conjunto de dados Companhia Aérea, que é particionado na coluna [DayOfWeek]. A função definida pelo usuário, `delayFunc`, é aplicada a cada uma das partições chamando rxExecBy. A função cria modelos separados para segundas-feiras, terças-feiras e assim por diante.

```sql
EXEC sp_execute_external_script
@language = N'R'
, @script = N'
delayFunc <- function(key, data, params) { 
    df <- rxImport(inData = airlineData) 
    rxLinMod(ArrDelay ~ CRSDepTime, data = df) 
} 
OutputDataSet <- rxExecBy(airlineData, c("DayOfWeek"), delayFunc)
'
, @input_data_1 = N'select ArrDelay, DayOfWeek, CRSDepTime from AirlineDemoSmall]'
, @input_data_1_name = N'airlineData'

```

Se você receber o erro, `varsToPartition is invalid`, verifique se o nome das colunas de chave foi digitado corretamente. A linguagem R diferencia maiúsculas de minúsculas.

Esse exemplo específico não é otimizado para SQL Server e você pode, em muitos casos, obter um melhor desempenho usando o SQL para agrupar os dados. No entanto, usando rxExecBy, você pode criar trabalhos paralelos usando o R.

O exemplo a seguir ilustra o processo em R, usando o SQL Server como o contexto de computação:

```R
sqlServerConnString <- "SERVER=hostname;DATABASE=TestDB;UID=DBUser;PWD=Password;"
inTable <- paste("airlinedemosmall")
sqlServerDataDS <- RxSqlServerData(table = inTable, connectionString = sqlServerConnString)

# user function
".Count" <- function(keys, data, params)
{
  myDF <- rxImport(inData = data)
  return (nrow(myDF))
}

# Set SQL Server compute context with level of parallelism = 2
sqlServerCC <- RxInSqlServer(connectionString = sqlServerConnString, numTasks = 4)
rxSetComputeContext(sqlServerCC)

# Execute rxExecBy in SQL Server compute context
sqlServerCCResults <- rxExecBy(inData = sqlServerDataDS, keys = c("DayOfWeek"), func = .Count)
```


