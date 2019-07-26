---
title: Tutorial de RevoScaleR de estatísticas de Resumo de computação
description: Tutorial explicativo sobre como computar estatísticas de resumo estatísticas usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5b1ec344a2ec9728a24d45c47dd80737e6155b01
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469821"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>Calcular estatísticas de resumo em R (tutorial de SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lição faz parte do [tutorial do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com SQL Server.

Ele usa as fontes de dados estabelecidas e contextos de computação criados nas lições anteriores para executar scripts R de alta potência neste. Nesta lição, você usará contextos de computação de servidor local e remoto para as seguintes tarefas:

> [!div class="checklist"]
> * Alternar o contexto de computação para SQL Server
> * Obter estatísticas de resumo sobre objetos de dados remotos
> * Calcular um resumo local

Se você concluiu as lições anteriores, deverá ter estes contextos de computação remota: SQLCOMPUTE e sqlComputeTrace. Avançando, você usará SQLCOMPUTE e o contexto de computação local nas lições subsequentes.

Use um R IDE ou **Rgui** para executar o script r nesta lição.

## <a name="compute-summary-statistics-on-remote-data"></a>Calcular estatísticas de resumo em dados remotos

Antes de executar qualquer código do R remotamente, você precisa especificar o contexto de computação remota. Todos os cálculos subsequentes ocorrem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador especificado no parâmetro SQLCOMPUTE.

Um contexto de computação permanece ativo até você alterá-lo. No entanto, todos os scripts do R que *não podem* ser executados em um contexto de servidor remoto serão automaticamente executados localmente.

Para ver como funciona um contexto de computação, gere estatísticas de resumo na fonte de dados sqlFraudDS no SQL Server remoto. Esse objeto de fonte de dados foi criado na [lição dois](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md) e representa a tabela ccFraudSmall no banco de dados RevoDeepDive. 

1. Alterne o contexto de computação para SQLCOMPUTE criado na lição anterior:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. Chame a função [rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary) e passe os argumentos necessários, como a fórmula e a fonte de dados, e atribua os resultados à variável `sumOut`.
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    A linguagem R fornece muitas funções de resumo, mas **rxSummary** no **RevoScaleR** dá suporte à execução em vários contextos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]computação remota, incluindo. Para obter informações sobre funções semelhantes, consulte resumos de [dados usando RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries).
  
3. Imprima o conteúdo de sumOut no console.
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > Se você receber um erro, aguarde alguns minutos para que a execução seja concluída antes de repetir o comando.

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
  
2. Ao extrair dados de SQL Server, muitas vezes você pode obter melhor desempenho aumentando o número de linhas extraídas para cada leitura, supondo que o tamanho do bloco aumentado possa ser acomodado na memória. Execute o comando a seguir para aumentar o valor do parâmetro *rowsPerRead* na fonte de dados. Anteriormente, o valor de *rowsPerRead* estava definido como 5000.
  
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

4. Volte para o contexto de computação remota para as próximas várias lições.

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Visualizar dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)