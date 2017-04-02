---
title: "Pontuar novos dados (Aprofundamento da ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# Pontuar novos dados (Aprofundamento da ci&#234;ncia de dados)
Agora que você tem um modelo que pode ser usado para previsões, você o alimentará com dados do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gerar algumas previsões.  
  
## Pontuar novos dados  
Você usará o modelo de regressão logística, *logitObj*, para criar pontuações para outro conjunto de dados que usa as mesmas variáveis independentes como entradas.  
  
> [!NOTE]  
> Você precisará de privilégios de administrador DDL para algumas dessas etapas.  
  
1.  Atualize a fonte de dados configurada anteriormente, *sqlScoreDS*, para adicionar as informações de coluna necessárias.  
  
    ```R  
    sqlScoreDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        table = sqlScoreTable,   
        colInfo = ccColInfo,   
        rowsPerRead = sqlRowsPerRead)    
    ```  
  
2.  Para garantir que não perca os resultados, você criará um novo objeto de fonte de dados e o usará para popular uma nova tabela do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    ```R    
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",   
        connectionString = sqlConnString,   
        rowsPerRead = sqlRowsPerRead )    
    ```  
     Neste ponto, a tabela não foi criada. Essa instrução define apenas um contêiner para os dados.
     
3.  Verifique o contexto de computação atual e defina o contexto de computação como o servidor, se necessário.  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
  
4.  Antes de executar a função de previsão que gera os resultados, você precisa verificar se há uma tabela de saída existente. Caso contrário, você obterá um erro ao tentar gravar a nova tabela  
  
    Para fazer isso, faça uma chamada para as funções *rxSqlServerTableExists* e *rxSqlServerDropTable*, passando o nome da tabela como entrada.  
  
    ```R  
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")   
    ```  
  
    -   A função *rxSqlServerTableExists* consultará o driver ODBC e retornará TRUE se a tabela existir, se não, retornará FALSE.    
    -   A função *rxSqlServerDropTable* executará a DDL e retornará TRUE se a tabela for removida com êxito, se não, retornará FALSE.   
  
5.  Agora, você está pronto para usar a função *rxPredict* para criar as pontuações e salvá-las na nova tabela definida na fonte de dados *sqlScoreDS*.  
  
    ```R  
    rxPredict(modelObject = logitObj,   
        data = sqlScoreDS,        
        outData = sqlServerOutDS,     
        predVarNames = "ccFraudLogitScore",   
          type = "link",      
        writeModelVars = TRUE,        
        overwrite = TRUE)    
    ```  
  
    A função *rxPredict* é outra função que dá suporte à execução em contextos de computação remota. Você pode usar a função *rxPredict* para criar pontuações de modelos criados usando *rxLinMod*, *rxLogit* ou *rxGlm*.  
  
    -   O parâmetro *writeModelVars* é definido como **TRUE** aqui. Isso significa que as variáveis usadas para a estimativa serão incluídas na nova tabela.  
  
    -   O parâmetro *predVarNames* especifica a variável em que os resultados serão armazenados. Aqui, você está passando uma nova variável, *ccFraudLogitScore*.  
  
    -   O parâmetro *type* de *rxPredict* define como você quer que as previsões sejam calculadas. Especifique a palavra-chave **response** para gerar pontuações com base na escala da variável de resposta ou use a palavra-chave **link** para gerar pontuações com base na função de link subjacente, caso em que as previsões estarão em uma escala de logística.  

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
  
## Exibir pontuações em um histograma  
Depois que a nova tabela foi criada, você vai calcular e exibir um histograma das 10.000 pontuações previstas. Os cálculos serão mais rápidos se você especificar valores altos e baixos, para que você os receba do banco de dados e os adicione aos seus dados de trabalho.  
  
1.  Crie uma nova fonte de dados, *sqlMinMax*, que consulta o banco de dados para obter valores altos e baixos.  
  
    ```R  
    sqlMinMax <- RxSqlServerData(  
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",   
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),   
        connectionString = sqlConnString)    
    ```  
     Neste exemplo, você também pode ver como é fácil usar objetos de fonte de dados *RxSqlServerData* para definir conjuntos de dados arbitrários com base em consultas SQL, funções ou procedimentos armazenados de fonte de dados e, em seguida, usá-los no seu código R. A variável não armazena os valores reais, apenas a definição de fonte de dados. A consulta é executada para gerar os valores somente quando você usá-los em uma função, como *rxImport*.  
      
2.  Chame a função *rxImport* para colocar os valores em um quadro de dados que pode ser compartilhado entre contextos de computação.  
  
    ```R  
    minMaxVals <- rxImport(sqlMinMax)   
    minMaxVals <- as.vector(unlist(minMaxVals))  
  
    ```  
     **Resultados**
 
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3.  Agora que os valores mínimo e máximo estão disponíveis, use-os para criar a fonte de dados de pontuação.  
  
    ```R  
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",    
        connectionString = sqlConnString,   
        rowsPerRead = sqlRowsPerRead,   
            colInfo = list(ccFraudLogitScore = list(   
                low = floor(minMaxVals[1]),    
                        high = ceiling(minMaxVals[2]) ) ) )  
  
    ```  

  
4.  Por fim, use o objeto de fonte de dados de pontuação para obter os dados de pontuação e calcular e exibir um histograma. Adicione o código para definir o contexto de computação, se necessário.  
  
    ```R  
    # rxSetComputeContext(sqlCompute)   
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)  
  
    ```  
  
    **Resultados**  
  
    ![complex histogram created by R](../../advanced-analytics/r-services/media/rsql-sue-complex-histogram.png "complex histogram created by R")  
  
## Próxima etapa  
[Lição 3: Transformar dados usando o R &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/lesson-3-transform-data-using-r-data-science-deep-dive.md)  
  
## Etapa anterior  
[Criar modelos &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/create-models-data-science-deep-dive.md)  
  
## Consulte também  
[Aprofundamento da ciência de dados: Visão geral &#40;SQL Server R Services&#41;](http://msdn.microsoft.com/library/mt637368(SQL.130).aspx)  
  
  
  
