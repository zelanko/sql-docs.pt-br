---
title: Consultar e modificar os dados do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 8c7007a9-9a8f-4dcd-8068-40060d4f6444
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 66543db80e1d4c6255f6ac64077bfdc10b28dc5d
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="query-and-modify-the-sql-server-data"></a>Consultar e modificar os dados do SQL Server

Agora que você carregou os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], poderá usar as fontes de dados criadas como argumentos para funções do R no [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], para obter informações básicas sobre as variáveis e gerar resumos e histogramas.

Nesta etapa, você usará novamente as fontes de dados para análise rápida e, em seguida, aprimorar os dados.

## <a name="query-the-data"></a>Consultar os dados

Primeiro, obtenha uma lista das colunas e seus tipos de dados.

1.  Use a função **à função rxGetVarInfo** e especifique a fonte de dados que você deseja analisar.
  
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

Nesta etapa, você fornecerá um vetor de cadeia de caracteres que contém as abreviações e, em seguida, mapear esses valores categóricos para os identificadores inteiros originais. Depois que essa variável estiver pronta, você vai usá-la no argumento *colInfo* para especificar que essa coluna seja tratada como um fator. Depois disso, as abreviações serão usadas e a coluna será tratada como um fator sempre que esses dados forem analisados ou importados.

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
  
3. Para criar a fonte de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa os dados atualizados, chame a função *RxSqlServerData* como antes, mas adicione o argumento *colInfo* .
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
    table = sqlFraudTable, colInfo = ccColInfo,
    rowsPerRead = sqlRowsPerRead)
    ```
  
    - No parâmetro *table* , passe a variável *sqlFraudTable*, que contém a fonte de dados criada anteriormente.
    - No parâmetro *colInfo* , passe a variável *ccColInfo* , que contém os tipos de dados de coluna e níveis de fator.
    - Mapear a coluna para as abreviações antes de usá-la como um fator também melhora o desempenho. Para obter mais informações, consulte [R e otimização de dados](https://msdn.microsoft.com/library/mt723575.aspx)
  
4.  Agora você pode usar à função rxGetVarInfo de função para exibir as variáveis na nova fonte de dados.
  
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

[Criar Objetos de Dados do SQL Server usando RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)



