---
title: Criar um modelo do Python – revoscalepy
description: Escreva o script do Python usando as funções revoscalepy para criar modelos de ciência de dados executados remotamente no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5faa8688f3036f80b947ccc5d99c09c4612f26fb
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73724448"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>Use o Python com revoscalepy para criar um modelo executado remotamente no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A biblioteca [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) do Python da Microsoft fornece algoritmos de ciência de dados para exploração de dados, visualização, transformações e análise. Essa biblioteca tem importância estratégica em cenários de integração do Python no SQL Server. Em um servidor de vários núcleos, funções do **revoscalepy** podem ser executadas em paralelo. Em uma arquitetura distribuída com um servidor central e estações de trabalho cliente (computadores físicos separados, todos com a mesma biblioteca **revoscalepy**), você pode escrever um código Python que inicie localmente, mas, em seguida, leve a execução para uma instância remota do SQL Server na qual os dados residam.

Você pode encontrar **revoscalepy** nos seguintes produtos e distribuições da Microsoft:

+ [Serviços de Machine Learning do SQL Server (no banco de dados)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (servidor não SQL, autônomo)](https://docs.microsoft.com/machine-learning-server/index)
+ [Bibliotecas Python do lado do cliente (para estações de trabalho de desenvolvimento)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

Este exercício demonstra como criar um modelo de regressão linear baseado em [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), um dos algoritmos no **revoscalepy** que aceita contexto de computação como entrada. O código que você executará neste exercício leva a execução de código de um ambiente de computação local para remota, habilitado por funções **revoscalepy** que habilitam um contexto de computação remota.

Ao acompanhar este tutorial, você aprenderá a:

> [!div class="checklist"]
> * Usar **revoscalepy** para criar um modelo linear
> * Mudar as operações do contexto de computação local para remota

## <a name="prerequisites"></a>Prerequisites

Os dados de exemplo usados neste exercício são o banco de dados [**flightdata**](demo-data-airlinedemo-in-sql.md).

Você precisa de um IDE para executar o código de exemplo neste artigo e o IDE deve estar vinculado ao executável do Python.

Para praticar uma mudança de contexto de computação, você precisa de uma [estação de trabalho local](../python/setup-python-client-tools-sql.md) e uma instância do mecanismo de banco de dados do SQL Server com [Serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) e Python habilitados. 

> [!Tip]
> Se você não tiver dois computadores, poderá simular um contexto de computação remota em um computador físico instalando aplicativos relevantes. Primeiro, uma instalação dos [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md) funciona como a instância "remota". Segundo, uma instalação das [bibliotecas cliente do Python](../python/setup-python-client-tools-sql.md) opera como o cliente. Você terá duas cópias da mesma distribuição do Python e de bibliotecas Python da Microsoft no mesmo computador. Você precisará acompanhar os caminhos de arquivo e qual cópia do Python.exe você está usando para concluir o exercício com êxito.

## <a name="remote-compute-contexts-and-revoscalepy"></a>Contextos de computação remota e revoscalepy

Este exemplo demonstra o processo de criação de um modelo do Python em um contexto de computação remota, que permite que você trabalhe em um cliente, mas escolha um ambiente remoto, como o SQL Server, o Spark ou o Machine Learning Server, nos quais as operações são de fato executadas. O objetivo do contexto de computação remota é trazer a computação para o local em que os dados residem.

Executar o código Python no SQL Server exige o pacote **revoscalepy**. Esse é um pacote especial do Python fornecido pela Microsoft, semelhante ao pacote **RevoScaleR** para a linguagem R. O pacote **revoscalepy** dá suporte à criação de contextos de computação e fornece a infraestrutura para passar dados e modelos entre uma estação de trabalho local e um servidor remoto. A função **revoscalepy** que dá suporte à execução de código no banco de dados é [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

Nesta lição, você usa dados no SQL Server para treinar um modelo linear baseado em [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), uma função no **revoscalepy** que dá suporte à regressão em conjuntos de dados muito grandes. 

Esta lição também demonstra as noções básicas de como configurar e usar um contexto de computação do **SQL Server** em Python. Para ver uma discussão de como os contextos de computação funcionam com outras plataformas e quais contextos de computação têm suporte, confira [Contexto de computação para execução de script no Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).


## <a name="run-the-sample-code"></a>Execute o código de exemplo

Depois de preparar o banco de dados e armazenar os dados para treinamento em uma tabela, abra um ambiente de desenvolvimento do Python e execute o exemplo de código.

O código realiza as seguintes etapas:

1. Importa as bibliotecas e funções necessárias.
2. Cria uma conexão com o SQL Server. Cria objetos da **fonte de dados** para trabalhar com os dados.
3. Modifica os dados usando **transformações** para que eles possam ser usados pelo algoritmo regressão logística.
4. Chama `rx_lin_mod` e define a fórmula usada para adequar-se ao modelo.
5. Gera um conjunto de previsões com base nos dados originais.
6. Cria um resumo com base nos valores previstos.

Todas as operações são executadas usando uma instância do SQL Server como o contexto de computação.

> [!NOTE]
> Para ver uma demonstração deste exemplo em execução da linha de comando, assista a este vídeo: [Análise Avançada do SQL Server 2017 com Python](https://www.youtube.com/watch?v=FcoY795jTcc)

### <a name="sample-code"></a>Código de exemplo

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

import os

def test_linmod_sql():
    sql_server = os.getenv('PYTEST_SQL_SERVER', '.')
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=sqlpy;Trusted_Connection=True;'
    print("connectionString={0!s}".format(sql_connection_string))

    data_source = RxSqlServerData(
        sql_query = "select top 10 * from airlinedemosmall",
        connection_string = sql_connection_string,

        column_info = {
            "ArrDelay" : { "type" : "integer" },
            "DayOfWeek" : {
                "type" : "factor",
                "levels" : [ "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" ]
            }
        })

    sql_compute_context = RxInSqlServer(
        connection_string = sql_connection_string,
        num_tasks = 4,
        auto_cleanup = False
        )

    #
    # Run linmod locally
    #
    linmod_local = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source)
    #
    # Run linmod remotely
    #
    linmod = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)

    # Predict results
    # 
    predict = rx_predict(linmod, data = rx_import(input_data = data_source))
    summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)
```

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>Como definir uma fonte de dados versus definir um contexto de computação

Uma fonte de dados é diferente de um contexto de computação. A *fonte de dados* define os dados usados em seu código. O contexto de computação define o local em que o código será executado. No entanto, ambos usam algumas das mesmas informações:

+ As variáveis do Python, como `sql_query` e `sql_connection_string`, definem a origem dos dados. 

    Passe essas variáveis para o construtor [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) para implementar o **objeto de fonte de dados** chamado `data_source`.

+ Você cria um **objeto de contexto de computação** usando o construtor [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver). O **objeto de contexto de computação** resultante é chamado de `sql_cc`.

    Este exemplo reutiliza a mesma cadeia de conexão que você usou na fonte de dados, supondo que os dados estejam na mesma instância do SQL Server que você usará como o contexto de computação. 
    
    No entanto, a fonte de dados e o contexto de computação podem estar em servidores diferentes.
 
### <a name="changing-compute-contexts"></a>Como alterar contextos de computação

Depois de definir um contexto de computação, defina o **contexto de computação ativo**. 

Por padrão, a maioria das operações é executada localmente, o que significa que, se você não especificar um contexto de computação diferente, os dados serão buscados da fonte de dados e o código será executado no ambiente atual do Python.

Há duas maneiras de definir o contexto de computação ativo:
+ Como um argumento de um método ou função
+ Chamando `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>Definir o contexto de computação como um argumento de um método ou função

Neste exemplo, você define o contexto de computação usando um argumento da função **rx** individual.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Esse contexto de computação é reutilizado na chamada para [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rx_set_compute_context"></a>Definir um contexto de computação explicitamente usando rx_set_compute_context

A função [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) permite que você alterne entre contextos de computação já definidos.

Depois de definir o contexto de computação ativo, ele permanecerá ativo até você alterá-lo.

### <a name="using-parallel-processing-and-streaming"></a>Como usar processamento paralelo e streaming

Ao definir o contexto de computação, você também pode definir parâmetros que controlam como os dados são processados pelo contexto de computação. Esses parâmetros diferem dependendo do tipo de fonte de dados.

Para contextos de computação do SQL Server, você pode definir o tamanho do lote ou fornecer dicas sobre o grau de paralelismo a ser usado nas tarefas em execução.

+ O exemplo foi executado em um computador com quatro processadores, portanto, o parâmetro `num_tasks` está definido como 4 para permitir o uso máximo de recursos. 
+ Se você definir esse valor como 0, o SQL Server usará o padrão, que é executar o máximo de tarefas em paralelo, nas configurações MAXDOP atuais para o servidor. No entanto, o número exato de tarefas que podem ser alocadas depende de vários outros fatores, como configurações do servidor e outros trabalhos em execução.

## <a name="next-steps"></a>Próximas etapas

Esses tutoriais e exemplos adicionais do Python demonstram cenários de ponta a ponta usando fontes de dados mais complexas, assim como o uso de contextos de computação remota.

+ [Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Criar um modelo de previsão usando Python e SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
