---
title: Usar o Python com revoscalepy para criar um modelo – Machine Learning do SQL Server
description: Escreva script de Python usando revoscalepy funções para criar modelos de ciência de dados que são executados remotamente no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f0d9916414514e0ad0d73c3bb849b9c6e546289d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512444"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>Usar o Python com revoscalepy para criar um modelo que é executado remotamente no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) biblioteca Python da Microsoft fornece algoritmos de ciência de dados para análise, visualização, transformações e exploração de dados. Esta biblioteca tem importância estratégica em cenários de integração de Python no SQL Server. Em um servidor de vários núcleo, **revoscalepy** funções podem ser executadas em paralelo. Em uma arquitetura distribuída com um estações de trabalho de cliente e servidor central (computadores físicos, tudo que tem o mesmo separados **revoscalepy** biblioteca), você pode escrever o código do Python que inicia localmente, mas, em seguida, desloca a execução para um instância remota do SQL Server onde os dados residem.

Você pode encontrar **revoscalepy** nos seguintes produtos da Microsoft e distribuições:

+ [(No banco de dados) de serviços de aprendizado de máquina do SQL Server](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (não-SQL, servidor autônomo)](https://docs.microsoft.com/machine-learning-server/index)
+ [Bibliotecas de Python do lado do cliente (para estações de trabalho de desenvolvimento)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

Este exercício demonstra como criar um modelo de regressão linear com base em [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), um dos algoritmos na **revoscalepy** que aceita o contexto de computação como entrada. O código neste exercício, você executará desloca a execução de código de um local para o ambiente de computação remoto, habilitado por **revoscalepy** contexto de computação de funções que permitem um controle remoto.

Ao concluir este tutorial, você aprenderá como:

> [!div class="checklist"]
> * Use **revoscalepy** para criar um modelo linear
> * Deslocar operações de local para o contexto de computação remota

## <a name="prerequisites"></a>Prerequisites

Dados de exemplo usados neste exercício são o [ **flightdata** ](demo-data-airlinedemo-in-sql.md) banco de dados.

Você precisa de IDE para executar o código de exemplo neste artigo, e o IDE deve ser vinculado para o executável do Python.

Para praticar uma mudança de contexto de computação, você precisa de uma [estação de trabalho local](../python/setup-python-client-tools-sql.md) e uma instância do mecanismo de banco de dados do SQL Server com [serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) e Python habilitado. 

> [!Tip]
> Se você não tiver dois computadores, você pode simular um contexto de computação remota em um computador físico, instalando aplicativos relevantes. Primeiro, uma instalação do [serviços do SQL Server Machine Learning](../install/sql-machine-learning-services-windows-install.md) funciona como a instância "remota". Segundo, uma instalação dos [bibliotecas de cliente de Python opera](../python/setup-python-client-tools-sql.md) como o cliente. Você terá duas cópias da mesma distribuição de Python e bibliotecas de Python de Microsoft no mesmo computador. Você terá que manter o controle de caminhos de arquivo e qual cópia do Python.exe que você está usando para concluir o exercício com êxito.

## <a name="remote-compute-contexts-and-revoscalepy"></a>Revoscalepy e contextos de computação remota

Este exemplo demonstra o processo de criação de um modelo de Python em um contexto de computação remota, que permite a você trabalhar em um cliente, mas escolha um ambiente remoto, como o SQL Server, Spark ou Machine Learning Server, em que as operações, na verdade, são executadas. O objetivo do contexto de computação remota é colocar a computação para onde os dados residem.

Para executar código Python no SQL Server requer o **revoscalepy** pacote. Este é um pacote especial do Python fornecido pela Microsoft, semelhante do **RevoScaleR** pacote para a linguagem R. O **revoscalepy** pacote dá suporte à criação de contextos de computação e fornece a infraestrutura para a passagem de dados e modelos entre uma estação de trabalho local e um servidor remoto. O **revoscalepy** que ofereça suporte a execução de código no banco de dados é de função [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

Nesta lição, você usar dados no SQL Server para treinar um modelo linear com base em [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), uma função na **revoscalepy** que dá suporte a regressão em conjuntos de dados muito grandes. 

Esta lição também demonstra as Noções básicas de como configurar e, em seguida, usar um **contexto de computação do SQL Server** em Python. Para uma discussão sobre como trabalhar de contextos de computação com outras plataformas e contextos de computação que têm suporte, consulte [contexto de computação para execução do script no Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).


## <a name="run-the-sample-code"></a>Executar o código de exemplo

Depois que você preparou o banco de dados e os dados de treinamento armazenados em uma tabela, abra um ambiente de desenvolvimento do Python e executar o exemplo de código.

O código executa as seguintes etapas:

1. Importa as bibliotecas necessárias e funções.
2. Cria uma conexão com o SQL Server. Cria **fonte de dados** objetos para trabalhar com os dados.
3. Modifica os dados usando **transformações** para que ele pode ser usado pelo algoritmo de regressão logística.
4. Chamadas `rx_lin_mod` e define a fórmula usada para ajustar o modelo.
5. Gera um conjunto de previsões com base nos dados originais.
6. Cria um resumo com base nos valores previstos.

Todas as operações são executadas usando uma instância do SQL Server como o contexto de computação.

> [!NOTE]
> Para ver uma demonstração deste exemplo em execução na linha de comando, consulte este vídeo: [Servidor SQL 2017 análises avançadas com o Python](https://www.youtube.com/watch?v=FcoY795jTcc)

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

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>Definindo uma fonte de dados vs. definindo um contexto de computação

Uma fonte de dados é diferente de um contexto de computação. O *fonte de dados* define os dados usados em seu código. O contexto de computação define onde o código será executado. No entanto, eles usarem algumas das mesmas informações:

+ Variáveis de Python, como `sql_query` e `sql_connection_string`, definir a fonte de dados. 

    Passar essas variáveis para o [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) construtor para implementar o **objeto fonte de dados** chamado `data_source`.

+ Você cria um **objeto de contexto de computação** usando o [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) construtor. Resultante **objeto de contexto de computação** é chamado `sql_cc`.

    Novamente, este exemplo usa a mesma cadeia de conexão que você usou na fonte de dados, presumindo que os dados estão na mesma instância do SQL Server que você usará como o contexto de computação. 
    
    No entanto, a fonte de dados e o contexto de computação pode estar em servidores diferentes.
 
### <a name="changing-compute-contexts"></a>Alterar os contextos de computação

Depois de definir um contexto de computação, você deve definir a **contexto de computação ativo**. 

Por padrão, a maioria das operações são executados localmente, o que significa que se você não especificar um contexto de computação diferentes, os dados serão obtidos da fonte de dados e o código será executado em seu ambiente atual do Python.

Há duas maneiras de definir o contexto de computação ativa:
+ Como um argumento de um método ou função
+ Chamando `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>Definir o contexto de computação como um argumento de um método ou função

Neste exemplo, você deve definir o contexto de computação usando um argumento do indivíduo **rx** função.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Esse contexto de computação é reutilizado na chamada para [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>Definir um contexto de computação explicitamente usando rx_set_compute_context

A função [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) permite alternar entre os contextos que já foram definidos de computação.

Depois de definir o contexto de computação do ativo, ele permanecerá ativo até você alterá-lo.

### <a name="using-parallel-processing-and-streaming"></a>Usando o processamento paralelo e streaming

Quando você define o contexto de computação, você também pode definir parâmetros que controlam como os dados são tratados pelo contexto de computação. Esses parâmetros são diferentes dependendo do tipo de fonte de dados.

Para contextos de computação do SQL Server, você pode definir o tamanho do lote, ou fornecer dicas sobre o grau de paralelismo a ser usado na execução de tarefas.

+ O exemplo foi executado em um computador com quatro processadores, portanto, o `num_tasks` parâmetro for definido como 4 para permitir o uso máximo de recursos. 
+ Se você definir esse valor como 0, o SQL Server usa o padrão, que é executar tantas tarefas em paralelo possível, sob as configurações de MAXDOP atuais para o servidor. No entanto, o número exato de tarefas que podem ser alocados depende de muitos outros fatores, como configurações do servidor e outros trabalhos em execução.

## <a name="next-steps"></a>Próximas etapas

Esses exemplos em Python e tutoriais adicionais demonstram cenários de ponta a ponta usando fontes de dados mais complexos, bem como o uso de contextos de computação remota.

+ [Python no banco de dados para desenvolvedores do SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Criar um modelo preditivo usando o Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
