---
title: "Criando vários modelos usando rxExecBy | Microsoft Docs"
ms.custom: 
ms.date: 04/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1afae193d01f8a4a8b3a06d0022d436d14b0dd0b
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="creating-multiple-models-using-rxexecby"></a>Criando vários modelos usando rxExecBy

SQL Server 2017 CTP 2.0 inclui uma nova função, **rxExecBy**, que oferece suporte ao processamento paralelo de vários modelos relacionados. Em vez de treinar um modelo muito grande com base nos dados de várias entidades semelhantes, o cientista de dados pode criar rapidamente vários modelos relacionados, cada uma usando dados específicos de uma única entidade.

Por exemplo, suponha que o monitoramento de falhas do dispositivo e captura de dados para vários tipos diferentes de equipamento. Usando rxExecBy, fornecer um único conjunto de dados grande como entrada, especificar uma coluna na qual estratificar o conjunto de dados, como o tipo de dispositivo e, em seguida, criar vários modelos de modelos para dispositivos individuais.

Esse processo tem sido denominado processamento "pleasingly paralelo", porque usa uma tarefa que foi um pouco oneroso para o cientista de dados ou na melhor das hipóteses entediante e torna uma operação simples.

Aplicativos típicos dessa abordagem incluem previsão individuais metros inteligentes domésticos, criar projeções de receita para linhas de produto separado ou criar modelos para aprovações de empréstimo, são adaptados às ramificações banco individuais.

## <a name="how-rxexec-works"></a>Como funciona o rxExec

A função rxExecBy em RevoScaleR se destina para paralelo de alto volume de processamento em um grande número de pequenos conjuntos de dados.

1. Você chama a função rxExecBy como parte do seu código R e passa um conjunto de dados de dados não ordenados.
2. Especifica a partição pelo qual os dados devem ser agrupados e classificados.
3. Definir uma transformação ou função que deve ser aplicada a cada partição de dados de modelagem
4. Quando a função é executada, as consultas de dados são processadas em paralelo, se o seu ambiente aceitar. Além disso, as tarefas de modelagem ou transformação são distribuídas entre núcleos individuais e executadas em paralelo. Contexto de computação com suporte para três operações incluem RxSpark e RxInSQLServer.
5. São retornados vários resultados.

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy sintaxe e exemplos

**rxExecBy** usa quatro entradas, uma das entradas que estão sendo um objeto de fonte de dados ou conjunto de dados que pode ser particionado em um site FTP **chave** coluna. A função retorna uma saída para cada partição. O formato da saída depende da função que é passada como um argumento e, em seguida, por exemplo, se você passar uma função de modelagem como rxLinMod, você pode retornar um modelo treinado separado para cada partição do conjunto de dados.

### <a name="supported-functions"></a>Funções suportadas

Modelagem: `rxLinMod`, `rxLogit`, `rxGlm`,`rxDtree`

Pontuação: `rxPredict`,

Transformação ou análise:`rxCovCor`

## <a name="example"></a>Exemplo

O exemplo a seguir demonstra como criar vários modelos usando o conjunto de dados aérea, que é particionado na coluna [DayOfWeek]. A função definida pelo usuário, `delayFunc`, é aplicada a cada uma das partições por chamada rxExecBy. A função cria modelos separados para segundas-feiras, terças-feiras, e assim por diante.

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

Se você obtiver o erro `varsToPartition is invalid`, verifique se o nome da coluna de chave ou colunas foi digitado corretamente. A linguagem R diferencia maiusculas de minúsculas.

Observe que este exemplo não é otimizado para o SQL Server, e você pode, em muitos casos obter melhor desempenho usando o SQL para agrupar os dados. No entanto, usando rxExecBy, você pode criar trabalhos paralelos de R.

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


