---
title: Modificar dados SQL usando o RevoScaleR
description: Saiba como consultar e modificar dados usando a linguagem R no SQL Server, especificamente a função RevoScaleR.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d66452796f3c3cd669784ae7233fb9dcf8e5bc5c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195098"
---
# <a name="query-and-modify-the-sql-server-data-sql-server-and-revoscaler-tutorial"></a>Consultar e modificar os dados do SQL Server (tutorial do SQL Server e RevoScaleR)
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este é o tutorial 3 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

No tutorial anterior, você carregou os dados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Neste tutorial, você pode explorar e modificar dados usando o **RevoScaleR**:

> [!div class="checklist"]
> * Retornar informações básicas sobre as variáveis
> * Criar dados categóricos de dados brutos

Os dados categóricos (ou *variáveis de fator*) são úteis para visualizações de dados exploratórios. Você pode usá-los como entradas para histogramas para ter uma ideia de qual é a aparência dos dados de variável.

## <a name="query-for-columns-and-types"></a>Consultar colunas e tipos

Use um IDE do R ou o RGui.exe para executar o script do R. 

Primeiro, obtenha uma lista das colunas e seus tipos de dados. Você pode usar a função [rxGetVarInfo](/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) e especificar a fonte de dados que você deseja analisar. Dependendo de sua versão de **RevoScaleR**, você poderia usar [rxGetVarNames](/machine-learning-server/r-reference/revoscaler/rxgetvarnames). 
  
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

Todas as variáveis são armazenadas como inteiros, mas algumas delas representam dados categóricos, chamados de *variáveis de fator* no R. Por exemplo, a coluna *state* contém números usados como identificadores para 50 estados, além do Distrito de Colúmbia. Para facilitar a compreensão dos dados, você pode substituir os números por uma lista de abreviações de estado.

Nesta etapa, você criará um vetor de cadeia de caracteres que contém as abreviações e, em seguida, mapeará esses valores categóricos para os identificadores inteiros originais. Em seguida, usará a nova variável no argumento *colInfo* para especificar que essa coluna deve ser tratada como um fator. Sempre que analisar os dados ou movê-los, as abreviações serão usadas e a coluna será tratada como um fator.

Mapear a coluna para as abreviações antes de usá-la como um fator também melhora o desempenho. Para obter mais informações, confira [R e otimização de dados](../r/r-and-data-optimization-r-services.md).

1. Comece criando uma variável do R, *stateAbb*, e definindo o vetor de cadeias de caracteres a ser adicionado a ela, da seguinte maneira.
  
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
  
3. Para criar a fonte de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa os dados atualizados, chame a função **RxSqlServerData** como antes, mas adicione o argumento *colInfo*.
  
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
> [Definir e usar contextos de computação](../../machine-learning/tutorials/deepdive-define-and-use-compute-contexts.md)