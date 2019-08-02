---
title: Carregar dados na memória usando RevoScaleR rxImport
description: Tutorial explicativo sobre como carregar dados usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0e498e2aff0f6c21d11e4c34439301f36119257f
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714919"
---
# <a name="load-data-into-memory-using-rximport-sql-server-and-revoscaler-tutorial"></a>Carregar dados na memória usando o rxImport (tutorial de SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lição faz parte do [tutorial do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com SQL Server.

A função [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) pode ser usada para mover dados de uma fonte de dados para um quadro de dados na memória da sessão ou para um arquivo Xdf no disco. Se você não especificar um arquivo como destino, os dados serão colocados na memória como um quadro de dados.

Nesta etapa, você aprende a obter dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e, em seguida, usa a função **rxImport** para colocar os dados de interesse em um arquivo local. Dessa forma, você pode analisá-los no contexto de computação local repetidamente, sem precisar consultar o banco de dados novamente.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Extrair um subconjunto de dados de SQL Server para a memória local

Você decidiu que deseja examinar apenas os indivíduos de alto risco com mais detalhes. A tabela de origem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no é grande, portanto, você deseja obter as informações sobre apenas os clientes de alto risco. Em seguida, você carrega esses dados em um quadro de dados na memória da estação de trabalho local.

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

3. Chame a função [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) para ler os dados em um quadro de dados na sessão do R local.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Se a operação tiver sido bem-sucedida, você deverá ver uma mensagem de status como esta: "Linhas lidas: 35, total de linhas processadas: 35, tempo total da parte: 0, 36 segundos "

4. Agora que as observações de alto risco estão em um quadro de dados na memória, você pode usar várias funções do R para manipular o quadro de dados. Por exemplo, você pode solicitar clientes por sua pontuação de risco e imprimir uma lista dos clientes que representam o risco mais alto.

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

A função **rxImport** atribui nomes de variáveis às colunas durante o processo de importação, mas você pode indicar novos nomes de variáveis usando o parâmetro *colInfo* ou alterar os tipos de dados usando o parâmetro *colClasses* .

Ao especificar outras operações no parâmetro *transforms* , você pode fazer o processamento básico em cada parte dos dados que é lida.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Criar nova tabela do SQL Server usando rxDataStep](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)