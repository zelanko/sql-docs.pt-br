---
title: Extensão da linguagem de programação Python
description: Saiba mais sobre a execução de código do Python e as bibliotecas do Python integradas no SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f3825a2b5085bf5a6e144a602c36cb20ccaca430
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688278"
---
# <a name="python-language-extension-in-sql-server"></a>Extensão de linguagem Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A extensão do Python faz parte do complemento SQL Server Serviços de Machine Learning ao mecanismo de banco de dados relacional. Ele adiciona um ambiente de execução Python, a distribuição Anaconda com o tempo de execução e o intérprete do Python 3,5, bibliotecas e ferramentas padrão e as bibliotecas de produtos da Microsoft para Python: [revoscalepy](../python/ref-py-revoscalepy.md) para análise em escala e [microsoftml](../python/ref-py-microsoftml.md) para algoritmos de aprendizado de máquina. 

A integração do Python é instalada como [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md).

A instalação do intérprete e do tempo de execução do Python 3,5 garante a compatibilidade quase completa com soluções Python padrão. O Python é executado em um processo separado do SQL Server, para garantir que as operações do banco de dados não sejam comprometidas.

## <a name="python-components"></a>Componentes do Python

SQL Server inclui pacotes de software livre e proprietários. O tempo de execução do Python instalado pela instalação é Anaconda 4,2 com Python 3,5. O tempo de execução do Python é instalado independentemente das ferramentas SQL e é executado fora dos processos principais do mecanismo, na estrutura de extensibilidade. Como parte da instalação do Serviços de Machine Learning com o Python, você deve consentir os termos da licença pública GNU. 

