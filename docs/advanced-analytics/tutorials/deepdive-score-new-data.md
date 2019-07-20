---
title: Pontuar novos dados usando RevoScaleR e rxPredict
description: Tutorial explicativo sobre como pontuar dados usando a linguagem R em SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: e14b01df14c6a7f08b1b25f3db6d55fb7beb130b
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345245"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>Pontuar novos dados (tutorial de SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição faz parte do [tutorial do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com SQL Server.

Nesta etapa, você usa o modelo de regressão logística que você criou na lição anterior para pontuar outro conjunto de dados que usa as mesmas variáveis independentes que as entradas.

> [!div class="checklist"]
> * Pontuar novos dados
> * Criar um histograma das pontuações

> [!NOTE]
> Você precisa de privilégios de administrador DDL para algumas dessas etapas.

## <a name="generate-and-save-scores"></a>Gerar e salvar pontuações
  
1. Atualize a fonte de dados sqlScoreDS (criada na [lição dois](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)) para usar as informações de coluna criadas na lição anterior.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Para certificar-se de que você não perca os resultados, crie um novo objeto de fonte de dados. Em seguida, use o novo objeto Data Source para popular uma nova tabela no banco de dados RevoDeepDive.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    Neste ponto, a tabela não foi criada. Essa instrução define apenas um contêiner para os dados.
     
3. Verifique o contexto de computação atual usando **rxGetComputeContext ()** e defina o contexto de computação para o servidor, se necessário.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Como precaução, verifique a existência da tabela de saída. Se já existir um com o mesmo nome, você receberá um erro ao tentar gravar a nova tabela.
  
    Para fazer isso, faça uma chamada para as funções [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) e [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable), passando o nome da tabela como entrada.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists** consulta o driver ODBC e retorna true se a tabela existir; caso contrário, false.
    + **rxSqlServerDropTable** executa a DDL e retorna true se a tabela for descartada com êxito; caso contrário, retornará false.

5. Execute [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) para criar as pontuações e salvá-las na nova tabela definida na fonte de dados sqlScoreDS.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    A função **rxPredict** é outra função que dá suporte à execução em contextos de computação remota. Você pode usar a função **rxPredict** para criar pontuações de modelos com base em [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)ou [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm).
  
    - O parâmetro *writeModelVars* é definido como **TRUE** aqui. Isso significa que as variáveis usadas para a estimativa serão incluídas na nova tabela.
  
    - O parâmetro *predVarNames* especifica a variável em que os resultados serão armazenados. Aqui, você está passando uma nova variável `ccFraudLogitScore`,.
  
    - O parâmetro *type* de **rxPredict** define como você quer que as previsões sejam calculadas. Especifique a palavra-chave **Response** para gerar pontuações com base na escala da variável de resposta. Ou use o **link** de palavra-chave para gerar pontuações com base na função de link subjacente. nesse caso, as previsões são criadas usando uma escala logística.

6. Após alguns instantes, você pode atualizar a lista de tabelas no Management Studio para ver a nova tabela e seus dados.

7. Para adicionar mais variáveis às previsões de saída, use o argumento *extraVarsToWrite*.  Por exemplo, no código a seguir, a variável *custID* é adicionada da tabela de dados de pontuação à tabela de saída de previsões.
  
    ```R
    rxPredict(modelObject = logitObj,
            data = sqlScoreDS,
            outData = sqlServerOutDS,
            predVarNames = "ccFraudLogitScore",
              type = "link",
            writeModelVars = TRUE,
            extraVarsToWrite = "custID",
            overwrite = TRUE)
    ```

## <a name="display-scores-in-a-histogram"></a>Exibir pontuações em um histograma

Depois que a nova tabela tiver sido criada, calcule e exiba um histograma das pontuações previstas 10.000. A computação será mais rápida se você especificar os valores baixos e altos, portanto, obtenha-os do banco de dados e adicione-os aos seus próprios seus dados de trabalho.

1. Crie uma nova fonte de dados, sqlMinMax, que consulta o banco de dado para obter os valores baixos e altos.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     Neste exemplo, você também pode ver como é fácil usar objetos de fonte de dados **RxSqlServerData** para definir conjuntos de dados arbitrários com base em consultas SQL, funções ou procedimentos armazenados de fonte de dados e, em seguida, usá-los no seu código R. A variável não armazena os valores reais, apenas a definição de fonte de dados. A consulta é executada para gerar os valores somente quando você usá-los em uma função, como **rxImport**.
      
2. Chame a função [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) para colocar os valores em um quadro de dados que pode ser compartilhado entre contextos de computação.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **Resultados**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. Agora que os valores máximo e mínimo estão disponíveis, use os valores para criar outra fonte de dados para as pontuações geradas.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. Use o objeto de fonte de dados sqlOutScoreDS para obter as pontuações e computar e exibir um histograma. Adicione o código para definir o contexto de computação, se necessário.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **Resultados**
  
    ![histograma complexo criado por R](media/rsql-sue-complex-histogram.png "histograma complexo criado por R")
  
## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Transformar dados usando o R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)