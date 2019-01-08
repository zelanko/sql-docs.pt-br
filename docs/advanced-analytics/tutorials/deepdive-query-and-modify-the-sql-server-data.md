---
title: Consultar e modificar os dados do SQL Server usando o RevoScaleR - aprendizagem de máquina do SQL Server
description: Tutorial passo a passo sobre como consultar e modificar dados usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 191dd7237307d33d3cdaca5872fee9a09d27f321
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645405"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>Consultar e modificar os dados do SQL Server (tutorial do SQL Server e o RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição é parte do [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar [funções RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Na lição anterior, você carregou os dados na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nesta etapa, você pode explorar e modificar dados usando **RevoScaleR**:

> [!div class="checklist"]
> * Retornar informações básicas sobre as variáveis
> * Criar dados categóricos dos dados brutos

Dados categóricos, ou *variáveis de fator*, são úteis para visualizações de exploração de dados. Você pode usá-los como entradas para histogramas para ter uma ideia da aparência dos dados variáveis.

## <a name="query-for-columns-and-types"></a>Consulta para colunas e tipos

Use um IDE R ou RGui.exe para executar script R. 

Primeiro, obtenha uma lista das colunas e seus tipos de dados. Você pode usar a função [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) e especifique a fonte de dados que você deseja analisar. Dependendo da sua versão do **RevoScaleR**, você também pode usar [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames). 
  
```R
rxGetVarInfo(data = sqlFraudDS)
```

**Resultados**

```R
Var 1: custID, Type: integer
Var 2: gender, Type: integer
Var 3: state, Type: integer
Var 4: cardholder, Type: integer
Var 5: balance, Type: integer
Var 6: numTrans, Type: integer
Var 7: numIntlTrans, Type: integer
Var 8: creditLine, Type: integer
Var 9: fraudRisk, Type: integer
```

## <a name="create-categorical-data"></a>Criar dados categóricos

Todas as variáveis são armazenadas como inteiros, mas algumas delas representam dados categóricos, chamados *variáveis de fator* em R. Por exemplo, a coluna *estado* contém números usados como identificadores para 50 estados, além do Distrito de Colúmbia. Para facilitar a compreensão dos dados, você pode substituir os números por uma lista de abreviações de estado.

Nesta etapa, você cria um vetor de cadeia de caracteres que contém as abreviações e, em seguida, mapear esses valores categóricos para os identificadores inteiros originais. Em seguida, você usa a nova variável na *colInfo* argumento, para especificar que essa coluna seja tratada como um fator. Sempre que você pode analisa os dados ou movê-la, as abreviações são usadas e a coluna será tratada como um fator.

Mapear a coluna para as abreviações antes de usá-la como um fator também melhora o desempenho. Para obter mais informações, consulte [otimização de dados e do R](../r/r-and-data-optimization-r-services.md).

1. Comece criando uma variável do R *stateAbb*e definindo o vetor de cadeias de caracteres para adicionar a ele, da seguinte maneira.
  
    ```R
    stateAbb <- c("AK", "AL", "AR", "AZ", "CA", "CO", "CT", "DC",
        "DE", "FL", "GA", "HI","IA", "ID", "IL", "IN", "KS", "KY", "LA",
        "MA", "MD", "ME", "MI", "MN", "MO", "MS", "MT", "NB", "NC", "ND",
        "NH", "NJ", "NM", "NV", "NY", "OH", "OK", "OR", "PA", "RI","SC",
        "SD", "TN", "TX", "UT", "VA", "VT", "WA", "WI", "WV", "WY")
    ```

2. Em seguida, crie um objeto de informações de coluna, chamado *ccColInfo*, que especifica o mapeamento dos valores inteiros existentes para os níveis categóricos (as abreviações dos estados).
  
    Essa instrução também cria variáveis de fator de gender e cardholder.
  
    ```R
    ccColInfo <- list(
    gender = list(
              type = "factor",
              levels = c("1", "2"),
              newLevels = c("Male", "Female")
              ),
    cardholder = list(
                  type = "factor",
                  levels = c("1", "2"),
                  newLevels = c("Principal", "Secondary")
                   ),
    state = list(
             type = "factor",
             levels = as.character(1:51),
             newLevels = stateAbb
             ),
    balance = list(type = "numeric")
    )
    ```
  
3. Para criar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fonte de dados que usa os dados atualizados, chame o **RxSqlServerData** funcionando como antes, mas adicionar o *colInfo* argumento.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
    table = sqlFraudTable, colInfo = ccColInfo,
    rowsPerRead = sqlRowsPerRead)
    ```
  
    - No parâmetro *table* , passe a variável *sqlFraudTable*, que contém a fonte de dados criada anteriormente.
    - No parâmetro *colInfo* , passe a variável *ccColInfo* , que contém os tipos de dados de coluna e níveis de fator.

4.  Agora, você pode usar a função **rxGetVarInfo** para exibir as variáveis na nova fonte de dados.
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **Resultados**
    
    ```R
    Var 1: custID, Type: integer
    Var 2: gender  2 factor levels: Male Female
    Var 3: state   51 factor levels: AK AL AR AZ CA ... VT WA WI WV WY
    Var 4: cardholder  2 factor levels: Principal Secondary
    Var 5: balance, Type: integer
    Var 6: numTrans, Type: integer
    Var 7: numIntlTrans, Type: integer
    Var 8: creditLine, Type: integer
    Var 9: fraudRisk, Type: integer
    ```

Agora as três variáveis especificadas (*gender*, *state*e *cardholder*) são tratadas como fatores.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Definir e usar contextos de computação](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)