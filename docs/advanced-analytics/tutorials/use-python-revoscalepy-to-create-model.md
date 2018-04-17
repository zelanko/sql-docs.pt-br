---
title: Usar o Python com revoscalepy para criar um modelo | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d886466d7bf4f0c86c1cd9505480a3fadb6e66ef
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>Usar o Python com revoscalepy para criar um modelo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Nesta lição, você aprenderá como executar o código Python de um cliente de desenvolvimento remoto, para criar um modelo de regressão linear no SQL Server. 

## <a name="prerequisites"></a>Prerequisites

+ Esta lição usa dados diferentes de lições anteriores. Você não precisa concluir as lições anteriores primeiro. No entanto, se você concluiu as lições anteriores e tiver um servidor já configurado para executar o Python, usam esse servidor e banco de dados como um contexto de computação.
+ Para executar o código Python usando o SQL Server como uma computação contexto requer o SQL Server 2017 ou posterior. Além disso, você deve instalar explicitamente e, em seguida, habilitar o recurso, **serviços de aprendizado de máquina**, escolhendo a opção de linguagem Python.

    Se você instalou uma versão de pré-lançamento do SQL Server 2017, você deve atualizar para pelo menos a versão RTM. Versões mais recentes do serviço tem contínuo expandir e melhorar a funcionalidade de Python. Alguns recursos deste tutorial podem não funcionar em versões de pré-lançamento.

+ Este exemplo usa um ambiente de Python predefinido, denominado `PYTEST_SQL_SERVER`. O ambiente foi configurado para conter **revoscalepy** e outras bibliotecas necessárias. 

    Se você não tiver um ambiente configurado para executar o Python, você deve fazer isso separadamente. Uma discussão sobre como criar ou modificar os ambientes de Python está fora do escopo deste tutorial. Para obter mais informações sobre como configurar um cliente do Python que contém as bibliotecas corretas, consulte [cliente instalar o Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) e [Python links para ferramentas](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools).

## <a name="remote-compute-contexts-and-revoscalepy"></a>Revoscalepy e contextos de computação remota

Este exemplo demonstra o processo de criação de um modelo de Python no remoto _contexto de computação_, que permite a você trabalhar em um cliente, mas escolha um ambiente remoto, como o SQL Server, Spark ou servidor de aprendizado de máquina, em que o operações, na verdade, são executadas. Usar contextos de computação facilita escrever o código uma vez e implantá-lo a qualquer ambiente.

