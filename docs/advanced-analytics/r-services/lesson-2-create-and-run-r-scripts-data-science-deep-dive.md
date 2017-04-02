---
title: "Li&#231;&#227;o 2: Criar e executar scripts do R (Aprofundamento da ci&#234;ncia de dados) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "10/26/2016"
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
ms.assetid: 51e8e66f-a0a5-4e96-aa71-f5c870e6d0d4
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 18
---
# Li&#231;&#227;o 2: Criar e executar scripts do R (Aprofundamento da ci&#234;ncia de dados)
Agora configurou as fontes de dados e estabeleceu um ou vários contextos de computação, você está pronto para executar alguns scripts do R de alta potência usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nesta lição, você aprenderá a usar o contexto de computação do servidor para executar algumas tarefas comuns de aprendizado de máquina:  
  
-   Visualizar dados e gerar algumas estatísticas de resumo    
-   Criar um modelo de regressão linear    
-   Criar um modelo de regressão logística    
-   Pontuar novos dados e criar um histograma das pontuações  
  
## Alterar o contexto de computação para o servidor  
Antes de executar um código do R, você precisa especificar o contexto de computação *atual* ou *ativo*.  
  
1.  Para ativar um contexto de computação que você já definiu usando o R, use a função *rxSetComputeContext*, como mostrado aqui:  
  
    ```R  
    rxSetComputeContext(sqlCompute)   
    ```  
  
    Assim que você executar essa instrução, todos os cálculos posteriores ocorrerão no computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificado no parâmetro *sqlCompute*.  
  
  
2.  Se você decidir que prefere executar o código do R na estação de trabalho, será possível mudar o contexto de computação para o computador local usando a palavra-chave  **local** .  
  
    ```R  
    rxSetComputeContext ("local")    
    ```  
  
    Para obter uma lista de outras palavras-chave com suporte nesta função, digite `help("rxSetComputeContext")` em uma linha de comando do R.  
  
> [!NOTE]  
> Depois de especificar um contexto de computação, ele permanecerá ativo até você alterá-lo. No entanto, os scripts do R que *não* podem ser executados em um contexto de servidor remoto são executados localmente.  
  
## Calcular estatísticas de resumo  
Para ver como o contexto de computação funciona, tente gerar algumas estatísticas resumidas usando a fonte de dados *sqlFraudDS*.  Lembre-se de que o objeto de fonte de dados define apenas os dados que serão usados; ele não altera o contexto de computação.

+ Para executar o resumo localmente, use *rxSetComputeContext* e especifique a palavra-chave "local".
+ Para criar os mesmos cálculos no computador do SQL Server, mude para o contexto de computação do SQL definido anteriormente.  

  
1.  Chame a função *rxSummary* e passe os argumentos necessários, como a fórmula e a fonte de dados, e atribua os resultados à variável *sumOut*.  
  
    ```R  
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)  
  
    ```  
  
    A linguagem R fornece muitas funções de resumo, mas *rxSummary* dá suporte à execução em diversos contextos de computação remota, incluindo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Para obter mais informações sobre funções semelhantes, consulte [Resumos de Dados](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries) na [Referência do ScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
  
2.  Quando o processamento for concluído, você pode imprimir o conteúdo da variável *sumOut* no console.  
  
    ```R  
    sumOut  
    ```  
  
    > [!NOTE]  
    > Não tente imprimir os resultados antes que eles sejam retornados do computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou você poderá receber um erro.  
  
  
**Resultados**  
  
*Summary Statistics Results for: ~gender + balance + numTrans +*   
 *numIntlTrans + creditLine*    
 *Data: sqlFraudDS (RxSqlServerData Data Source)*    
 *Number of valid observations: 10000*    
 *Name  Mean    StdDev  Min Max ValidObs    MissingObs*    
 *balance       4075.0318 3926.558714            0   25626 100000*    
 *numTrans        29.1061   26.619923 0     100 10000    0           100000*    
 *numIntlTrans     4.0868    8.726757 0      60 10000    0           100000*    
 *creditLine       9.1856    9.870364 1      75 10000    0          100000 Category Counts for gender*    
 *Number of categories: 2*    
 *Number of valid observations: 10000*   
 *Number of missing observations: 0*    
 *gender Counts*    
 *Male   6154*    
  *Female 3846*  
  
## Adicionar valores mínimo e máximo  
Com base nas estatísticas de resumo calculadas, você descobriu algumas informações úteis sobre os dados que deseja inserir na fonte de dados para uso em outros cálculos. Por exemplo, os valores mínimo e máximo podem ser usados para calcular histogramas e, portanto, você decide adicionar os valores alto e baixo à fonte de dados *RxSqlServerData*.  
  
Felizmente, o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] inclui funções otimizadas que podem converter de forma muito eficiente dados de inteiro em dados de fator categórico.  
  
1.  Comece configurando algumas variáveis temporárias.  
  
    ```R  
    sumDF <- sumOut$sDataFrame   
    var <- sumDF$Name    
    ```  
  
2.  Use a variável *ccColInfo* que você criou anteriormente para definir as colunas na fonte de dados.  
  
    Você também adicionará algumas novas colunas calculadas (*numTrans*, *numIntlTrans* e *creditLine*) à coleção de colunas.  
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",  
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")), 
        cardholder = list(type = "factor",  
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
  
    ```  
  
3.  Depois de atualizar a coleção de colunas, você poderá aplicar a instrução a seguir para criar uma versão atualizada da fonte de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definida anteriormente.  
  
    ```R  
    sqlFraudDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        table = sqlFraudTable,   
        colInfo = ccColInfo,        
        rowsPerRead = sqlRowsPerRead)   
    ```  
  
    A fonte de dados *sqlFraudDS* agora inclui as novas colunas adicionadas em *ccColInfo*.  
  
Essas modificações afetam apenas o objeto de fonte de dados no R; nenhum dado novo foi gravado na tabela de banco de dados ainda. No entanto, você pode usar os dados capturados na variável *sumOut* para criar visualizações e resumos. Na etapa seguinte, você aprenderá a fazer isso alternando contextos de computação. 

> [!TIP]
> Se você esquecer qual contexto de computação está usando, use `rxGetComputeContext()`.  Se o valor retornado for `RxLocalSeq Compute Context`, você está usando o contexto de computação local.
  
## Próxima etapa  
[Visualizar dados do SQL Server usando o R &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/visualize-sql-server-data-using-r-data-science-deep-dive.md)  
  
## Etapa anterior  
[Definir e usar contextos de computação &#40;Aprofundamento da ciência de dados&#41;](../../advanced-analytics/r-services/define-and-use-compute-contexts-data-science-deep-dive.md)  
  
  
  
