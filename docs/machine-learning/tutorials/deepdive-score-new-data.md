---
title: Pontuação de dados usando RevoScaleR
description: Use o modelo de regressão logística que você criou no tutorial anterior para pontuar outro conjunto de dados que usa as mesmas variáveis independentes como entradas.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15'
ms.openlocfilehash: 314520a54bb9052fb091932b63b9cf4c817a0f16
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470497"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>Pontuar dados novos (tutorial do SQL Server e RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este é o tutorial 8 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Nesse tutorial, você usará o modelo de regressão logística que criou no tutorial anterior para pontuar outro conjunto de dados que usa as mesmas variáveis independentes como entradas.

> [!div class="checklist"]
> * Pontuar novos dados
> * Criar um histograma das pontuações

> [!NOTE]
> Você precisa de privilégios de administrador DDL para algumas dessas etapas.

## <a name="generate-and-save-scores"></a>Gerar e salvar pontuações
  
1. Atualize a fonte de dados sqlScoreDS (criada no [tutorial dois](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)) para usar as informações de coluna criadas no tutorial anterior.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Para não perder os resultados, crie um novo objeto de fonte de dados. Em seguida, use o novo objeto de fonte de dados para popular uma nova tabela no banco de dados RevoDeepDive.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    Neste ponto, a tabela não foi criada. Essa instrução define apenas um contêiner para os dados.
     
3. Verifique o contexto de computação atual usando **rxGetComputeContext()** e defina o contexto de computação como o servidor, se necessário.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Como precaução, verifique a existência da tabela de saída. Se já existir uma com o mesmo nome, você obterá um erro ao tentar gravar na nova tabela.
  
    Para fazer isso, faça uma chamada para as funções [rxSqlServerTableExists](/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) e [rxSqlServerDropTable](/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable), passando o nome da tabela como entrada.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists** consulta o driver ODBC e retorna TRUE se a tabela existir ou FALSE, caso contrário.
    + **rxSqlServerDropTable** executa a DDL e retornará TRUE se a tabela for removida com êxito; se não, retornará FALSE.

5. Execute [rxPredict](/machine-learning-server/r-reference/revoscaler/rxpredict) para criar as pontuações e salvá-las na nova tabela definida na fonte de dados sqlScoreDS.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    A função **rxPredict** é outra função que dá suporte à execução em contextos de computação remota. Você pode usar a função **rxPredict** para criar pontuações de modelos baseados em [rxLinMod](/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](/machine-learning-server/r-reference/revoscaler/rxlogit) ou [rxGlm](/machine-learning-server/r-reference/revoscaler/rxglm).
  
    - O parâmetro *writeModelVars* é definido como **TRUE** aqui. Isso significa que as variáveis usadas para a estimativa serão incluídas na nova tabela.
  
    - O parâmetro *predVarNames* especifica a variável em que os resultados serão armazenados. Aqui você está passando uma nova variável, a `ccFraudLogitScore`.
  
    - O parâmetro *type* de **rxPredict** define como você quer que as previsões sejam calculadas. Especifique a palavra-chave **response** para gerar pontuações com base na escala da variável de resposta. Ou use a palavra-chave **link** para gerar pontuações com base na função de link subjacente; nesse caso, as previsões serão criadas usando uma escala logística.

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

Depois que a nova tabela foi criada, calcule e exiba um histograma das 10 mil pontuações previstas. Os cálculos serão mais rápidos se você especificar valores altos e baixos, portanto obtenha-os no banco de dados e os adicione aos dados de trabalho.

1. Crie uma nova fonte de dados, sqlMinMax, que consulta o banco de dados para obter valores altos e baixos.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     Neste exemplo, você também pode ver como é fácil usar objetos de fonte de dados **RxSqlServerData** para definir conjuntos de dados arbitrários com base em consultas SQL, funções ou procedimentos armazenados de fonte de dados e, em seguida, usá-los no seu código R. A variável não armazena os valores reais, apenas a definição de fonte de dados. A consulta é executada para gerar os valores somente quando você usá-los em uma função, como **rxImport**.
      
2. Chame a função [rxImport](/machine-learning-server/r-reference/revoscaler/rximport) para colocar os valores em um quadro de dados que pode ser compartilhado entre contextos de computação.
  
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
> [Transformar dados usando o R](../../machine-learning/tutorials/deepdive-transform-data-using-r.md)