Para executar o código Python no SQL Server requer o **revoscalepy** pacote. Este é um pacote do Python especial fornecido pela Microsoft, como o **RevoScaleR** pacote para a linguagem R. O **revoscalepy** pacote suporta a criação de contextos de computação e fornece a infraestrutura para transmitir dados e modelos entre uma estação de trabalho local e um servidor remoto. O **revoscalepy** função que ofereça suporte a execução de código no banco de dados é [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

Nesta lição, você usar dados no SQL Server para treinar um modelo linear com base em [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), uma função em **revoscalepy** que dá suporte a regressão em grandes conjuntos de dados. 

Esta lição também demonstra os conceitos básicos de como configurar e, em seguida, usar um **contexto de computação do SQL Server** em Python. Para obter uma discussão de como os contextos de computação trabalhar com outras plataformas e contextos de computação que têm suporte, consulte [contexto de computação para execução de script no servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)

## <a name="prepare-the-database-and-sample-data"></a>Preparar os banco de dados e dados de exemplo

1. Esta lição usa o banco de dados `sqlpy`. Se você não tiver completado qualquer uma das lições anteriores, você pode criar o banco de dados, executando o código a seguir:

    ```sql
    CREATE DATABASE sqlpy;
    GO
    USE sqlpy;
    GO
    ```

    > [!IMPORTANT]
    > Se você quiser usar um banco de dados diferente, certifique-se de editar o código de exemplo e altere o nome do banco de dados na cadeia de conexão.

2. Este exemplo usa o conjunto de dados aérea, que está disponível em R e Python. Depois de criar um banco de dados para as amostras Python, popular uma tabela com os dados conforme descrito aqui: [amostra de dados em RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/sample-built-in-data).

3. Altere o nome desse ambiente para usar um ambiente disponível no cliente.

## <a name="run-the-sample-code"></a>Execute o código de exemplo

Após ter preparado o banco de dados e ter os dados de treinamento armazenados em uma tabela, abra um ambiente de desenvolvimento do Python e executar o exemplo de código.

O código executa as seguintes etapas:

1. Importa as funções e as bibliotecas necessárias.
2. Cria uma conexão com o SQL Server. Cria **fonte de dados** objetos para trabalhar com os dados.
3. Modifica os dados usando **transformações** para que ele pode ser usado pelo algoritmo de regressão logística.
4. Chamadas `rx_lin_mod` e define a fórmula usada para ajustar o modelo.
5. Gera um conjunto de previsões com base nos dados originais.
6. Cria um resumo com base nos valores previstos.

Todas as operações são executadas usando uma instância do SQL Server como o contexto de computação.

> [!NOTE]
> Para ver uma demonstração desse exemplo em execução na linha de comando, consulte este vídeo: [SQL Server 2017 Advanced Analytics com Python](https://www.youtube.com/watch?v=FcoY795jTcc)

### <a name="sample-code"></a>Código de exemplo

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

from pandas import Categorical
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

Uma fonte de dados é diferente de um contexto de computação. O _fonte de dados_ define os dados usados em seu código. O _contexto de computação_ define onde o código será executado. No entanto, eles usar algumas das mesmas informações:

+ Variáveis de Python, tais como `sql_query` e `sql_connection_string`, definir a fonte de dados. 

    Passar essas variáveis para o [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) construtor para implementar o **o objeto de fonte de dados** chamado `data_source`.

+ Você cria um **objeto de contexto de computação** usando o [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserverdata) construtor. Resultante **objeto de contexto de computação** chamado `sql_cc`.

    Novamente, este exemplo usa a mesma cadeia de conexão que você usou na fonte de dados, supondo que os dados estão na mesma instância do SQL Server que você usará como o contexto de computação. 
    
    No entanto, a fonte de dados e o contexto de computação podem estar em servidores diferentes.
 
### <a name="changing-compute-contexts"></a>Alterando os contextos de computação

Depois de definir um contexto de computação, você deve definir o **contexto de computação ativa**. 

Por padrão, a maioria das operações são executadas localmente, o que significa que se você não especificar um contexto de computação diferente, os dados serão obtidos da fonte de dados e o código será executado no ambiente atual do Python.

Há duas maneiras de definir o contexto de computação ativa:
+ Como um argumento de um método ou função
+ Chamando `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>Definir o contexto de computação como um argumento de um método ou função

Neste exemplo, você define o contexto de computação usando um argumento do indivíduo **rx** função.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Este contexto de computação é reutilizado na chamada para [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):.

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>Definir um contexto de computação explicitamente usando rx_set_compute_context

A função [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) permite que você alterne entre computação contextos que já foi definidos.

Depois de ter definido contexto de computação do ativo, ele permanece ativo até você alterá-lo.

### <a name="using-parallel-processing-and-streaming"></a>Usando o processamento paralelo e streaming

Quando você define o contexto de computação, você também pode definir parâmetros que controlam como os dados são manipulados pelo contexto de computação. Esses parâmetros são diferentes dependendo do tipo de fonte de dados.

Contextos de computação do SQL Server, você pode definir o tamanho do lote, ou fornecer dicas sobre o grau de paralelismo a ser usado na execução de tarefas.

+ O exemplo foi executado em um computador com quatro processadores, portanto, o `num_tasks` parâmetro é definido como 4 para permitir o uso máximo de recursos. 
+ Se você definir esse valor como 0, o SQL Server usa o padrão, que é executar o máximo de tarefas em paralelo possível, nas configurações atuais de MAXDOP para o servidor. No entanto, o número exato de tarefas que podem ser alocados depende de vários outros fatores, como configurações do servidor e outros trabalhos em execução.

## <a name="related-samples"></a>Exemplos relacionados

Esses exemplos de Python de adicionais e tutoriais demonstram cenários de ponta a ponta usando fontes de dados mais complexos, como também o uso de contextos de computação remota.

+ [Python no banco de dados para desenvolvedores em SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Criar um modelo de previsão usando Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [Criar um modelo de previsão usando Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