SQL Server não modifica os executáveis do Python, mas você deve usar a versão do Python instalada pela instalação, pois essa versão é aquela na qual os pacotes proprietários são compilados e testados. Para obter uma lista de pacotes com suporte na distribuição Anaconda, consulte o site de análise de continuidade: [Lista de pacotes Anaconda](https://docs.continuum.io/anaconda/packages/pkg-docs).

A distribuição Anaconda associada a uma instância específica do mecanismo de banco de dados pode ser encontrada na pasta associada à instância. Por exemplo, se você instalou SQL Server mecanismo de banco de dados 2017 com Serviços de Machine Learning e Python na instância padrão, `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`procure em.

Os pacotes do Python adicionados pela Microsoft para cargas de trabalho paralelas e distribuídas incluem as bibliotecas a seguir.

| Biblioteca | Descrição |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Dá suporte a objetos de fonte de dados e exploração de dados, manipulação, transformação e visualização. Ele dá suporte à criação de contextos de computação remota, bem como a vários modelos escalonáveis de aprendizado de máquina, como o **rxLinMod**. Para obter mais informações, consulte [módulo revoscalepy com SQL Server](../python/ref-py-revoscalepy.md).  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Contém algoritmos de aprendizado de máquina que foram otimizados para velocidade e precisão, bem como transformações em linha para trabalhar com texto e imagens. Para obter mais informações, consulte [módulo microsoftml com SQL Server](../python/ref-py-microsoftml.md). |

Microsoftml e revoscalepy estão rigidamente acoplados; as fontes de dados usadas em microsoftml são definidas como objetos revoscalepy. Limitações de contexto de computação na transferência de revoscalepy para microsoftml. Ou seja, todas as funcionalidades estão disponíveis para operações locais, mas a alternância para um contexto de computação remota requer RxInSqlServer.

## <a name="using-python-in-sql-server"></a>Usando o Python no SQL Server

Você importa o módulo **revoscalepy** para seu código Python e, em seguida, chama funções do módulo, como qualquer outra função do Python.

As fontes de dados com suporte incluem bancos de dados ODBC, SQL Server e formato de arquivo XDF para trocar dados com outras fontes, ou com soluções de R. Os dados de entrada para Python devem ser tabulares. Todos os resultados do Python devem ser retornados na forma de um quadro de dados do pandas.

Os contextos de computação com suporte incluem o contexto de computação local ou remoto SQL Server. Um contexto de computação remota refere-se à execução de código que começa em um computador como uma estação de trabalho, mas, em seguida, alterna a execução do script para um computador remoto. Alternar o contexto de computação requer que ambos os sistemas tenham a mesma biblioteca revoscalepy.

Contexto de computação local, como você pode esperar, inclui a execução de código Python no mesmo servidor que a instância do mecanismo de banco de dados, com código dentro de T-SQL ou inserido em um procedimento armazenado. Você também pode executar o código de um IDE Python local e fazer com que o script seja executado no computador SQL Server, definindo um contexto de computação remota.

## <a name="execution-architecture"></a>Arquitetura de execução

Os diagramas a seguir descrevem a interação de SQL Server componentes com o tempo de execução do Python em cada um dos cenários com suporte: execução de script no banco de dados e execução remota de um terminal do Python, usando um contexto de computação SQL Server.

### <a name="python-scripts-executed-in-database"></a>Scripts Python executados no banco de dados

Ao executar o Python "Inside" SQL Server, você deve encapsular o script Python dentro de um procedimento armazenado especial, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Depois que o script tiver sido inserido no procedimento armazenado, qualquer aplicativo que possa fazer uma chamada de procedimento armazenado poderá iniciar a execução do código Python.  Depois disso SQL Server gerencia a execução de código conforme resumido no diagrama a seguir.

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Uma solicitação para o tempo de execução do Python é indicada `@language='Python'` pelo parâmetro passado para o procedimento armazenado. SQL Server envia essa solicitação ao serviço Launchpad.
2. O serviço Launchpad inicia o iniciador apropriado; Nesse caso, PythonLauncher.
3. PythonLauncher inicia o processo Python35 externo.
4. O BxlServer coordena com o tempo de execução do Python para gerenciar trocas de dados e o armazenamento de resultados de trabalho.
5. O satélite do SQL gerencia as comunicações sobre tarefas e processos relacionados com o SQL Server.
6. O BxlServer usa o satélite do SQL para comunicar o status e os resultados para SQL Server.
7. SQL Server obtém resultados e fecha as tarefas e os processos relacionados.

### <a name="python-scripts-executed-from-a-remote-client"></a>Scripts do Python executados de um cliente remoto

Você pode executar scripts Python de um computador remoto, como um laptop, e fazer com que eles sejam executados no contexto do computador do SQl Server, se essas condições forem atendidas:

+ Você cria os scripts adequadamente
+ O computador remoto instalou as bibliotecas de extensibilidade usadas pelo Serviços de Machine Learning. O pacote [revoscalepy](../python/ref-py-revoscalepy.md) é necessário para usar contextos de computação remota.

O diagrama a seguir resume o fluxo de trabalho geral quando os scripts são enviados de um computador remoto.

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. Para funções com suporte no **revoscalepy**, o tempo de execução do Python chama uma função de vinculação que, por sua vez, chama BxlServer.
2. O BxlServer está incluído com Serviços de Machine Learning (no banco de dados) e é executado em um processo separado do tempo de execução do Python.
3. BxlServer determina o destino de conexão e inicia uma conexão usando ODBC, passando credenciais fornecidas como parte da cadeia de conexão no script Python.
4. BxlServer abre uma conexão com a instância de SQL Server.
5. Quando um tempo de execução de script externo é chamado, o serviço Launchpad é invocado, o que, por sua vez, inicia o iniciador apropriado: nesse caso, PythonLauncher. dll. Depois disso, o processamento do código Python é tratado em um fluxo de trabalho semelhante àquele quando o código Python é invocado de um procedimento armazenado no T-SQL.
6. PythonLauncher faz uma chamada para a instância do Python que está instalada no computador SQL Server.
7. Os resultados são retornados ao BxlServer.
8. O satélite do SQL gerencia a comunicação com SQL Server e a limpeza de objetos de trabalho relacionados.
9. SQL Server passa os resultados de volta para o cliente.

## <a name="next-steps"></a>Próximas etapas

+ [módulo revoscalepy no SQL Server](../python/ref-py-revoscalepy.md)
+ [referência de função revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [Estrutura de extensibilidade no SQL Server](extensibility-framework.md)
+ [Extensões de R e Machine Learning no SQL Server](extension-r.md)
+ [Obter informações do pacote do Python](../package-management/python-package-information.md)
+ [Instalar pacotes do Python com o sqlmlutils](../package-management/install-additional-python-packages-on-sql-server.md)
