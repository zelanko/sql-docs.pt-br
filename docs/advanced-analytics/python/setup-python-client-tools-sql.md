---
title: Configurar um cliente de Python para uso com o SQL Server Machine Learning | Microsoft Docs
description: Configure um ambiente local do Python para conexões remotas com serviços do SQL Server Machine Learning com o Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 326676d1be684b90784351de316590ebdb1ff29f
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50051148"
---
# <a name="set-up-a-python-client-for-use-with-sql-server-machine-learning"></a>Configurar um cliente de Python para uso com o SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integração do Python está disponível começando no SQL Server 2017 ou posterior, quando você inclui a opção de Python em uma instalação de serviços do Machine Learning (no banco de dados). Para obter mais informações, consulte [instalar o SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md).

Neste artigo, saiba como configurar uma estação de trabalho de desenvolvimento do cliente para que você pode se conectar a um SQL Server remoto habilitado para integração do Python e aprendizado de máquina. No final, você terá as mesmas bibliotecas de Python, como aqueles no SQL Server além da habilidade para enviar cálculos de uma sessão local para uma sessão remota no SQL Server.

> [!Tip]
> Para uma demonstração em vídeo, consulte [executar R e Python remotamente no SQL Server de blocos de anotações do Jupyter](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/).

> [!Note]
> Uma alternativa para instalar apenas as bibliotecas de cliente está usando um servidor autônomo. Servidor como um cliente avançado usando um autônomo é uma opção que alguns clientes preferem mais trabalho do cenário de ponta a ponta. Se você tiver um [servidor autônomo](../install/sql-machine-learning-standalone-windows-install.md) como fornecido na instalação do SQL Server, você tem um servidor de Python que é completamente separado de uma instância do mecanismo de banco de dados do SQL Server. Um servidor standalon inclui a distribuição de base de código-fonte aberto do Anaconda mais as bibliotecas específicas da Microsoft. Você pode encontrar o executável do Python neste local: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`. Como validação de sua instalação do cliente avançado, abra uma [notebook Jupyter](#python-tools) para executar comandos que usam o Python.exe no servidor.

## <a name="1---install-python-packages"></a>1 – instalar pacotes Python

Estações de trabalho locais devem ter as mesmas versões de pacote do Python como aqueles no SQL Server, incluindo a distribuição de base e pacotes específicos da Microsoft [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e [microsftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package). O [gerenciamento de modelos de azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) pacote também é instalado, mas ele se aplica a tarefas de operacionalização associadas a um contexto de Machine Learning Server autônomo (não da instância). Para uma análise no banco de dados em uma instância do SQL Server, a operacionalização é por meio de procedimentos armazenados.

1. Baixe o script de instalação para instalar o Anaconda 4.2.0 com Python 3.5.2 e três listados anteriormente pacotes da Microsoft.

  + [https://aka.ms/mls-py](https://aka.ms/mls-py) Se o SQL Server 2017 não está associado (caso comum). Escolha esse script se você não tiver certeza.

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) Se a instância remota do SQL Server estiver [associado ao Machine Learning Server 9.3](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

2. Abra uma janela do PowerShell com permissões de administrador com privilégios elevados (clique com botão direito **executar como administrador**).

3. Vá para a pasta na qual você baixou o instalador e execute o script. Adicionar o `-InstallFolder` argumento de linha de comando para especificar um local de pasta para as bibliotecas. Por exemplo: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

Se você omitir a pasta de instalação, o padrão é C:\Program Files\Microsoft\PyForMLS.

Instalação leva algum tempo para concluir. Você pode monitorar o progresso na janela do PowerShell. Quando a instalação for concluída, você tem um conjunto completo de pacotes. 

> [!Tip] 
> É recomendável o [FAQ de Python para Windows](https://docs.python.org/3/faq/windows.html) para obter informações sobre como executar programas de Python no Windows purppose geral.

## <a name="2---locate-executables"></a>2 – localizar executáveis

Ainda no PowerShell, navegue até a pasta de instalação para confirmar o local de outros pacotes, scripts e o Python.exe. 

1. Insira `cd \` ir para a unidade raiz e, em seguida, insira o caminho especificado para `-InstallFolder` na etapa anterior. Se você omitir esse parâmetro durante a instalação, o padrão é `cd C:\Program Files\Microsoft\PyForMLS`.

2. Insira `dir *.exe` para listar os arquivos executáveis. Você deve ver **python.exe**, **pythonw.exe**, e **anaconda.exe desinstalar**.

  ![Lista de arquivos executáveis do Python](media/powershell-python-exe.png)
   
Em sistemas de ter várias versões do Python, lembre-se de usar este Python.exe específico se você deseja carregar **revoscalepy** e outros pacotes da Microsoft.

> [!Note] 
> O script de instalação não modifica a variável de ambiente PATH em seu computador, o que significa que os módulos que você acabou de instalar e um novo interpretador de python não estão automaticamente disponíveis para outras ferramentas que você pode ter. Para obter ajuda sobre como vincular o interpretador do Python e bibliotecas para ferramentas, consulte [instalar um IDE](#install-ide).

<a name="python-tool"></a>

## <a name="3---open-jupyter-notebooks"></a>3 - abra Jupyter Notebooks

Anaconda inclui blocos de anotações do Jupyter. Como uma próxima etapa, crie um bloco de anotações e execute um código Python que contém as bibliotecas que você acabou de instalar.

1. No prompt do Powershell, navegue até a pasta de scripts para abrir o Jupyter Notebooks:

   ```powershell
   .\Scripts\jupyter-notebook
   ```

  Um bloco de anotações deve abrir no navegador padrão no `http://localhost:8889/tree`.

