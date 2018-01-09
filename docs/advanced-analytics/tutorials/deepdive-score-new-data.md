---
title: Pontuar novos dados (SQL e R mergulho profundo) | Microsoft Docs
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9b4192252edff42275acff6902677e3dadd3122e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="score-new-data-sql-and-r-deep-dive"></a>Pontuar novos dados (SQL e R mergulho profundo)

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Nesta etapa, você deve usar o modelo de regressão logística que você criou anteriormente, para criar pontuações para outro conjunto de dados que usa as mesmas variáveis independentes, como entradas.

> [!NOTE]
> Você precisa de privilégios de administrador DDL para algumas dessas etapas.

## <a name="generate-and-save-scores"></a>Gerar e salvar os resultados
  
1. Atualizar a fonte de dados que você configurou anteriormente, `sqlScoreDS`, para adicionar as informações de coluna necessária.
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. Para certificar-se de que você não perca os resultados, crie um novo objeto de fonte de dados. Em seguida, use o novo objeto de fonte de dados para popular uma nova tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    Neste ponto, a tabela não foi criada. Essa instrução define apenas um contêiner para os dados.
     
3. Verifique o contexto de computação atual e defina o contexto de computação como o servidor, se necessário.
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Antes de executar a função de previsão que gera os resultados, você precisa verificar se há uma tabela de saída existente. Caso contrário, você obterá um erro ao tentar gravar a nova tabela.
  
    Para fazer isso, faça uma chamada para as funções **rxSqlServerTableExists** e **rxSqlServerDropTable**, passando o nome da tabela como entrada.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    -  A função **rxSqlServerTableExists** consultará o driver ODBC e retornará TRUE se a tabela existir, se não, retornará FALSE.
    -  A função **rxSqlServerDropTable** executa a DDL e retorna TRUE se a tabela com êxito é descartado, FALSO caso contrário.
    - Referência para ambas as funções podem ser encontradas aqui: [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)
  
5. Agora você está pronto para usar o [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) para criar as pontuações de função e salvá-los na nova tabela definida na fonte de dados `sqlScoreDS`.
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    A função **rxPredict** é outra função que dá suporte à execução em contextos de computação remota. Você pode usar a função **rxPredict** para criar pontuações de modelos criados usando [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod), [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)ou [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm).
  
    - O parâmetro *writeModelVars* é definido como **TRUE** aqui. Isso significa que as variáveis usadas para a estimativa serão incluídas na nova tabela.
  
    - O parâmetro *predVarNames* especifica a variável em que os resultados serão armazenados. Aqui você estiver passando uma nova variável, `ccFraudLogitScore`.
  
    - O parâmetro *type* de **rxPredict** define como você quer que as previsões sejam calculadas. Especifique a palavra-chave **resposta** para gerar pontuações com base na escala da variável de resposta. Ou, use a palavra-chave **link** para gerar pontuações com base na função de link subjacente, caso em que previsões são criadas usando uma escala de logística.

6. Após alguns instantes, você pode atualizar a lista de tabelas no Management Studio para ver a nova tabela e seus dados.

7. Para adicionar mais variáveis às previsões de saída, use o argumento *extraVarsToWrite*.  Por exemplo, no código a seguir, a variável `custID` é adicionado da tabela de classificação de dados na tabela de saída de previsões.
  
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

## <a name="display-scores-in-a-histogram"></a>Pontuações de exibição em um histograma

Depois que a nova tabela foi criada, você pode calcular e exibir um histograma das pontuações previstas 10.000. Computação é mais rápida se você especificar os valores altos e baixos, para obter os do banco de dados e adicioná-las aos seus dados de trabalho.

1. Criar uma nova fonte de dados, `sqlMinMax`, que consulta o banco de dados para obter os valores altos e baixos.
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     Neste exemplo, você também pode ver como é fácil usar objetos de fonte de dados **RxSqlServerData** para definir conjuntos de dados arbitrários com base em consultas SQL, funções ou procedimentos armazenados de fonte de dados e, em seguida, usá-los no seu código R. A variável não armazena os valores reais, apenas a definição de fonte de dados. A consulta é executada para gerar os valores somente quando você usá-los em uma função, como **rxImport**.
      
2. Chamar o [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) função para colocar os valores em um quadro de dados que pode ser compartilhado entre contextos de computação.
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals \<- as.vector(unlist(minMaxVals))
  
    ```
     **Resultados**
     
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3. Agora que os valores mínimo e máximo estiverem disponíveis, use os valores para criar outra fonte de dados para as pontuações geradas.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. Use o objeto de fonte de dados `sqlOutScoreDS` para obter as pontuações e calcular e exibir um histograma. Adicione o código para definir o contexto de computação, se necessário.
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **Resultados**
  
    ![histograma complexo criado por R](media/rsql-sue-complex-histogram.png "histograma complexo criado por R")
  
## <a name="next-step"></a>Próxima etapa

[Transformar dados usando o R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="previous-step"></a>Etapa anterior

[Criar modelos](../../advanced-analytics/tutorials/deepdive-create-models.md)


