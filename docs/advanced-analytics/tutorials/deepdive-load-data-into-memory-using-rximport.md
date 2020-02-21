---
title: Carregar dados usando rxImport
description: 'Tutorial 10 do RevoScaleR: Como carregar dados usando a linguagem R no SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b9b3924f2c9b315e519d5f65e68d2006a2a6edf4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74947062"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>Carregar dados na memória usando rxImport (tutorial do SQL Server e do RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este é o tutorial 10 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Neste tutorial, você aprenderá a obter dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usar a função **rxImport** para colocar os dados desejados em um arquivo local. Dessa forma, você pode analisá-los no contexto de computação local repetidamente, sem precisar consultar o banco de dados novamente.

A função [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) pode ser usada para mover dados de uma fonte de dados para um quadro de dados na memória da sessão ou para um arquivo XDF em disco. Se você não especificar um arquivo como destino, os dados serão colocados na memória como um quadro de dados.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Extrair um subconjunto de dados do SQL Server para a memória local

Você decidiu que deseja examinar somente os indivíduos de alto risco mais detalhadamente. A tabela de origem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é grande e, portanto, você obterá as informações apenas sobre os clientes de alto risco. Em seguida, você carregará os dados em uma estrutura de dados na memória da estação de trabalho local.

1. Redefina o contexto de computação como a estação de trabalho local.

    ```R
    rxSetComputeContext("local")
    ```

2. Crie um novo objeto de fonte de dados do SQL Server, fornecendo uma instrução SQL válida no parâmetro *sqlQuery* . Este exemplo obtém um subconjunto das observações com as classificações de risco mais altas. Dessa forma, somente os dados que você realmente precisa são colocados na memória local.

    ```R
    sqlServerProbDS \<- RxSqlServerData(
        sqlQuery = paste("SELECT * FROM ccScoreOutput2",
        "WHERE (ccFraudProb > .99)"),
        connectionString = sqlConnString)
    ```

3. Chame a função [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) para ler os dados em uma estrutura de dados na sessão do R local.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Se a operação tiver sido bem-sucedida, você deverá ver uma mensagem de status como esta: "Linhas lidas: 35, Total de linhas processadas: 35, Tempo total da parte: 0,036 segundos"

4. Agora que as observações de alto risco estão em uma estrutura de dados na memória, você pode usar várias funções do R para manipular a estrutura de dados. Por exemplo, você pode ordenar os clientes pela pontuação de risco e imprimir uma lista dos clientes que apresentam o maior risco.

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**Resultados**

```R
ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1
9.786345    SD   Male  Principal   23456       25            5 75   0.99994382
9.433040    FL Female  Principal   20629       24           28 75   0.99992003
8.556785    NY Female  Principal   19064       82           53 43   0.99980784
8.188668    AZ Female  Principal   19948       29            0 75   0.99972235
7.551699    NY Female  Principal   11051       95            0 75   0.99947516
7.335080    NV   Male  Principal   21566        4            6  75   0.9993482
```

## <a name="more-about-rximport"></a>Mais sobre rxImport

Você pode usar **rxImport** não apenas para mover os dados, mas para transformar os dados no processo de leitura. Por exemplo, é possível especificar o número de caracteres para colunas de largura fixa, fornecer uma descrição das variáveis, definir níveis de colunas de fator e, até mesmo, criar novos níveis a serem usados após a importação.

A função **rxImport** atribui nomes de variáveis às colunas durante o processo de importação, mas você pode indicar novos nomes de variáveis usando o parâmetro *colInfo* ou alterar os tipos de dados usando o parâmetro *colClasses*.

Ao especificar outras operações no parâmetro *transforms* , você pode fazer o processamento básico em cada parte dos dados que é lida.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar nova tabela do SQL Server usando rxDataStep](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)