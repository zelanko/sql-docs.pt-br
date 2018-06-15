---
title: Configurar as ferramentas de cliente do Python para uso com o aprendizado de máquina do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ace5ea536c020d2713f1aa07bd1b26c41065a587
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203798"
---
# <a name="set-up-python-client-tools-for-use-with-sql-server-machine-learning"></a>Configurar o Python ferramentas de cliente para uso com o aprendizado de máquina do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve como configurar um ambiente de Python em um computador com Windows para oferecer suporte a código Python em execução no SQL Server. Isso inclui os seguintes cenários:

+ Testar e desenvolver soluções em uma estação de trabalho remota do Python e enviar o código para o SQL Server para execução em um contexto de computação do SQL Server. 

    Em geral, você deseja instalar um ambiente de desenvolvimento do Python completo. 
    
    Seu ambiente de Python local deve ser compatível com o ambiente do Python na instância do SQL Server, e você deve instalar as bibliotecas que oferecem suporte a contextos de computação remota.

+ Desenvolver e testar seu código usando as ferramentas Python dedicadas e, em seguida, migrar o código para o SQL Server para ser executado em um procedimento armazenado.

    Você pode usar um IDE de Python completo para o desenvolvimento de servidor. No entanto, antes de implantar seu código, você testá-lo em um ambiente que emula o ambiente do SQL Server.

+ Executar código Python principalmente em um procedimento armazenado no SQL Server e não desenvolver código Python. Você espera que o código foi testado e depurado antes de você colocá-los em um procedimento armazenado. No entanto, ocasionalmente, você precisará executar o código fora do SQL Server, para determinar a origem de um problema.

    Você não deseja instalar as ferramentas Python no servidor e usa apenas as ferramentas padrão instaladas com a distribuição. Você pode decidir configurar um ambiente do Python que usa a biblioteca de instância, para verificar se o código funciona fora de um procedimento armazenado.

## <a name="requirements"></a>Requisitos

Independentemente de quais ferramentas você pode usar para desenvolver o código Python, os seguintes requisitos se aplicam sempre que você executar o código Python no SQL Server ou usar dados do SQL Server:

