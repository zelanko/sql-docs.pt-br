---
title: Configurar ferramentas de cliente do Python para uso com o SQL Server Machine Learning | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6f6823870060992586756dffa93aac6937d27d65
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "40401296"
---
# <a name="set-up-python-client-tools-for-use-with-sql-server-machine-learning"></a>Configurar Python ferramentas de cliente para uso com o SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integração do Python está disponível começando no SQL Server 2017 ou posterior, quando você adiciona que o suporte do Python para serviços do Machine Learning (no banco de dados). Para obter mais informações, consulte [instalar o SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md).

Neste artigo, saiba como configurar estações de trabalho de desenvolvimento para que você pode se conectar a um SQL Server remoto habilitado para o Python.

### <a name="evaluation-and-independent-development"></a>Desenvolvimento independente e avaliação
 
Se você tiver a edição de desenvolvedor e o plano para trabalhar localmente em um script Python que você planeja mover para o SQL Server, você poderá pular para [instalar um IDE](#install-ide) e apontar a ferramenta para bibliotecas de Python locais usadas pelo SQL Server.

> [!Tip]
> Para obter uma demonstração e vídeo passo a passo, consulte [executar R e Python remotamente no SQL Server de qualquer IDE ou de blocos de anotações do Jupyter](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/) ou isso [vídeo do YouTube](https://youtu.be/D5erljpJDjE).

## <a name="1---install-python-packages"></a>1 – instalar pacotes Python

Estações de trabalho locais devem ter as mesmas versões de pacote do Python como aqueles no SQL Server: revoscalepy e microsftml. Pacotes adicionais Python estão disponíveis, mas são mais comumente usados com outros cenários em um contexto de Machine Learning Server autônomo (não da instância). 

1. Baixe o script de shell de instalação do [ https://aka.ms/mls93-py ](https://aka.ms/mls93-py) (ou use [ https://aka.ms/mls-py ](https://aka.ms/mls-py) para o 9.2. versão). O script instala o Anaconda 4.2.0, que inclui o Python 3.5.2, juntamente com todos os pacotes listados anteriormente.

  Componentes do Python são fornecidos por meio [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054&clcid=1033). Se você precisar de uma versão diferente, consulte [CAB downloads](../install/sql-ml-cab-downloads.md)

2. Abrir janela do PowerShell com permissões de administrador com privilégios elevados (clique com botão direito **executar como administrador**).

3. Vá para a pasta na qual você baixou o instalador e execute o script. Adicionar o `-InstallFolder` argumento de linha de comando para especificar um local de pasta para as bibliotecas. Por exemplo: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls")
   ```

   Instalação leva algum tempo para concluir. Você pode monitorar o progresso na janela do PowerShell. Quando a instalação for concluída, você tem um conjunto completo de pacotes. Por exemplo, se você especificou `C:\mspythonlibs` como o nome da pasta, você encontraria os pacotes em `C:\mspythonlibs\Lib\site-packages`. Caso contrário, a pasta padrão é `C:\Program Files\Microsoft\PyForMLS1`.

O script de instalação não modifica a variável de ambiente PATH em seu computador para que os módulos que você acabou de instalar e um novo interpretador de python não ficam automaticamente disponíveis para suas ferramentas. Para obter ajuda sobre como vincular o interpretador do Python e bibliotecas para ferramentas, consulte [5 - instalar um IDE](#install-ide).

<a name="python-tool"></a>
 
## <a name="2---open-a-python-prompt"></a>2 - Abra um prompt de Python

Integração do Python no Microsoft inclui ferramentas internas e dados, além das bibliotecas específicas do produto, como revoscalepy e microsoftml. Os itens a seguir estão disponíveis em instâncias de cliente e servidor quando a instalação for concluída:

+ Dados de exemplo do Python
+ Distribuição do anaconda 4.2 
+ Pythonw.exe e Python executáveis python.exe

> [!Tip] 
> É recomendável o [FAQ de Python para Windows](https://docs.python.org/3/faq/windows.html) para obter informações sobre como executar programas de Python no Windows purppose geral.

### <a name="on-client-workstations"></a>Em estações de trabalho do cliente

Para usar o executável do Python instalado pelo script de instalação:

1. Vá para `C:\Program Files\Microsoft\PyForMLS\python.exe` ou de qualquer local em que você escolheu para o caminho de instalação.

2. Clique com botão direito **Python.exe** e selecione **executar como administrador** para abrir uma janela interativa de linha de comando.

### <a name="on-sql-server"></a>No SQL Server

Instalação do SQL Server adiciona recursos e ferramentas padrão do Python para uma instância de servidor. Se você estiver usando a edição de desenvolvedor e quiser verificar a versão do Python ou execute comandos ad hoc:

1. Vá para `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`.

2. Clique com botão direito **Python.exe** e selecione **executar como administrador** para abrir uma janela interativa de linha de comando.

> [!Note]
> Em geral, para evitar contenção de recursos, é recomendável que você **não** executar Python da biblioteca de instância no servidor, se você achar que é possível que a instância do SQL Server é executar código Python. No entanto, usando as ferramentas na biblioteca de instância pode ser útil se você está tentando depurar um problema que ocorre somente quando em execução no SQL Server e para exibir mensagens de erro mais detalhadas, ou certifique-se de que todos os pacotes necessários estão instalados.

## <a name="3---permissions"></a>3 - permissões

Para se conectar a uma instância do SQL Server para executar scripts e carregar dados, você deve ter um logon válido no servidor de banco de dados. Você pode usar um logon SQL ou a autenticação integrada do Windows. Em geral, é recomendável que você usa a autenticação integrada do Windows, mas usar o logon do SQL é mais simples para alguns cenários.

No mínimo, a conta usada para executar o código deve ter permissão para ler os bancos de dados você está trabalhando, além de permissão especial executar qualquer SCRIPT externo. A maioria dos desenvolvedores também exigem permissões para criar novos objetos na forma de procedimentos armazenados que contém o script e gravar dados em tabelas que contêm dados de treinamento ou pontuados dados. 

Peça ao administrador de banco de dados para configurar as seguintes permissões para a conta, no banco de dados em que você usar o Python:

+ **EXECUTE ANY EXTERNAL SCRIPT** para executar o Python no servidor.
+ **db_datareader** privilégios para executar as consultas usadas para treinar o modelo.
+ **db_datawriter** para gravar dados de treinamento ou dados de pontuação.
+ **db_owner** para criar objetos, como procedimentos armazenados, tabelas, funções. 
  Você também precisa **db_owner** criar bancos de dados de exemplo e teste. 

Se seu código exigir pacotes que não são instalados por padrão com o SQL Server, organize-se com o administrador de banco de dados para ter os pacotes instalados com a instância. SQL Server é um ambiente seguro e há restrições sobre onde os pacotes podem ser instalados. Instalação de ad hoc de pacotes como parte do seu código não é recomendável, mesmo se você tiver direitos. Além disso, sempre considere as implicações de segurança antes de instalar novos pacotes na biblioteca do servidor.

## <a name="4---test-connections"></a>4 - testar conexões

Depois de instalar todas as ferramentas e bibliotecas, você deve se conectar ao servidor e verifique se que você pode criar um contexto de computação, ou se o Python pode se comunicar com o SQL Server.

### <a name="verify-that-revoscalepy-works-from-the-python-command-line"></a>Verifique se que esse revoscalepy funciona na linha de comando do Python

Para verificar se o **revoscalepy** módulo pode ser carregado, execute o seguinte código de exemplo em um prompt de comando interativo do Python. O código gera um resumo de dados usando os dados de exemplo do Python e [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary). 

```Python
import os
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions
sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)
ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay+DayOfWeek", ds)
print(summary)
```

O caminho de dados de exemplo é impresso para que você possa determinar qual instância do Python está sendo chamada.

### <a name="verify-that-python-can-be-called-from-a-local-sql-server"></a>Verifique se que o Python pode ser chamado de um SQL Server local

Em um ambiente de desenvolvimento local, verifique se que o Python está se comunicando com o local [instância do SQL Server configurada para execução de scripts externos](../install/sql-machine-learning-services-windows-install.md). Usar o SQL Server Management Studio para abrir uma nova **consulta** janela e executar qualquer Python simples de comandos no contexto de um procedimento armazenado:

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'print(3+4)'
```

Pode levar algum tempo para iniciar o tempo de execução do Python pela primeira vez, mas se não houver nenhum erro, você sabe que o Launchpad do SQL Server está funcionando, e o Python pode ser iniciado a partir do SQL Server.

Para verificar se **revoscalepy** está disponível na biblioteca de instância do SQL Server, execute o script com base em [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary), com algumas pequenas modificações para gerar resultados compatível com o SQL Server. 

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

Como rx_summary retorna um objeto do tipo `class revoscalepy.functions.RxSummary.RxSummaryResults`, que contém vários elementos, para manipular os resultados no SQL Server, é possível extrair apenas o quadro de dados em um formato tabular.

### <a name="verify-python-execution-in-sql-server-as-remote-compute-context"></a>Verificar a execução de Python no SQL Server como o contexto de computação remota

Se você tiver instalado **revoscalepy** em seu ambiente de desenvolvimento local do Python, você deve ser capaz de se conectar a uma instância remota do SQL Server 2017 no qual Python foi habilitado e executar um exemplo de código semelhante usando o servidor como o contexto de computação. 

Para esse script executar, especifique um nome de servidor válido e um banco de dados existente. Esse script em particular não usa o banco de dados, mas a cadeia de caracteres de conexão requer a ele.

```Python
import os
from revoscalepy import rx_summary, RxOptions, RxXdfData, RxSqlServerData, RxInSqlServer

# define connection string and compute context
sql_conn_string="Driver=SQL Server;Server=<server-name>;Database=TestDB;Trusted_Connection=True"
sqlcc = RxInSqlServer(
    connection_string = sql_conn_string,
    num_tasks = 1,
    auto_cleanup = False,
    console_output = True,
    execution_timeout_seconds = 0,
    wait = True
    )
rx_set_compute_context(sqlcc)

# get sample data and path
sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

# generate summary
ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay+DayOfWeek", ds)
print(summary)
```

Neste exemplo, o objeto de resumo é retornado para o console, em vez de retornados dados tabulares bem formados para o SQL Server. 

Além disso, porque [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) foi invocado, os dados de exemplo são carregados na pasta exemplos no computador do SQL Server e não de sua pasta de exemplos de local.


<a name="install-ide"></a>

## <a name="5---install-an-ide"></a>5 - instalar um IDE

Se você simplesmente estiver depurando scripts da linha de comando, você pode obter com as ferramentas padrão do Python. No entanto, se você estiver desenvolvendo novas soluções, ou trabalhando em um cliente remoto, recomendamos o uso de um IDE do Python completo. Opções populares são:

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/) com Python
+ [Ferramentas de IA para Visual Studio](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Python no Visual Studio Code](https://code.visualstudio.com/docs/languages/python)
+ Ferramentas de terceiros populares, como PyCharm, Spyder e Eclipse

É recomendável o Visual Studio porque ele dá suporte a projetos de banco de dados, bem como projetos de aprendizado de máquina. Para obter ajuda sobre como configurar um ambiente de Python, consulte [Gerenciando ambientes do Python no Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio).

Porque com frequência, os desenvolvedores trabalham com várias versões do Python, a instalação não adiciona Python ao seu caminho. Para usar o executável do Python e bibliotecas instaladas pela instalação, vincular seu IDE para **Python.exe** no caminho que também fornece revoscalepy e microsoftml. Por exemplo, para um projeto do Python no Visual Studio, seu ambiente personalizado especificaria `C:\Program Files\Microsoft\PyForMLS`, `C:\Program Files\Microsoft\PyForMLS\python.exe` e `C:\Program Files\Microsoft\PyForMLS\pythonw.exe` para **caminho do prefixo**, **interpretu**e  **Interpretador de janela**, respectivamente.

Para obter orientação adicional, consulte [as ferramentas do Python de Link e IDEs](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools). O artigo foi escrito para o Microsoft Machine Learning Server, portanto, os caminhos de Python são diferentes, mas ele mostra como um link para as bibliotecas de Python de várias ferramentas.

## <a name="next-steps"></a>Próximas etapas

Agora que você tem uma conexão de trabalho para o SQL Server e ferramentas, percorra um tutorial para obter uma olhada nas funções revoscalepy e alternar contextos de computação.

> [!div class="nextstepaction"]
> [Criar um modelo usando revoscalepy e um contexto de computação remota](../tutorials/use-python-revoscalepy-to-create-model.md)