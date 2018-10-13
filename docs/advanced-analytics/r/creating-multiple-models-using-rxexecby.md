---
title: Criando vários modelos usando rxExecBy (aprendizado de máquina do SQL Server) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b83abad65689e3e12310251d09199f5aa0e7c3cb
ms.sourcegitcommit: 0d6e4cafbb5d746e7d00fdacf8f3ce16f3023306
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49085122"
---
# <a name="creating-multiple-models-using-rxexecby"></a>Criar vários modelos usando rxExecBy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2017 CTP 2.0 inclui uma nova função, **rxExecBy**, que dá suporte ao processamento paralelo de vários modelos relacionados. Em vez de treinar um modelo muito grande com base nos dados de várias entidades semelhantes, o cientista de dados pode criar rapidamente vários modelos relacionados, cada uma usando dados específicos a uma única entidade.

Por exemplo, suponha que são o monitoramento de falhas do dispositivo e captura de dados para muitos tipos diferentes de equipamentos. Usando rxExecBy, você pode fornecer um único conjunto de dados grande como entrada, especifique uma coluna na qual estratificar o conjunto de dados, como o tipo de dispositivo e, em seguida, criar vários modelos de dispositivos individuais.

Esse processo tem sido chamado processamento "pleasingly paralelo", porque ele usa uma tarefa que foi um pouco oneroso para o cientista de dados ou na melhor das hipóteses entediante e a torna uma operação rápida e simple.

Os aplicativos típicos dessa abordagem incluem de previsão para medidores inteligentes de domésticos individuais, criar projeções de receita para linhas de produto separado ou criação de modelos para aprovações de empréstimos que são adaptadas às ramificações bancária individual.

## <a name="how-rxexec-works"></a>Como funciona o rxExec

A função rxExecBy de RevoScaleR destina-se de paralelo de alto volume de processamento em um grande número de pequenos conjuntos de dados.

1. Chame a função rxExecBy como parte do seu código R e passar um conjunto de dados não ordenados.
2. Especifica a partição pelo qual os dados devem ser agrupados e classificados.
3. Definir uma transformação ou função que deve ser aplicada a cada partição de dados de modelagem
4. Quando a função é executada, as consultas de dados são processadas em paralelo, se seu ambiente oferece suporte a ele. Além disso, as tarefas de modelagem ou transformação são distribuídas entre os núcleos individuais e executadas em paralelo. Contexto de computação com suporte para três operações incluem o RxSpark e o RxInSQLServer.
5. São retornados vários resultados.

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy sintaxe e exemplos

**rxExecBy** usa quatro entradas, uma das entradas que estão sendo um objeto de fonte de dados ou conjunto de dados que pode ser particionado em um site FTP **chave** coluna. A função retorna uma saída para cada partição. A forma da saída depende da função que é passada como um argumento e, em seguida, por exemplo, se você passar uma função de modelagem como rxLinMod, você poderia retornar um modelo treinado separado para cada partição do conjunto de dados.

### <a name="supported-functions"></a>Funções suportadas

Modelagem: `rxLinMod`, `rxLogit`, `rxGlm`, `rxDtree`

Pontuação: `rxPredict`,

Análise ou transformação: `rxCovCor`

## <a name="example"></a>Exemplo

O exemplo a seguir demonstra como criar vários modelos usando o conjunto de dados de companhia aérea, que é particionado na coluna [DayOfWeek]. A função definida pelo usuário, `delayFunc`, é aplicada a cada uma das partições por chamada rxExecBy. A função cria modelos separados para as segundas-feiras, às terças, e assim por diante.

```SQL
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

Se você receber o erro `varsToPartition is invalid`, verifique se o nome da coluna de chave ou colunas foi digitado corretamente. A linguagem R diferencia maiusculas de minúsculas.

Observe que neste exemplo não é otimizado para o SQL Server, e você pode em muitos casos obter melhor desempenho usando o SQL para agrupar os dados. No entanto, usando rxExecBy, você pode criar trabalhos paralelos de R.

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


