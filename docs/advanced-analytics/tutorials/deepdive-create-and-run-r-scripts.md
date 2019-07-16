---
title: Calcular estatísticas de resumo RevoScaleR tutorial – Machine Learning do SQL Server
description: Tutorial passo a passo sobre como calcular estatísticas de resumo estatísticas usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 945b7cb32c64c343ca7bb5ab2aab4169fd7bea24
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962283"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>Calcular estatísticas de resumo em R (tutorial do SQL Server e o RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição é parte do [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar [funções RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Ele usa as fontes de dados estabelecida e contextos de computação criados nas lições anteriores para executar scripts de R de alta potência neste. Nesta lição, você irá usar contextos de computação de servidor local e remoto para as seguintes tarefas:

> [!div class="checklist"]
> * Alternar o contexto de computação para o SQL Server
> * Obter estatísticas de resumo em objetos de dados remotos
> * Um resumo de local de computação

Se você concluiu as lições anteriores, você deve ter esses contextos de computação remota: sqlCompute e sqlComputeTrace. Mais adiante, que você usa serão sqlCompute e o local contexto de computação nas lições subsequentes.

Usar um IDE R ou **Rgui** para executar o script de R nesta lição.

## <a name="compute-summary-statistics-on-remote-data"></a>Calcular estatísticas de resumo sobre os dados remotos

Antes de executar qualquer código R remotamente, você precisará especificar o contexto de computação remota. Todos os cálculos posteriores ocorrerá na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador especificado em de *sqlCompute* parâmetro.

Um contexto de computação permanece ativo até você alterá-lo. No entanto, os scripts do R que *não é possível* execução em um contexto de servidor remoto será automaticamente executado localmente.

Para ver como funciona um contexto de computação, gere estatísticas resumidas sobre a fonte de dados sqlFraudDS no SQL Server remoto. Esse objeto de fonte de dados foi criado no [lição dois](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md) e representa a tabela ccFraudSmall no banco de dados RevoDeepDive. 

1. Alterne o contexto de computação para sqlCompute criado na lição anterior:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. Chame o [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) de função e passe os argumentos necessários, como a fórmula e fonte de dados e atribua os resultados à variável `sumOut`.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    A linguagem R fornece muitas funções de resumidas, mas **rxSummary** na **RevoScaleR** dá suporte à execução em diversos contextos de computação remota, incluindo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre funções semelhantes, consulte [resumos de dados usando o RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).
  
3. Imprima o conteúdo do sumOut no console.
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > Se você receber um erro, aguarde alguns minutos para a execução seja concluída antes de tentar novamente o comando.

**Resultados**

```R
Summary Statistics Results for: ~gender + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Number of valid observations: 10000

 Name  Mean    StdDev  Min Max ValidObs    MissingObs
 balance       4075.0318 3926.558714            0   25626 100000
 numTrans        29.1061   26.619923 0     100 10000    0           100000
 numIntlTrans     4.0868    8.726757 0      60 10000    0           100000
 creditLine       9.1856    9.870364 1      75 10000    0          100000
 
 Category Counts for gender
 Number of categories: 2
 Number of valid observations: 10000
 Number of missing observations: 0

 gender Counts
  Male   6154
  Female 3846
```

## <a name="create-a-local-summary"></a>Criar um resumo local

1. Altere o contexto de computação para fazer todo o seu trabalho localmente.
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. Ao extrair dados do SQL Server, você geralmente pode obter um melhor desempenho, aumentando o número de linhas extraídas para cada leitura, supondo que o tamanho do maior bloco pode ser acomodado em memória. Execute o seguinte comando para aumentar o valor para o *rowsPerRead* parâmetro na fonte de dados. Anteriormente, o valor de *rowsPerRead* estava definido como 5000.
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. Chame **rxSummary** na nova fonte de dados.
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   Os resultados reais devem ser iguais a quando você executa **rxSummary** no contexto do computador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No entanto, a operação pode ser mais rápida ou mais lenta. Depende muito da conexão com seu banco de dados, pois os dados estão sendo transferidos para o computador local para análise.

4. Alterne novamente para o controle remoto de contexto de computação para as próximas várias lições.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Visualizar dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)