2. Clique em **New** e, em seguida, clique em **Python 3**.

  ![anotações do jupyter com o Python 3 nova seleção](media/jupyter-notebook-new-p3.png)

3. Insira `import revoscalepy` e execute o comando para carregar uma das bibliotecas específicas da Microsoft.

4. Insira uma série mais complexa de instruções. Este exemplo gera estatísticas de resumo usando [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) sobre um conjunto de dados local. Outras funções de obtém o local dos dados de exemplo e criar um objeto de fonte de dados para um arquivo. xdf local.

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

Captura de tela a seguir mostra a entrada e uma parte da saída, resumida para fins de brevidade.

  ![bloco de anotações do jupyter mostrando a saída e revoscalepy entradas](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4 – obter permissões do SQL

Para se conectar a uma instância do SQL Server para executar scripts e carregar dados, você deve ter um logon válido no servidor de banco de dados. Você pode usar um logon SQL ou a autenticação integrada do Windows. Em geral, é recomendável que você usa a autenticação integrada do Windows, mas usando o logon do SQL é mais simples para alguns cenários, especialmente quando o script contém cadeias de caracteres de conexão para dados externos.

No mínimo, a conta usada para executar o código deve ter permissão para ler os bancos de dados você está trabalhando, além de permissão especial executar qualquer SCRIPT externo. A maioria dos desenvolvedores também exigem permissões para criar procedimentos armazenados e para gravar dados em tabelas que contêm dados de treinamento ou pontuação de dados. 

Peça ao administrador de banco de dados para configurar as seguintes permissões para a conta, no banco de dados em que você usar o Python:

+ **EXECUTE ANY EXTERNAL SCRIPT** para executar o Python no servidor.
+ **db_datareader** privilégios para executar as consultas usadas para treinar o modelo.
+ **db_datawriter** para gravar dados de treinamento ou dados de pontuação.
+ **db_owner** para criar objetos, como procedimentos armazenados, tabelas, funções. 
  Você também precisa **db_owner** criar bancos de dados de exemplo e teste. 

Se seu código exigir pacotes que não são instalados por padrão com o SQL Server, organize-se com o administrador de banco de dados para ter os pacotes instalados com a instância. SQL Server é um ambiente seguro e há restrições sobre onde os pacotes podem ser instalados. Instalação de ad hoc de pacotes como parte do seu código não é recomendável, mesmo se você tiver direitos. Além disso, sempre considere as implicações de segurança antes de instalar novos pacotes na biblioteca do servidor.

## <a name="5---test-remote-connection"></a>5 - testar a conexão remota

Antes de tentar esta próxima etapa, verifique se você tem permissões na instância do SQL Server e uma cadeia de conexão para o [banco de dados de exemplo de íris](../tutorials/demo-data-iris-in-sql.md). Se o banco de dados não existe e você tem permissões suficientes, você poderá [criar um banco de dados usando estas instruções embutidas](#create-iris-remotely).

Substitua a cadeia de conexão com os valores válidos. O código de exemplo usa `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` , mas seu código deve especificar um servidor remoto, possivelmente com um nome de instância.

### <a name="define-a-function"></a>Definir uma função

O código a seguir define uma função que você enviará para o SQL Server em uma etapa posterior. Quando executado, ele usa dados e bibliotecas (revoscalepy, pandas, matplotlib) no servidor remoto para criar gráficos de dispersão do conjunto de dados íris. Ele retorna o fluxo de bytes da. png para blocos de anotações do Jupyter para renderizar no navegador.

```python
def send_this_func_to_sql():
    from revoscalepy import RxSqlServerData, rx_import
    from pandas.tools.plotting import scatter_matrix
    import matplotlib.pyplot as plt
    import io
    
    # remember the scope of the variables in this func are within our SQL Server Python Runtime
    connection_string = "Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"
    
    # specify a query and load into pandas dataframe df
    sql_query = RxSqlServerData(connection_string=connection_string, sql_query = "select * from iris_data")
    df = rx_import(sql_query)
    
    scatter_matrix(df)
    
    # return bytestream of image created by scatter_matrix
    buf = io.BytesIO()
    plt.savefig(buf, format="png")
    buf.seek(0)
    
    return buf.getvalue()
```

### <a name="send-the-function-to-sql-server"></a>A função Send para o SQL Server

Neste exemplo, criar o contexto de computação remota e, em seguida, enviar a execução da função para o SQL Server com [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec). O **rx_exec** função é útil porque ele aceita um contexto de computação como um argumento. Qualquer função que você deseja executar remotamente deve ter um argumento de contexto de computação. Algumas funções, como [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) dá suporte a esse argumento diretamente. Para operações que não, você pode usar **rx_exec** para entregar seu código em um contexto de computação remota.

Neste exemplo, não há dados brutos tinham que ser transferidas do SQL Server para o bloco de anotações do Jupyter. Todos os cálculos ocorrem no banco de dados íris e apenas o arquivo de imagem é retornado ao cliente.

```python
from IPython import display
import matplotlib.pyplot as plt 
from revoscalepy import RxInSqlServer, rx_exec

# create a remote compute context with connection to SQL Server
sql_compute_context = RxInSqlServer(connection_string=connection_string.format(new_db_name))

# use rx_exec to send the function execution to SQL Server
image = rx_exec(send_this_func_to_sql, compute_context=sql_compute_context)[0]

# only an image was returned to my jupyter client. All data remained secure and was manipulated in my db.
display.Image(data=image)
```

Captura de tela a seguir mostra a saída de plotagem de dispersão e de entrada.

  ![bloco de anotações do jupyter mostrando a saída de gráficos de dispersão](media/jupyter-notebook-scatterplot.png)

## <a name="6---link-ide-to-pythonexe"></a>6 - link de IDE para python.exe

Se você simplesmente estiver depurando scripts da linha de comando, você pode obter com as ferramentas padrão do Python. No entanto, se você estiver desenvolvendo novas soluções, você pode exigir um IDE do Python completo. Opções populares são:

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/) com Python
+ [Ferramentas de IA para Visual Studio](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Python no Visual Studio Code](https://code.visualstudio.com/docs/languages/python)
+ Ferramentas de terceiros populares, como PyCharm, Spyder e Eclipse

É recomendável o Visual Studio porque ele dá suporte a projetos de banco de dados, bem como projetos de aprendizado de máquina. Para obter ajuda sobre como configurar um ambiente de Python, consulte [Gerenciando ambientes do Python no Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio).

Porque com frequência, os desenvolvedores trabalham com várias versões do Python, a instalação não adiciona Python ao seu caminho. Para usar o executável do Python e bibliotecas instaladas pela instalação, vincular seu IDE para **Python.exe** no caminho que também fornece **revoscalepy** e **microsoftml**. 

Para um projeto do Python no Visual Studio, seu ambiente personalizado especifica valores a seguir, supondo que uma instalação padrão.

| Definição de configuração | value |
|-----------------------|-------|
| **Caminho do prefixo** | C:\Program Files\Microsoft\PyForMLS |
| **Caminho do interpretador** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **Interpretador de janela** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

<a name="create-iris-remotely"></a>

## <a name="optional-create-the-iris-database-remotely"></a>Opcional: Crie a banco de dados íris remotamente

Se você tiver permissões para criar um banco de dados no servidor remoto, você pode executar o código a seguir para criar o banco de dados de demonstração de íris usado para os exemplos neste artigo.

### <a name="1---create-the-irissql-database"></a>1 - criar o banco de dados irissql

```Python
import pyodbc

# creating a new db to load Iris sample in
new_db_name = "irissql"
connection_string = "Driver=SQL Server;Server=localhost;Database={0};Trusted_Connection=Yes;" 
                        # you can also swap Trusted_Connection for UID={your username};PWD={your password}
cnxn = pyodbc.connect(connection_string.format("master"), autocommit=True)
cnxn.cursor().execute("IF EXISTS(SELECT * FROM sys.databases WHERE [name] = '{0}') DROP DATABASE {0}".format(new_db_name))
cnxn.cursor().execute("CREATE DATABASE " + new_db_name)
cnxn.close()

print("Database created")
```

### <a name="2---import-iris-sample-from-sklearn"></a>2 - exemplo de íris importação de SkLearn

```Python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-recoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3 - usar RecoscalePy APIs para criar uma tabela e carregar os dados de íris

```Python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

<a name="install-ide"></a>

## <a name="next-steps"></a>Próximas etapas

Agora que você tem uma conexão de trabalho para o SQL Server e ferramentas, percorra um tutorial para obter uma olhada nas funções revoscalepy e alternar contextos de computação.

> [!div class="nextstepaction"]
> [Criar um modelo usando revoscalepy e um contexto de computação remota](../tutorials/use-python-revoscalepy-to-create-model.md)