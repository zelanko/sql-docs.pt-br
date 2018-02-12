---
title: Transformar dados usando R (SQL e R mergulho profundo) | Microsoft Docs
ms.date: 12/24/2017
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
dev_langs:
- R
ms.assetid: 0327e788-94cc-4a47-933b-7c5c027b9208
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d3dbda505155cb8da1f192b2dc36a6889938ccde
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2018
---
# <a name="transform-data-using-r-sql-and-r-deep-dive"></a>Transformar dados usando R (SQL e R mergulho profundo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

O pacote **RevoScaleR** fornece várias funções para transformar os dados em vários estágios da análise:

- **rxDataStep** pode ser usada para criar e transformar subconjuntos de dados.

- **rxImport** dá suporte à transformação de dados conforme os dados são importados para ou de um arquivo XDF ou quadro de dados na memória.

- Embora não sejam destinadas especificamente à movimentação de dados, as funções **rxSummary**, **rxCube**, **rxLinMod**e **rxLogit** dão suporte a transformações de dados.

Nesta seção, você aprenderá a usar essas funções. Vamos começar com [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep).

## <a name="use-rxdatastep-to-transform-variables"></a>Use rxDataStep para transformar variáveis

A função **rxDataStep** processa uma parte dos dados por vez, lendo de uma fonte de dados e gravando em outra. Você pode especificar as colunas a serem transformadas, bem como as transformações a serem carregadas, e assim por diante.

Para tornar este exemplo interessante, vamos usar uma função de outro pacote de R para transformar os dados.  O pacote **inicialização** é um dos pacotes “recomendados”, o que significa que **inicialização** é incluído com cada distribuição do R, mas não é carregado automaticamente na inicialização. Portanto, o pacote já deve estar disponível na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo usada com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

Do **inicialização** do pacote, use a função `inv.logit`, que calcula o inverso de um logit. Ou seja, a função `inv.logit` converte um logit novamente para uma probabilidade na escala [0,1].

> [!TIP] 
> Outra maneira de obter previsões nessa escala seria definir o *tipo* parâmetro **resposta** na chamada original para rxPredict.

1. Comece criando uma fonte de dados para manter os dados destinados para a tabela `ccScoreOutput`.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. Adicionar outra fonte de dados para manter os dados da tabela `ccScoreOutput2`.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    Na nova tabela, armazenar todas as variáveis do anterior `ccScoreOutput` tabela mais a variável recém-criada.
  
3. Defina o contexto de computação como a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Use a função **rxSqlServerTableExists** para verificar se a tabela de saída `ccScoreOutput2` já existe; e nesse caso, use a função **rxSqlServerDropTable** para excluir a tabela.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. Chame a função **rxDataStep** e especifique as transformações desejadas em uma lista.
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    Quando define as transformações aplicadas a cada coluna, você também pode especificar todos os pacotes do R adicionais necessários para executar as transformações.  Para obter mais informações sobre os tipos de transformações que você pode executar, consulte [como transformar e subconjunto dados usando o RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-transform).
  
6. Chame **rxGetVarInfo** para exibir um resumo das variáveis no novo conjunto de dados.
  
    ```R
    rxGetVarInfo(sqlOutScoreDS2)
    ```

    **Resultados**
    
    *Var 1: ccFraudLogitScore, Tipo: numérico*
    
    *Var 2: state, Tipo: caractere*
    
    *Var 3: gender, Tipo: caractere*
    
    *Var 4: cardholder, Tipo: caractere*
    
    *Var 5: balance, Type: integer*
    
    *Var 6: numTrans, Type: integer*
    
    *Var 7: numIntlTrans, Type: integer*
    
    *Var 8: creditLine, Type: integer*
    
    *Var 9: ccFraudProb, Tipo: numérico*

As pontuações de logit originais são preservadas, mas uma nova coluna, *ccFraudProb*, foi adicionada, na qual as pontuações de logit são representadas como valores entre 0 e 1.

Observe que as variáveis de fator foram gravadas para a tabela `ccScoreOutput2` como dados de caractere. Para usá-las como fatores nas próximas análises, use o parâmetro *colInfo* para especificar os níveis.

## <a name="next-step"></a>Próxima etapa

[Carregar dados na memória usando rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)

## <a name="previous-step"></a>Etapa anterior

[Criar e executar scripts do R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
