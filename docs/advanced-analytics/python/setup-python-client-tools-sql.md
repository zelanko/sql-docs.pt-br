---
title: Configurar um cliente de ciência de dados para o desenvolvimento de Python - aprendizagem de máquina do SQL Server
description: Configure um ambiente local do Python (bloco de notas Jupyter ou PyCharm) para conexões remotas com serviços do SQL Server Machine Learning com o Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/09/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c0ca592d98f9bb69586c537006fd14d4230b661b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642805"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>Configurar um cliente de ciência de dados para o desenvolvimento de Python em serviços do SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Integração do Python está disponível começando no SQL Server 2017 ou posterior, quando você inclui a opção de Python em um [instalação de serviços do Machine Learning (no banco de dados)](../install/sql-machine-learning-services-windows-install.md). 

Para desenvolver e implantar soluções de Python para o SQL Server, instale da Microsoft [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) e outras bibliotecas de Python sua estação de trabalho de desenvolvimento. A biblioteca revoscalepy, que também está na instância remota do SQL Server, coordena solicitações de computação entre os dois sistemas. 

Neste artigo, saiba como configurar uma estação de trabalho de desenvolvimento do Python para que você pode interagir com um SQL Server remoto habilitado para integração do Python e aprendizado de máquina. Depois de concluir as etapas neste artigo, você terá as mesmas bibliotecas de Python, como aqueles no SQL Server. Você também saberá como enviar por push os cálculos de uma sessão local do Python para uma sessão remota do Python no SQL Server.

![Componentes de cliente-servidor](media/sqlmls-python-client-revo.png "sessões locais e remotas do Python e bibliotecas")

