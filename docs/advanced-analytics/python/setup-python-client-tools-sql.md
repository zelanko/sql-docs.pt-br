---
title: Configurar um cliente de ciência de dados para desenvolvimento em Python
description: Configure um ambiente local do Python (Jupyter Notebook ou PyCharm) para conexões remotas para SQL Server Serviços de Machine Learning com Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 399aab131a30560ac3305b0cac678cd9e0d18553
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344802"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>Configurar um cliente de ciência de dados para desenvolvimento em Python no SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A integração do Python está disponível a partir do SQL Server 2017 ou posterior quando você inclui a opção Python em uma [instalação do serviços de Machine Learning (no banco de dados)](../install/sql-machine-learning-services-windows-install.md). 

Para desenvolver e implantar soluções Python para SQL Server, instale o [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) da Microsoft e outras bibliotecas do Python em sua estação de trabalho de desenvolvimento. A biblioteca revoscalepy, que também está na instância de SQL Server remota, coordena as solicitações de computação entre ambos os sistemas. 

Neste artigo, saiba como configurar uma estação de trabalho de desenvolvimento do Python para que você possa interagir com um SQL Server remoto habilitado para aprendizado de máquina e integração do Python. Depois de concluir as etapas neste artigo, você terá as mesmas bibliotecas Python que aquelas em SQL Server. Você também saberá como enviar por push cálculos de uma sessão local do Python para uma sessão remota do Python em SQL Server.

![Componentes cliente-servidor](media/sqlmls-python-client-revo.png "Bibliotecas e sessões locais e remotas do Python")

