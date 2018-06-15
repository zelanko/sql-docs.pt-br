---
title: Consultar e modificar dados do SQL Server (SQL e R mergulho profundo) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 90b836cd09fd0c6f130ff65c531f6077a28c2014
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31202218"
---
# <a name="query-and-modify-the-sql-server-data-sql-and-r-deep-dive"></a>Consultar e modificar dados do SQL Server (SQL e R mergulho profundo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Agora que você carregou os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], poderá usar as fontes de dados criadas como argumentos para funções do R no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para obter informações básicas sobre as variáveis e gerar resumos e histogramas.

Nesta etapa, você reutilizar as fontes de dados para análise rápida e, em seguida, aprimorar os dados.

## <a name="query-the-data"></a>Consultar os dados

Primeiro, obtenha uma lista das colunas e seus tipos de dados.

1.  Use a função [à função rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) e especifique a fonte de dados que você deseja analisar.

    Dependendo de sua versão do RevoScaleR, você também pode usar [rxGetVarNames](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarnames). 
  
    ```R
    rxGetVarInfo(data = sqlFraudDS)
    ```

    **Resultados**
    
    *Var 1: custID, Type: integer*
    
    *Var 2: gender, Type: integer*
    
    *Var 3: state, Type: integer*
    
    *Var 4: cardholder, Type: integer*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: fraudRisk, Type: integer*


## <a name="modify-metadata"></a>Modificar metadados

Todas as variáveis são armazenadas como inteiros, mas algumas delas representam dados categóricos, chamados de *variáveis de fator* no R. Por exemplo, a coluna *state* contém números usados como identificadores para 50 estados, além do Distrito de Colúmbia.  Para facilitar a compreensão dos dados, você pode substituir os números por uma lista de abreviações de estado.

Nesta etapa, você cria um vetor de cadeia de caracteres que contém as abreviações e, em seguida, mapear esses valores categóricos para os identificadores de inteiro original. Em seguida, usar a nova variável no *colInfo* argumento, para especificar que essa coluna ser tratado como um fator. Sempre que você analise os dados ou movê-la, as abreviações são usadas e a coluna é tratada como um fator.

Mapear a coluna para as abreviações antes de usá-la como um fator também melhora o desempenho. Para obter mais informações, consulte [otimização R e dados](..\r\r-and-data-optimization-r-services.md).

1. Comece criando uma variável do R, *stateAbb*, e definindo o vetor de cadeias de caracteres a ser adicionado a ela, da seguinte maneira:
  
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
  
3. Para criar a fonte de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa os dados atualizados, chame a função **RxSqlServerData** como antes, mas adicione o argumento *colInfo* .
  
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
    
    *Var 1: custID, Type: integer*
    
    *Var 2: 2 níveis de fator de sexo: Masculino feminino*
    
    *Var 3: 51 níveis de fator de estado: AK AL AR AZ CA... VT WA WI WV WY*
    
    *Var 4: níveis de fator de titulares 2: entidade secundária*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: fraudRisk, Type: integer*

Agora as três variáveis especificadas (_gender_, _state_e _cardholder_) são tratadas como fatores.

## <a name="next-step"></a>Próxima etapa

[Definir e usar contextos de computação](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)

## <a name="previous-step"></a>Etapa anterior

[Criar objetos de dados do SQL Server usando RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)
