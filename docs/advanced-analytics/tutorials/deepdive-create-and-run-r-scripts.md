---
title: Criar e executar scripts de R (SQL e R mergulho profundo) | Microsoft Docs
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 51e8e66f-a0a5-4e96-aa71-f5c870e6d0d4
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 3f26a5850ffe3245029486a2be4406790e36b6ab
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2017
---
# <a name="create-and-run-r-scripts-sql-and-r-deep-dive"></a>Criar e executar scripts de R (SQL e R mergulho profundo)

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Agora configurou as fontes de dados e estabeleceu um ou vários contextos de computação, você está pronto para executar alguns scripts do R de alta potência usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Nesta lição, você pode usar o contexto de computação de servidor para fazer algumas tarefas de aprendizado de máquina comuns:

- Visualizar dados e gerar algumas estatísticas de resumo
- Criar um modelo de regressão linear
- Criar um modelo de regressão logística
- Pontuar novos dados e criar um histograma das pontuações

## <a name="change-compute-context-to-the-server"></a>Alterar o contexto para o servidor de computação

Antes de executar um código do R, você precisa especificar o contexto de computação *atual* ou *ativo* .

1. Para ativar um contexto de computação que você já definiu usando o R, use a função **rxSetComputeContext** , como mostrado aqui:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
    Assim que você executa esta instrução, todos os cálculos subsequentes ocorrerá no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador especificado no *sqlCompute* parâmetro.
  
2. Se você decidir que prefere executar o código do R na estação de trabalho, será possível mudar o contexto de computação para o computador local usando a palavra-chave  **local** .
  
    ```R
    rxSetComputeContext ("local")
    ```
  
    Para obter uma lista de outras palavras-chave com suporte nesta função, digite `help("rxSetComputeContext")` em uma linha de comando do R.
  
3. Depois de especificar um contexto de computação, ele permanecerá ativo até você alterá-lo. No entanto, os scripts do R que *não* podem ser executados em um contexto de servidor remoto são executados localmente.

## <a name="compute-some-summary-statistics"></a>Algumas estatísticas de resumo de computação

Para ver como funciona o contexto de computação, tente gerar algumas estatísticas de resumo usando o `sqlFraudDS` fonte de dados.  Lembre-se de que o objeto de fonte de dados define apenas os dados que você usar; ele não altera o contexto de computação.

+ Para executar o resumo localmente, use **rxSetComputeContext** e especifique o _local_ palavra-chave.
+ Para criar os mesmos cálculos no computador do SQL Server, mude para o contexto de computação do SQL definido anteriormente.

1. Chamar o [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) de função e passar os argumentos necessários, como a fórmula e a fonte de dados e atribuir os resultados para a variável `sumOut`.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    A linguagem R fornece muitas funções de resumidas, mas **rxSummary** dá suporte à execução em diversos contextos de computação remota, incluindo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre funções semelhantes, consulte [resumos de dados usando o RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).
  
2. Quando o processamento é concluído, você pode imprimir o conteúdo do `sumOut` variável para o console.
  
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

 *creditLine 9.1856 9.870364 1 75 10000 0 100000*

 *Contagens de categoria de sexo*

 *Number of categories: 2*

 *Number of valid observations: 10000*

 *Number of missing observations: 0*

 *gender Counts*

 *Male   6154*

  *Female 3846*

## <a name="add-maximum-and-minimum-values"></a>Adicionar valores mínimo e máximo

Com base nas estatísticas de resumo calculadas, você descobriu algumas informações úteis sobre os dados que deseja inserir na fonte de dados para uso em outros cálculos. Por exemplo, os valores mínimo e máximo podem ser usados para calcular os histogramas. Por esse motivo, vamos adicionar os valores altos e baixos para a **RxSqlServerData** fonte de dados.

Felizmente [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] inclui funções otimizadas que podem ser convertido com eficiência dados de inteiro de dados categóricos fator.

1. Comece configurando algumas variáveis temporárias.
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. Use a variável `ccColInfo` que você criou anteriormente para definir as colunas na fonte de dados.
  
    Além disso, adicionar algumas novas colunas computadas (`numTrans`, `numIntlTrans`, e `creditLine`) para a coleção de colunas.
  
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
  
3. Tendo atualizadas a coleção de colunas, aplicar a seguinte instrução para criar uma versão atualizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fonte de dados que você definiu anteriormente.
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    O `sqlFraudDS` fonte de dados agora inclui as novas colunas adicionadas usando `ccColInfo`.
  

Neste ponto, as modificações afetam apenas o objeto de fonte de dados em R; Nenhum dado novo foi gravado na tabela de banco de dados ainda. No entanto, você pode usar os dados capturados no `sumOut` variável para criar visualizações e resumos. A próxima etapa, você aprenderá como fazer isso durante a troca de contextos de computação.

> [!TIP]
> Se você esquecer qual contexto de computação que você está usando, execute `rxGetComputeContext()`.  Um valor de retorno de "Contexto de computação RxLocalSeq" indica que você está executando no contexto de computação local.

## <a name="next-step"></a>Próxima etapa

[Visualizar dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)

## <a name="previous-step"></a>Etapa anterior

[Definir e usar contextos de computação](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
