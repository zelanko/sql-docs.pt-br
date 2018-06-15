---
title: Carregar dados em memória usando rxImport (SQL e R mergulho profundo) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ea5a977f1504a245e270a93a876ac617d8aa6852
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31201698"
---
# <a name="load-data-into-memory-using-rximport-sql-and-r-deep-dive"></a>Carregar dados em memória usando rxImport (SQL e R mergulho profundo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

O [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) função pode ser usada para mover dados de uma fonte de dados em um quadro de dados na memória de sessão ou em um arquivo XDF no disco. Se você não especificar um arquivo como destino, os dados serão colocados na memória como um quadro de dados.

Nesta etapa, você aprenderá a obter dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e, em seguida, use o **rxImport** função colocar os dados de interesse em um arquivo local. Dessa forma, você pode analisá-los no contexto de computação local repetidamente, sem precisar consultar o banco de dados novamente.

## <a name="extract-a-subset-of-data-from-sql-server-to-local-memory"></a>Extrair um subconjunto de dados do SQL Server para a memória local

Você decidiu que você deseja examinar apenas os indivíduos de alto risco mais detalhadamente. A tabela de origem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é grande, para que você deseja obter as informações sobre clientes alto risco. Você, em seguida, carrega dados em um quadro de dados na memória da estação de trabalho local.

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

3. Chame a função [rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport) para ler os dados em um quadro de dados na sessão local do R.

    ```R
    highRisk <- rxImport(sqlServerProbDS)
    ```

    Se a operação foi bem-sucedida, você verá uma mensagem de status como esta: "linhas lidas: 35, processados Total de linhas: 35, tempo Total de bloco: 0.036 segundos"

4. Agora que as observações de alto risco estão em um quadro de dados na memória, você pode usar várias funções de R para manipular o quadro de dados. Por exemplo, você pode ordenar os clientes por sua pontuação de risco e imprima uma lista dos clientes que apresentam o maior risco.

    ```R
    orderedHighRisk <- highRisk[order(-highRisk$ccFraudProb),]
    row.names(orderedHighRisk) <- NULL
    head(orderedHighRisk)
    ```

**Resultados**

*ccFraudLogitScore   state gender cardholder balance numTrans numIntlTrans creditLine ccFraudProb1*

*9.786345    SD   Male  Principal   23456       25            5 75   0.99994382*

*9.433040    FL Female  Principal   20629       24           28 75   0.99992003*

*8.556785    NY Female  Principal   19064       82           53 43   0.99980784*

*8.188668    AZ Female  Principal   19948       29            0 75   0.99972235*

*7.551699    NY Female  Principal   11051       95            0 75   0.99947516*

*7.335080    NV   Male  Principal   21566        4            6  75   0.9993482*

## <a name="more-about-rximport"></a>Mais sobre rxImport

Você pode usar **rxImport** não apenas para mover os dados, mas para transformar os dados no processo de leitura. Por exemplo, é possível especificar o número de caracteres para colunas de largura fixa, fornecer uma descrição das variáveis, definir níveis de colunas de fator e, até mesmo, criar novos níveis a serem usados após a importação.

O **rxImport** função atribui nomes de variáveis para as colunas durante o processo de importação, mas você pode indicar novos nomes de variável usando o *colInfo* parâmetro ou tipos de dados de alteração usando o *colClasses* parâmetro.

Ao especificar outras operações no parâmetro *transforms* , você pode fazer o processamento básico em cada parte dos dados que é lida.

## <a name="next-step"></a>Próxima etapa

[Criar nova tabela do SQL Server usando rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)

## <a name="previous-step"></a>Etapa anterior

[Transformar dados usando o R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

