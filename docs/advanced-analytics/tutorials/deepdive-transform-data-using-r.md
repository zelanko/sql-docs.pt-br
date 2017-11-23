---
title: Transformar dados usando R | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 0327e788-94cc-4a47-933b-7c5c027b9208
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 24f37dd048f9eb7f8bb872515958006874a9b3a7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="transform-data-using-r"></a>Transformar dados usando R

O pacote **RevoScaleR** fornece várias funções para transformar os dados em vários estágios da análise:

- **rxDataStep** pode ser usada para criar e transformar subconjuntos de dados.

- **rxImport** dá suporte à transformação de dados conforme os dados são importados para ou de um arquivo XDF ou quadro de dados na memória.

- Embora não sejam destinadas especificamente à movimentação de dados, as funções **rxSummary**, **rxCube**, **rxLinMod**e **rxLogit** dão suporte a transformações de dados.

Nesta seção, você aprenderá a usar essas funções. Vamos começar com rxDataStep.

## <a name="use-rxdatastep-to-transform-variables"></a>Usar o rxDataStep para transformar variáveis

A função rxDataStep processa uma parte de dados de cada vez, de uma fonte de dados de leitura e gravação para outro. Você pode especificar as colunas a serem transformadas, bem como as transformações a serem carregadas, e assim por diante.

Para tornar este exemplo interessante, você usará uma função de outro pacote do R para transformar seus dados.  O pacote **inicialização** é um dos pacotes “recomendados”, o que significa que **inicialização** é incluído com cada distribuição do R, mas não é carregado automaticamente na inicialização. Portanto, o pacote já deve estar disponível na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo usada com o [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)].

Do pacote **inicialização** , você usará a função `inv.logit`, que calcula o inverso de um logit. Ou seja, a função `inv.logit` converte um logit novamente para uma probabilidade na escala [0,1].

> [!TIP] 
> Outra maneira de obter previsões nessa escala seria definir o *tipo* parâmetro **resposta** na chamada original para rxPredict.

1. Comece criando uma fonte de dados para manter os dados destinados à tabela, *ccScoreOutput*.
  
    ```R
    sqlOutScoreDS <- RxSqlServerData( table =  "ccScoreOutput",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
2. Adicione outra fonte de dados para manter os dados da tabela ccScoreOutput2.
  
    ```R
    sqlOutScoreDS2 <- RxSqlServerData( table =  "ccScoreOutput2",  connectionString = sqlConnString, rowsPerRead = sqlRowsPerRead )
    ```
  
    Na nova tabela, você obterá todas as variáveis da tabela *ccScoreOutput* anterior, além da variável recém-criada.
  
3. Defina o contexto de computação como a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. Use a função rxSqlServerTableExists para verificar se a tabela de saída *ccScoreOutput2* já existe; e nesse caso, use a função rxSqlServerDropTable para excluir a tabela.
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput2"))     rxSqlServerDropTable("ccScoreOutput2")
    ```
  
5. Chame a função rxDataStep e especifique as transformações desejadas em uma lista.
  
    ```R
    rxDataStep(inData = sqlOutScoreDS,
        outFile = sqlOutScoreDS2,
        transforms = list(ccFraudProb = inv.logit(ccFraudLogitScore)),
        transformPackages = "boot",
        overwrite = TRUE)
    ```

    Quando define as transformações aplicadas a cada coluna, você também pode especificar todos os pacotes do R adicionais necessários para executar as transformações.  Para obter mais informações sobre os tipos de transformações que podem ser executadas, consulte  [Transforming and Subsetting Data](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform)(Transformação e divisão de dados em subconjuntos)
  
6. Chamada à função rxGetVarInfo para exibir um resumo das variáveis no novo conjunto de dados.
  
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

Observe que as variáveis de fator foram gravadas na tabela como dados de caractere de *ccScoreOutput2* .  Para usá-las como fatores nas próximas análises, use o parâmetro *colInfo* para especificar os níveis.

## <a name="next-step"></a>Próxima etapa

[Carregar dados em memória usando rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)

## <a name="previous-step"></a>Etapa anterior

[Criar e executar Scripts de R](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
