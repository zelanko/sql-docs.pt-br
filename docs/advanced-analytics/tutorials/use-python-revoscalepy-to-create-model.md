---
title: Usar o Python com revoscalepy para criar um modelo | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 07/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6b7e166971ff74add56bce628838c82a9a6c1128
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>Usar o Python com revoscalepy para criar um modelo

Este exemplo demonstra como você pode criar um modelo de regressão logística no SQL Server, usando um algoritmo do **revoscalepy** pacote.

O **revoscalepy** pacote Python contém objetos, transformações, e algoritmos semelhantes àqueles fornecidos para o **RevoScaleR** pacote para a linguagem R. Com essa biblioteca, você pode criar um contexto de computação, mover dados entre contextos de computação, transformam dados e treinar modelos de previsão usando algoritmos populares, como a regressão logística e linear, árvores de decisão e muito mais.

Para obter mais informações, consulte [novidades revoscalepy?](../python/what-is-revoscalepy.md)

## <a name="prerequisites"></a>Pré-requisitos

> [!IMPORTANT]
> Para executar o código Python no SQL Server, você deve ter instalado o SQL Server de 2017 CTP 2.0 ou posterior, e você deve instalar e habilitar o recurso **serviços de aprendizado de máquina** com Python. Outras versões do SQL Server não dão suporte a integração do Python.

## <a name="run-the-sample-code"></a>Execute o código de exemplo

Esse código realiza as seguintes etapas:

1. Importa as bibliotecas necessárias e funções
2. Cria uma conexão com o SQL Server e cria objetos de fonte de dados para trabalhar com os dados
3. Modifica os dados para que ele pode ser usado pelo algoritmo de regressão logística
4. Chamadas `rx_lin_mod` e define a fórmula usada para ajustar o modelo
5. Gera um conjunto de previsões com base no conjunto de dados original
6. Cria um resumo com base nos valores previstos

Todas as operações são executadas usando uma instância do SQL Server como o contexto de computação.

Em geral, o processo de chamada Python em um contexto de computação remota é semelhante à forma como você usar o R em um contexto de computação remota. Execute o exemplo de como um script de Python da linha de comando ou usando um ambiente de desenvolvimento do Python que inclui os componentes de integração do Python fornecidos nesta versão. No seu código, crie e use um objeto de contexto de computação para indicar onde você deseja que as computações específicas a serem executadas.

> [!NOTE]
> Certifique-se de alterar os nomes de banco de dados e ambiente conforme apropriado.
> 
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
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=PyTestDb;Trusted_Connection=True;'
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

## <a name="discussion"></a>Discussão

Vamos examinar o código e destacar algumas etapas principais.

### <a name="defining-a-data-source-and-compute-context"></a>Definindo um dados de origem e contexto de computação

Uma fonte de dados é diferente de um contexto de computação. O _fonte de dados_ define os dados usados em seu código. O _contexto de computação_ define onde o código será executado.

1. Criar variáveis de Python, tais como `sql_query` e `sql_connection_string`, que definem a fonte e os dados que você deseja usar. Passar essas variáveis para o construtor RxSqlServerData para implementar o **o objeto de fonte de dados** chamado `data_source`.
2. Criar um objeto de contexto de computação usando o **RxInSqlServer** construtor. Neste exemplo, você passa a mesma cadeia de conexão que você definiu anteriormente, supondo que os dados estão na mesma instância do SQL Server que você usará como o contexto de computação. No entanto, a fonte de dados e o contexto de computação podem estar em servidores diferentes. Resultante **objeto de contexto de computação** chamado `sql_cc`.
3. Escolha o contexto de computação ativa. Por padrão, as operações são executadas localmente, o que significa que se você não especificar um contexto de computação diferente, os dados serão obtidos da fonte de dados e ajuste o modelo será executado no ambiente atual do Python.

### <a name="changing-compute-contexts"></a>Alterando os contextos de computação

Neste exemplo, você define o contexto de computação usando um argumento do indivíduo **rx** função.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

O mesmo se aplica na chamada para **rxsummary**, onde o contexto de computação é reutilizado.

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

Você também pode usar a função **rxsetcomputecontext** para alternar entre os contextos de computação que já foi definidos. 

### <a name="setting-the-degree-of-parallelism"></a>Definir o grau de paralelismo

Quando você define o contexto de computação, você também pode definir parâmetros que controlam como os dados são manipulados pelo contexto de computação. Esses parâmetros são diferentes dependendo do tipo de fonte de dados. 

Contextos de computação do SQL Server, você pode definir o tamanho do lote, ou fornecer dicas sobre o grau de paralelismo a ser usado na execução de tarefas.

O exemplo foi executado em um computador com quatro processadores, portanto, definimos o *num_tasks* parâmetro 4. Se você definir esse valor como 0, o SQL Server usa o padrão, que é executar o máximo de tarefas em paralelo possível, nas configurações atuais de MAXDOP para o servidor. No entanto, até mesmo em servidores com vários processadores, o número exato de tarefas que podem ser alocados depende de vários outros fatores, como configurações do servidor e outros trabalhos em execução. 

Para obter mais informações, consulte [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver).

## <a name="related-samples"></a>Exemplos relacionados

Consulte esses exemplos de Python e tutoriais para dicas avançadas e demonstrações de ponta a ponta.

+ [Python no banco de dados para desenvolvedores em SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Criar um modelo de previsão usando Python e o SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [Implantar e consumir Python modelos](../python/publish-consume-python-code.md)