+ Para usar o Python, SQL Server 2017 ou posterior é necessário. Você deve instalar também o recurso que oferece suporte a serviços de aprendizado de máquina (no banco de dados) e habilitar explicitamente o recurso. Para obter mais informações, consulte [configurar o SQL Server 2017](../r/set-up-sql-server-r-services-in-database.md).

    Se você instalou uma versão mais recente do SQL Server 2017, você poderá receber erros se você tentar executar os comandos de Python desse utilitário de linha de comando. É recomendável que você [atualização para a versão mais recente](#bkmk_update) se possível. 

+ Certifique-se de que a conta usada para executar o código tem permissão para se conectar ao banco de dados e executar o código Python. A permissão especial `EXECUTE ANY EXTERNAL SCRIPT` é necessária para todas as contas que usam o script R ou Python. 

+ Certifique-se de que a conta tem quaisquer permissões de banco de dados que podem ser necessárias para ler os dados ou criar novos objetos. 

+ Se seu código requer pacotes que não são instalados por padrão com o SQL Server, organize com o administrador de banco de dados para que os pacotes instalados no ambiente de Python é usado pela instância. SQL Server é um ambiente seguro e há restrições sobre onde os pacotes podem ser instalados. 

    Instalação ad hoc de pacotes como parte do seu código não é recomendável, mesmo se você tiver direitos. Além disso, sempre considere as implicações de segurança antes de instalar novos pacotes na biblioteca do servidor.

> [!NOTE]
> Se você pretende usar o Python com servidor de aprendizado de máquina, que oferece suporte para contextos de computação adicionais, como o Linux ou Spark clusters, consulte estes artigos:
> 
> + [Como instalar o interpretador e pacotes do Python personalizados localmente no Windows](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)
> + [Ferramentas do Python de link e IDEs ao interpretador do Python instalado com o servidor de aprendizado de máquina](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)

## <a name="default-tools-included-with-standard-install"></a>Ferramentas padrão incluídas com a instalação padrão

Uma instalação padrão do SQL Server 2017 com serviços de aprendizado de máquina (no banco de dados) e Python adiciona as seguintes ferramentas Python padrão e recursos:

+ Dados de exemplo do Python
+ Distribuição anaconda 4.2 
+ Pythonw.exe e Python executáveis python.exe

Por padrão, a instalação é nesta pasta: `~\Program Files\Microsoft SQL Server\<instance_name>\PYTHON_SERVICES`. 

## <a name="open-python-from-the-command-line"></a>Abra o Python da linha de comando 

Para usar o tempo de execução do Python que é instalado com a instância, você pode iniciar o Python executável do caminho de instalação. Instruções básicas estão disponíveis no [Python para Windows perguntas frequentes sobre](https://docs.python.org/3/faq/windows.html).

> [!IMPORTANT]
> Em geral, para evitar contenção de recursos, recomendamos que você **não** executar Python da biblioteca de instância no servidor, se você achar que é possível que a instância do SQL Server está em execução código Python. No entanto, usando as ferramentas na biblioteca de instância pode ser útil se você está tentando depurar um problema que ocorre apenas durante a execução no SQL Server e para exibir mensagens de erro mais detalhadas, ou certifique-se de que todos os pacotes necessários estão instalados.

1. Navegue até a pasta em que a biblioteca de instância é instalada. Por exemplo, em uma instalação padrão, a pasta é `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`.

2. Localize Python.exe. 

3. Clique com botão direito e selecione **executar como administrador** para abrir uma janela de linha de comando interativa.

## <a name="bkmk_update"></a> Atualizar os componentes do Python

Você pode atualizar os componentes do Python baixando e instalando uma versão mais recente, usando o script descrito aqui: [cliente instalar o Python no Windows](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter#install-on-windows)
> 
> O instalador baixado pelo script é [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054&clcid=1033). Se você precisar de uma versão diferente, consulte [instalação de componentes de aprendizado de máquina sem acesso à internet](http://bing.com)

## <a name="set-up-a-python-development-environment"></a>Configurar um ambiente de desenvolvimento do Python

Se você simplesmente é depuração de scripts de linha de comando, você pode obter com as ferramentas Python padrão instaladas com os serviços de aprendizado de máquina, ou usar um editor de texto. No entanto, se você estiver desenvolvendo novas soluções ou trabalhando em um cliente remoto, recomendamos o uso de um IDE de Python completo. Opções comuns são:

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/) com Python
+ [Ferramentas do AI para Visual Studio](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Python no código do Visual Studio](https://code.visualstudio.com/docs/languages/python)
+ Ferramentas de terceiros populares, como PyCharm, Spyder e Eclipse

É recomendável o Visual Studio porque ele oferece suporte a projetos de banco de dados, bem como projetos de aprendizado de máquina. Para obter ajuda sobre como configurar um ambiente de Python, consulte [ambientes de gerenciamento de Python no Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

## <a name="install-revoscalepy"></a>Instalar revoscalepy

Mesmo se você instalou com êxito os serviços de aprendizado de máquina, você poderá receber um erro ao tentar carregar **revoscalepy** funções em uma linha de comando do Python. Estas etapas descrevem como você pode instalar uma atualização para habilitar o uso de **revoscalepy**.

1. Baixar o script de shell de instalação do https://aka.ms/mls93-py (ou usar https://aka.ms/mls-py para o 9.2. versão). O script instala Anaconda 4.2.0, que inclui o Python 3.5.2, juntamente com todos os pacotes listados anteriormente.

2. Abra uma nova janela do PowerShell com permissões elevadas (como administrador).

3. Abra a pasta na qual você baixou o instalador e execute o script:

```ps1
cd {{download-directory}}
.\Install-PyForMLS.ps1
```

Você também pode executar o `-InstallFolder` argumento de linha de comando e especifique o novo caminho como parte do comando. Por exemplo: 

```ps1
.\Install-PyForMLS.ps1 -InstallFolder "<installation_path>")
```

Se você receber um erro, talvez seja necessário suspender as políticas de execução de um arquivo específico, a duração da sessão, da seguinte maneira: 

```ps1
powershell -ExecutionPolicy Bypass -File "C:\<installation_path>\Install-PyForMLS.ps1"
```

Você também pode suspender as políticas de execução para a duração da sessão. Com esta instrução, a política de execução é definida como `Unrestricted` para a duração da sessão e não alterar a configuração ou a alteração de gravação no disco.

```ps1
Set-ExecutionPolicy Bypass -Scope Process
```

## <a name="verify-that-python-and-revoscalepy-are-working"></a>Verificar se o Python e revoscalepy estão funcionando

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

O caminho de dados de exemplo é impresso para que você possa determinar qual instância do Python que está sendo chamada.

### <a name="verify-that-python-can-be-called-from-sql-server"></a>Verifique se que o Python pode ser chamado do SQL Server

Para verificar se o Python está se comunicando com o SQL Server, abra o SQL Server Management Studio. (Você pode usar outra ferramenta semelhante, como [Studio de operações SQL](https://docs.microsoft.com/sql/sql-operations-studio/what-is).) Abra uma nova **consulta** janela e executar qualquer Python simples de comando no contexto de um procedimento armazenado:

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'print(3+4)'
```

Pode levar algum tempo para iniciar o tempo de execução do Python pela primeira vez, mas se não houver nenhum erro, você sabe que o Launchpad do SQL Server está funcionando e Python pode ser iniciado a partir do SQL Server.

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

Como rx_summary retorna um objeto do tipo `class revoscalepy.functions.RxSummary.RxSummaryResults`, que contém vários elementos, para manipular os resultados no SQL Server, você pode extrair apenas o quadro de dados em um formato tabular.

### <a name="verify-python-execution-in-sql-server-as-remote-compute-context"></a>Verifique se a execução do Python no SQL Server como o contexto de computação remota

Se você tiver instalado o **revoscalepy** em seu ambiente de desenvolvimento do Python local, você deve ser capaz de se conectar a uma instância do SQL Server 2017 onde Python foi habilitado e executar um exemplo de código semelhante usando o servidor como o de computação contexto. 


```Python
import os
from revoscalepy import rx_summary, RxOptions, RxXdfData, RxSqlServerData, RxInSqlServer

# define connection string and compute context
sql_conn_string="Driver=SQL Server;Server=;Database=TestDB;Trusted_Connection=True"
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

Neste exemplo, o objeto de resumo é retornado para o console, em vez de retornar dados tabulares bem formados para o SQL Server. 

Além disso, porque [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) foi chamado, os dados de exemplo são carregados na pasta exemplos no computador do SQL Server e não a partir de sua pasta de exemplos de local.