Para validar a instalação, você pode usar os blocos de anotações internos do Jupyter, conforme descrito neste artigo, ou [vincular as bibliotecas](#install-ide) ao PyCharm ou a qualquer outro IDE que você normalmente usa.

> [!Tip]
> Para ver uma demonstração em vídeo desses exercícios, consulte [executar o R e o Python remotamente em SQL Server notebooks Jupyter](https://youtu.be/D5erljpJDjE).

> [!Note]
> Uma alternativa para a instalação da biblioteca de cliente é usar um [servidor autônomo](../install/sql-machine-learning-standalone-windows-install.md) como um cliente avançado, que alguns clientes preferem para um cenário mais profundo de trabalho. Um servidor autônomo é totalmente dissociado de SQL Server, mas como ele tem as mesmas bibliotecas Python, você pode usá-lo como um cliente para SQL Server análise no banco de dados. Você também pode usá-lo para trabalho não relacionado ao SQL, incluindo a capacidade de importar e modelar dados de outras plataformas de dados. Se você instalar um servidor autônomo, poderá encontrar o executável do Python neste local: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`. Para validar a instalação, [abra um notebook Jupyter](#python-tools) para executar comandos usando o Python. exe nesse local.

## <a name="commonly-used-tools"></a>Ferramentas usadas com frequência

Seja você um desenvolvedor de Python novo no SQL ou um desenvolvedor de SQL novo para Python e análise no banco de dados, precisará de uma ferramenta de desenvolvimento Python e de um editor de consultas T-SQL como o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) para exercitar todos os recursos do análise no banco de dados.

Para o desenvolvimento em Python, você pode usar notebooks Jupyter, que vêm agrupados na distribuição Anaconda instalada pelo SQL Server. Este artigo explica como iniciar o Jupyter notebooks para que você possa executar o código Python localmente e remotamente em SQL Server.

O SSMS é um download separado, útil para criar e executar procedimentos armazenados em SQL Server, incluindo aqueles que contêm código Python. Quase todos os códigos Python que você escreve nos notebooks Jupyter podem ser inseridos em um procedimento armazenado. Você pode percorrer outros guias de início rápido para saber mais sobre o [SSMS e o Python incorporado](../tutorials/quickstart-python-verify.md).

## <a name="1---install-python-packages"></a>1-instalar pacotes do Python

As estações de trabalho locais devem ter as mesmas versões de pacote Python que aquelas em SQL Server, incluindo a base Anaconda 4.2.0 com a distribuição 3.5.2 do Python e pacotes específicos da Microsoft.

Um script de instalação adiciona três bibliotecas específicas da Microsoft ao cliente Python. O script instala o [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), usado para definir objetos de fonte de dados e o contexto de computação. Ele instala o [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) fornecendo algoritmos de aprendizado de máquina. O pacote do [azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) também é instalado, mas se aplica a tarefas de operacionalização associadas a um contexto de Machine Learning Server autônomo (não de instância) e pode ser de uso limitado para análise no banco de dados.

1. Baixar um script de instalação.

  + [https://aka.ms/mls-py](https://aka.ms/mls-py)instala a versão 9.2.1 dos pacotes do Microsoft Python. Esta versão corresponde a uma instância de SQL Server 2017 padrão. 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py)instala a versão 9,3 dos pacotes do Microsoft Python. Esta versão é uma opção melhor se a instância remota SQL Server 2017 estiver [associada a Machine Learning Server 9,3](../install/upgrade-r-and-python.md).

2. Abra uma janela do PowerShell com permissões de administrador elevadas (clique com o botão direito do mouse em **Executar como administrador**).

3. Vá para a pasta em que você baixou o instalador e execute o script. Adicione o `-InstallFolder` argumento de linha de comando para especificar um local de pasta para as bibliotecas. Por exemplo: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

Se você omitir a pasta de instalação, o padrão será C:\Program Files\Microsoft\PyForMLS.

A instalação leva algum tempo para ser concluída. Você pode monitorar o progresso na janela do PowerShell. Quando a instalação for concluída, você terá um conjunto completo de pacotes. 

> [!Tip] 
> Recomendamos as [perguntas frequentes sobre o Python para Windows](https://docs.python.org/3/faq/windows.html) para informações gerais de purppose sobre a execução de programas Python no Windows.

## <a name="2---locate-executables"></a>2-localizar executáveis

Ainda no PowerShell, liste o conteúdo da pasta de instalação para confirmar se o Python. exe, os scripts e outros pacotes estão instalados. 

1. Insira `cd \` para ir para a unidade raiz e, em seguida, insira o caminho especificado `-InstallFolder` para a etapa anterior. Se você omitir esse parâmetro durante a instalação, o `cd C:\Program Files\Microsoft\PyForMLS`padrão será.

2. Insira `dir *.exe` para listar os executáveis. Você deve ver **Python. exe**, **pythonw. exe**e **Uninstall-Anaconda. exe**.

  ![Lista de executáveis do Python](media/powershell-python-exe.png)
   
Em sistemas com várias versões do Python, lembre-se de usar esse Python. exe específico se você quiser carregar o **revoscalepy** e outros pacotes da Microsoft.

> [!Note] 
> O script de instalação não modifica a variável de ambiente PATH no seu computador, o que significa que o novo interpretador do Python e os módulos que você acabou de instalar não estão automaticamente disponíveis para outras ferramentas que você possa ter. Para obter ajuda sobre como vincular o intérprete do Python e bibliotecas a ferramentas, consulte [instalar um IDE](#install-ide).

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3-abrir blocos de anotações do Jupyter

O Anaconda inclui blocos de anotações do Jupyter. Como uma próxima etapa, crie um bloco de anotações e execute algum código Python contendo as bibliotecas que você acabou de instalar.

1. No prompt do PowerShell, ainda no diretório C:\Program Files\Microsoft\PyForMLS, abra blocos de anotações do Jupyter na pasta scripts:

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  Um bloco de anotações deve ser aberto no navegador `https://localhost:8889/tree`padrão em.

  Outra maneira de começar é clicar duas vezes em **jupyter-notebook. exe**. 

2. Clique em **novo** e em **Python 3**.

  ![bloco de anotações jupyter com a nova seleção do Python 3](media/jupyter-notebook-new-p3.png)

3. Insira `import revoscalepy` e execute o comando para carregar uma das bibliotecas específicas da Microsoft.

4. Insira e execute `print(revoscalepy.__version__)` para retornar as informações de versão. Você deve ver 9.2.1 ou 9.3.0. Você pode usar qualquer uma dessas versões com [revoscalepy no servidor](../package-management/installed-package-information.md). 

4. Insira uma série mais complexa de instruções. Este exemplo gera estatísticas de resumo usando [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) em um conjunto de dados local. Outras funções obtêm o local dos dados de exemplo e criam um objeto de fonte de dados para um arquivo. Xdf local.

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

A captura de tela a seguir mostra a entrada e uma parte da saída, cortada por brevidade.

  ![Notebook jupyter mostrando entradas e saídas do revoscalepy](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4-obter permissões do SQL

Para se conectar a uma instância do SQL Server para executar scripts e carregar dados, você deve ter um logon válido no servidor de banco de dados. Você pode usar um logon SQL ou a autenticação integrada do Windows. Geralmente, é recomendável usar a autenticação integrada do Windows, mas usar o logon do SQL é mais simples para alguns cenários, especialmente quando o script contém cadeias de conexão para dados externos.

No mínimo, a conta usada para executar o código deve ter permissão para ler os bancos de dados com os quais você está trabalhando, além da permissão especial executar qualquer SCRIPT externo. A maioria dos desenvolvedores também exige permissões para criar procedimentos armazenados e para gravar dados em tabelas que contêm dados de treinamento ou dados pontuados. 

Peça ao administrador do banco de dados para [configurar as seguintes permissões para sua conta](../security/user-permission.md), no banco de dados em que você usa o Python:

+ **Execute qualquer script externo** para executar o Python no servidor.
+ privilégios **db_datareader** para executar as consultas usadas para treinar o modelo.
+ **db_datawriter** para escrever dados de treinamento ou dados pontuados.
+ **db_owner** para criar objetos, como procedimentos armazenados, tabelas, funções. 
  Você também precisa do **db_owner** para criar bancos de dados de exemplo e de teste. 

Se o seu código exigir pacotes que não estão instalados por padrão com SQL Server, organize com o administrador de banco de dados para que os pacotes sejam instalados com a instância do. SQL Server é um ambiente seguro e há restrições sobre onde os pacotes podem ser instalados. A instalação ad hoc de pacotes como parte do seu código não é recomendada, mesmo que você tenha direitos. Além disso, sempre considere cuidadosamente as implicações de segurança antes de instalar novos pacotes na biblioteca do servidor.


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5-criar dados de teste

Se você tiver permissões para criar um banco de dados no servidor remoto, poderá executar o código a seguir para criar o banco de dados de demonstração íris usado para as etapas restantes neste artigo.

### <a name="1---create-the-irissql-database-remotely"></a>1-criar o banco de dados irissql remotamente

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

### <a name="2---import-iris-sample-from-sklearn"></a>2-importar exemplo de íris de SkLearn

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-usar APIs Revoscalepy para criar uma tabela e carregar os dados da íris

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6-testar conexão remota

Antes de tentar esta próxima etapa, verifique se você tem permissões na instância de SQL Server e uma cadeia de conexão para o [banco de dados de exemplo da íris](../tutorials/demo-data-iris-in-sql.md). Se o banco de dados não existir e você tiver permissões suficientes, você poderá [criar um banco de dados usando essas instruções embutidas](#create-iris-remotely).

Substitua a cadeia de conexão por valores válidos. O código de exemplo `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` usa, mas seu código deve especificar um servidor remoto, possivelmente com um nome de instância, e uma opção de credencial que mapeia para o logon de usuário do banco de dados.

### <a name="define-a-function"></a>Definir uma função

O código a seguir define uma função que você enviará para SQL Server em uma etapa posterior. Quando executado, ele usa dados e bibliotecas (revoscalepy, pandas, matplotlib) no servidor remoto para criar gráficos de dispersão do conjunto de dados íris. Ele retorna o bytes do. png de volta aos blocos de anotações do Jupyter para renderizar no navegador.

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

### <a name="send-the-function-to-sql-server"></a>Enviar a função para SQL Server

Neste exemplo, crie o contexto de computação remota e, em seguida, envie a execução da função para SQL Server com [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec). A função **rx_exec** é útil porque aceita um contexto de computação como um argumento. Qualquer função que você deseja executar remotamente deve ter um argumento de contexto de computação. Algumas funções, como [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) , dão suporte a esse argumento diretamente. Para operações que não têm, você pode usar **rx_exec** para entregar seu código em um contexto de computação remota.

Neste exemplo, nenhum dado bruto foi transferido do SQL Server para o Jupyter Notebook. Todos os cálculos ocorrem no banco de dados íris e apenas o arquivo de imagem é retornado ao cliente.

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

A captura de tela a seguir mostra a saída de gráfico de entrada e dispersão.

  ![jupyter Notebook mostrando a saída de gráfico de dispersão](media/jupyter-notebook-scatterplot.png)


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7-iniciar o Python em ferramentas

Como os desenvolvedores trabalham com frequência com várias versões do Python, a instalação não adiciona Python ao seu caminho. Para usar o executável do Python e as bibliotecas instaladas pela instalação, vincule o IDE ao **Python. exe** no caminho que também fornece **revoscalepy** e **microsoftml**. 

### <a name="command-line"></a>Linha de Comando

Ao executar o **Python. exe** em C:\Program Files\Microsoft\PyForMLS (ou em qualquer local que você especificou para a instalação da biblioteca de cliente do Python), você tem acesso à distribuição completa do Anaconda, além dos módulos Python da Microsoft, **revoscalepy** e **microsoftml**.

1. Vá para C:\Program Files\Microsoft\PyForMLS e clique duas vezes em **Python. exe**.
2. Abrir a ajuda interativa:`help()`
3. Digite o nome de um módulo no prompt de ajuda: `help> revoscalepy`. A ajuda retorna o nome, o conteúdo do pacote, a versão e o local do arquivo.
4. Retornar informações de versão e pacote no prompt de **>** de `revoscalepy`ajuda:. Pressione Enter algumas vezes para sair da ajuda.
5. Importar um módulo:`import revoscalepy`


### <a name="jupyter-notebooks"></a>Blocos de anotações do Jupyter

Este artigo usa notebooks Jupyter internos para demonstrar chamadas de função para **revoscalepy**. Se você for novo nesta ferramenta, a captura de tela a seguir ilustra como as peças se encaixam e por que tudo "simplesmente funciona". 

A pasta pai C:\Program Files\Microsoft\PyForMLS contém Anaconda e os pacotes da Microsoft. Os notebooks Jupyter estão incluídos no Anaconda, na pasta scripts, e os executáveis do Python são registrados automaticamente com notebooks Jupyter. Os pacotes encontrados em site-Packages podem ser importados para um notebook, incluindo os três pacotes da Microsoft usados para ciência de dados e aprendizado de máquina.

  ![Executáveis e bibliotecas](media/jupyter-notebook-python-registration.png)

Se você estiver usando outro IDE, será necessário vincular os executáveis do Python e as bibliotecas de funções à sua ferramenta. As seções a seguir fornecem instruções para ferramentas usadas com frequência.

### <a name="visual-studio"></a>Visual Studio

Se você tiver o [Python no Visual Studio](https://code.visualstudio.com/docs/languages/python), use as seguintes opções de configuração para criar um ambiente Python que inclui os pacotes python da Microsoft.

| Definição de configuração | value |
|-----------------------|-------|
| **Caminho do prefixo** | C:\Arquivos de Files\Microsoft\PyForMLS |
| **Caminho do intérprete** | C:\Arquivos de Files\Microsoft\PyForMLS\python.exe |
| **Interpretador em janelas** | C:\Arquivos de Files\Microsoft\PyForMLS\pythonw.exe |

Para obter ajuda para configurar um ambiente Python, consulte [Gerenciando ambientes Python no Visual Studio](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio).

### <a name="pycharm"></a>PyCharm

No PyCharm, defina o intérprete para o executável do Python instalado pelo Machine Learning Server.

1. Em um novo projeto, em configurações, clique em **Adicionar local**.

2. Insira `C:\Program Files\Microsoft\PyForMLS\`.

Agora você pode importar os módulos **revoscalepy**, **microsoftml**ou **azureml** . Você também pode escolher **ferramentas** > **console do Python** para abrir uma janela interativa.

## <a name="next-steps"></a>Próximas etapas

Agora que você tem ferramentas e uma conexão de trabalho com SQL Server, expanda suas habilidades executando os guias de início rápido do Python usando o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

> [!div class="nextstepaction"]
> [Início Rápido: Verifique se o Python existe no SQL Server](../tutorials/quickstart-python-verify.md)