Para validar a instalação, você pode usar o Jupyter Notebooks interno conforme descrito neste artigo, ou [vincular as bibliotecas](#install-ide) PyCharm ou qualquer outro IDE que você normalmente usa.

> [!Tip]
> Para uma demonstração em vídeo deste exercício, consulte [executar R e Python remotamente no SQL Server a partir de blocos de anotações do Jupyter](https://youtu.be/D5erljpJDjE).

> [!Note]
> Uma alternativa para a instalação da biblioteca de cliente está usando um [servidor autônomo](../install/sql-machine-learning-standalone-windows-install.md) como um cliente avançado, que alguns clientes preferem para o trabalho mais profundo do cenário. Um servidor autônomo é totalmente separado do SQL Server, mas porque ele tem as mesmas bibliotecas de Python, você pode usá-lo como um cliente para análise do SQL Server no banco de dados. Você também pode usá-lo para o trabalho não relacionados ao SQL, incluindo a capacidade de importar e modelar dados de outras plataformas de dados. Se você instalar um servidor autônomo, você pode encontrar o executável do Python neste local: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`. Para validar sua instalação [abrir um notebook Jupyter](#python-tools) para executar comandos que usam o Python.exe nesse local.

## <a name="commonly-used-tools"></a>Ferramentas usadas comumente

Se você for um desenvolvedor de Python iniciante em SQL ou desenvolvedor familiarizado com o Python e análise no banco de dados do SQL, será necessário uma ferramenta de desenvolvimento do Python e um editor de consultas T-SQL, como [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para exercer todos os recursos de análise no banco de dados.

Para o desenvolvimento do Python, você pode usar blocos de anotações do Jupyter, que vem incluído na distribuição do Anaconda instalada pelo SQL Server. Este artigo explica como iniciar o Jupyter Notebooks para que você possa executar código Python local e remotamente no SQL Server.

O SSMS é um download separado, útil para criar e executar procedimentos armazenados no SQL Server, incluindo aqueles que contém o código do Python. Praticamente qualquer código do Python que você escreve em blocos de anotações do Jupyter pode ser inserido em um procedimento armazenado. Você pode percorrer os outros guias de início rápido para saber mais sobre [SSMS e Python incorporado](../tutorials/quickstart-python-verify.md).

## <a name="1---install-python-packages"></a>1 – instalar pacotes Python

Estações de trabalho locais devem ter as mesmas versões de pacote do Python como aqueles no SQL Server, incluindo o Anaconda 4.2.0 base com a distribuição do Python 3.5.2 e pacotes específicos da Microsoft.

Um script de instalação adiciona três bibliotecas específicas da Microsoft para o cliente do Python. O script instala [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), usado para definir objetos de fonte de dados e o contexto de computação. Ele instala [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) fornecendo os algoritmos de aprendizado de máquina. O [azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) pacote também é instalado, mas ele se aplica a tarefas de operacionalização associadas a um contexto de Machine Learning Server autônomo (não da instância) e pode ser de uso limitado para análise no banco de dados.

1. Baixe um script de instalação.

  + [https://aka.ms/mls-py](https://aka.ms/mls-py) instala a versão 9.2.1 dos pacotes Python de Microsoft. Esta versão corresponde a uma instância do SQL Server 2017 padrão. 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) instala a versão 9.3 dos pacotes Python de Microsoft. Esta versão é uma opção melhor se for a instância remota do SQL Server 2017 [associado ao Machine Learning Server 9.3](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md).

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

Ainda no PowerShell, liste o conteúdo da pasta de instalação para confirmar que Python.exe, scripts e outros pacotes são instalados. 

1. Insira `cd \` ir para a unidade raiz e, em seguida, insira o caminho especificado para `-InstallFolder` na etapa anterior. Se você omitir esse parâmetro durante a instalação, o padrão é `cd C:\Program Files\Microsoft\PyForMLS`.

2. Insira `dir *.exe` para listar os arquivos executáveis. Você deve ver **python.exe**, **pythonw.exe**, e **anaconda.exe desinstalar**.

  ![Lista de arquivos executáveis do Python](media/powershell-python-exe.png)
   
Em sistemas de ter várias versões do Python, lembre-se de usar este Python.exe específico se você deseja carregar **revoscalepy** e outros pacotes da Microsoft.

> [!Note] 
> O script de instalação não modifica a variável de ambiente PATH em seu computador, o que significa que os módulos que você acabou de instalar e um novo interpretador de python não estão automaticamente disponíveis para outras ferramentas que você pode ter. Para obter ajuda sobre como vincular o interpretador do Python e bibliotecas para ferramentas, consulte [instalar um IDE](#install-ide).

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3 - abra Jupyter Notebooks

Anaconda inclui blocos de anotações do Jupyter. Como uma próxima etapa, crie um bloco de anotações e execute um código Python que contém as bibliotecas que você acabou de instalar.

1. No prompt do Powershell, no diretório C:\Program Files\Microsoft\PyForMLS, abra blocos de anotações do Jupyter na pasta Scripts:

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  Um bloco de anotações deve abrir no navegador padrão no `https://localhost:8889/tree`.

  Outra maneira de iniciar é clicar duas vezes **jupyter notebook.exe**. 

2. Clique em **New** e, em seguida, clique em **Python 3**.

  ![anotações do jupyter com o Python 3 nova seleção](media/jupyter-notebook-new-p3.png)

3. Insira `import revoscalepy` e execute o comando para carregar uma das bibliotecas específicas da Microsoft.

4. Digite e execute `print(revoscalepy.__version__)` para retornar as informações de versão. Você deve ver 9.2.1 ou 9.3.0. Você pode usar qualquer uma dessas versões com [revoscalepy no servidor](../r/determine-which-packages-are-installed-on-sql-server.md#get-package-vers). 

4. Insira uma série mais complexa de instruções. Este exemplo gera estatísticas de resumo usando [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) sobre um conjunto de dados local. Outras funções de obtém o local dos dados de exemplo e criar um objeto de fonte de dados para um arquivo. xdf local.

  ```python
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

Peça ao administrador de banco de dados para [configure as seguintes permissões para sua conta](../security/user-permission.md), no banco de dados em que você usar o Python:

+ **EXECUTE ANY EXTERNAL SCRIPT** para executar o Python no servidor.
+ **db_datareader** privilégios para executar as consultas usadas para treinar o modelo.
+ **db_datawriter** para gravar dados de treinamento ou dados de pontuação.
+ **db_owner** para criar objetos, como procedimentos armazenados, tabelas, funções. 
  Você também precisa **db_owner** criar bancos de dados de exemplo e teste. 

Se seu código exigir pacotes que não são instalados por padrão com o SQL Server, organize-se com o administrador de banco de dados para ter os pacotes instalados com a instância. SQL Server é um ambiente seguro e há restrições sobre onde os pacotes podem ser instalados. Instalação de ad hoc de pacotes como parte do seu código não é recomendável, mesmo se você tiver direitos. Além disso, sempre considere as implicações de segurança antes de instalar novos pacotes na biblioteca do servidor.


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5 - Criar dados de teste

Se você tiver permissões para criar um banco de dados no servidor remoto, você pode executar o código a seguir para criar o banco de dados de demonstração de íris usado para as etapas restantes neste artigo.

### <a name="1---create-the-irissql-database-remotely"></a>1 - criar o banco de dados irissql remotamente

```python
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

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3 - usar Revoscalepy APIs para criar uma tabela e carregar os dados de íris

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6 - teste de conexão remota

Antes de tentar esta próxima etapa, verifique se você tem permissões na instância do SQL Server e uma cadeia de conexão para o [banco de dados de exemplo de íris](../tutorials/demo-data-iris-in-sql.md). Se o banco de dados não existe e você tem permissões suficientes, você poderá [criar um banco de dados usando estas instruções embutidas](#create-iris-remotely).

Substitua a cadeia de conexão com os valores válidos. O código de exemplo usa `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` , mas seu código deve especificar um servidor remoto, possivelmente com um nome de instância e uma opção de credencial que é mapeado para um logon de usuário de banco de dados.

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


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7 - Iniciar Python tools

Porque com frequência, os desenvolvedores trabalham com várias versões do Python, a instalação não adiciona Python ao seu caminho. Para usar o executável do Python e bibliotecas instaladas pela instalação, vincular seu IDE para **Python.exe** no caminho que também fornece **revoscalepy** e **microsoftml**. 

### <a name="command-line"></a>Linha de Comando

Quando você executa **Python.exe** de C:\Program Files\Microsoft\PyForMLS (ou qualquer local em que você especificou para a instalação de biblioteca de cliente do Python), você tem acesso para a distribuição Anaconda completa plus Microsoft Python módulos, **revoscalepy** e **microsoftml**.

1. Vá para C:\Program Files\Microsoft\PyForMLS e clique duas vezes em **Python.exe**.
2. Abrir a Ajuda interativa: `help()`
3. Digite o nome de um módulo no prompt de Ajuda: `help> revoscalepy`. Ajuda retorna o nome, o conteúdo do pacote, a versão e o local do arquivo.
4. Retornar informações de versão e o pacote com o **Ajuda >** prompt: `revoscalepy`. Pressione Enter algumas vezes para sair da Ajuda.
5. Importe um módulo: `import revoscalepy`


### <a name="jupyter-notebooks"></a>Blocos de anotações do Jupyter

Este artigo usa o Jupyter Notebooks interno para demonstrar as chamadas de função **revoscalepy**. Se você estiver familiarizado com essa ferramenta, a captura de tela a seguir ilustra como as peças se encaixam e porque tudo isso "simplesmente funciona". 

A pasta pai C:\Program Files\Microsoft\PyForMLS contém Anaconda mais os pacotes Microsoft. Blocos de anotações do Jupyter está incluído no Anaconda, sob a pasta de Scripts, e os executáveis de Python são registrados automaticamente com os Notebooks Jupyter. Pacotes encontrados nos pacotes do site podem ser importados para um bloco de anotações, incluindo os três pacotes Microsoft usados para o aprendizado de máquina e ciência de dados.

  ![Bibliotecas e executáveis](media/jupyter-notebook-python-registration.png)

Se você estiver usando outro IDE, você precisará vincular as bibliotecas de executáveis e a função de Python à sua ferramenta. As seções a seguir fornecem instruções para as ferramentas comumente usadas.

### <a name="visual-studio"></a>Visual Studio

Se você tiver [Python no Visual Studio](https://code.visualstudio.com/docs/languages/python), use as seguintes opções de configuração para criar um ambiente de Python que inclui os pacotes do Python de Microsoft.

| Definição de configuração | value |
|-----------------------|-------|
| **Caminho do prefixo** | C:\Program Files\Microsoft\PyForMLS |
| **Caminho do interpretador** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **Interpretador de janela** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

Para obter ajuda sobre como configurar um ambiente de Python, consulte [Gerenciando ambientes do Python no Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio).

### <a name="pycharm"></a>PyCharm

No PyCharm, defina o interpretador de Python executável instalado pelo Machine Learning Server.

1. Em um novo projeto, em configurações, clique em **Adicionar Local**.

2. Enter `C:\Program Files\Microsoft\PyForMLS\`.

Agora você pode importar **revoscalepy**, **microsoftml**, ou **azureml** módulos. Você também pode escolher **ferramentas** > **Console Python** para abrir uma janela interativa.

## <a name="next-steps"></a>Próximas etapas

Agora que você tem uma conexão de trabalho para o SQL Server e ferramentas, amplie suas habilidades com a execução por meio de guias de início rápido do Python usando [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

> [!div class="nextstepaction"]
> [Guia de início rápido: Verifique se que existe do Python no SQL Server](../tutorials/quickstart-python-verify.md)