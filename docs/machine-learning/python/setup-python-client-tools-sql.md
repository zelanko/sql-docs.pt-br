---
title: Configurar um cliente de ciência de dados do Python
description: Configure um ambiente local do Python (Jupyter Notebook ou PyCharm) para conexões remotas a Serviços de Machine Learning do SQL Server com o Python.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/04/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5199f22e5e72e68be3b1a76769fb8bd3a9518413
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956597"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>Configurar um cliente de ciência de dados para desenvolvimento em Python nos Serviços de Machine Learning do SQL Server
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

A integração do Python está disponível no SQL Server 2017 e posterior, quando você inclui a opção do Python em uma [instalação de Serviços de Machine Learning (no banco de dados)](../install/sql-machine-learning-services-windows-install.md). 

Para desenvolver e implantar soluções Python para SQL Server, instale o [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) da Microsoft e outras bibliotecas do Python em sua estação de trabalho de desenvolvimento. A biblioteca revoscalepy, que também está na instância do SQL Server remoto, coordena as solicitações de computação entre os dois sistemas. 

Neste artigo, saiba como configurar uma estação de trabalho de desenvolvimento do Python para que você possa interagir com um SQL Server remoto habilitado para aprendizado de máquina e para integração com o Python. Depois de concluir as etapas neste artigo, você terá as mesmas bibliotecas do Python que aquelas existentes no SQL Server. Você também saberá como enviar por push cálculos de uma sessão local do Python para uma sessão remota do Python no SQL Server.

![Componentes cliente-servidor](media/sqlmls-python-client-revo.png "Bibliotecas e sessões locais e remotas do Python")

Para validar a instalação, você pode usar Jupyter Notebooks internos conforme descrito neste artigo ou [vincular as bibliotecas](#install-ide) ao PyCharm ou a qualquer outro IDE que você normalmente use.

> [!Tip]
> Para ver uma demonstração em vídeo desses exercícios, confira [Executar R e Python remotamente no SQL Server de Jupyter Notebooks](https://youtu.be/D5erljpJDjE).

> [!Note]
> Uma alternativa à instalação da biblioteca de clientes é usar um [servidor autônomo](../install/sql-machine-learning-standalone-windows-install.md) como um cliente avançado, que alguns clientes preferem para trabalho em um cenário mais aprofundado. Um servidor autônomo é totalmente dissociado do SQL Server, mas já que ele tem as mesmas bibliotecas do Python, você pode usá-lo como um cliente para análise no banco de dados do SQL Server. Você também pode usá-lo para trabalho não relacionado ao SQL, incluindo a capacidade de importar e modelar dados de outras plataformas de dados. Se você instalar um servidor autônomo, poderá encontrar o executável do Python nesta localização: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`. Para validar a instalação, [abra um Jupyter Notebook](#python-tools) para executar comandos usando o Python.exe nessa localização.

## <a name="commonly-used-tools"></a>Ferramentas usadas com frequência

Seja você um desenvolvedor de Python não familiarizado com o SQL ou um desenvolvedor do SQL não familiarizado com o Python e a análise no banco de dados, você precisará de uma ferramenta de desenvolvimento Python e de um editor de consultas T-SQL (como o [SSMS, SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md) para fazer uso de todas as funcionalidades da análise no banco de dados.

Para o desenvolvimento em Python, você pode usar Jupyter Notebooks, que vêm agrupados na distribuição do Anaconda instalada pelo SQL Server. Este artigo explica como iniciar o Jupyter Notebooks para que você possa executar o código Python localmente e remotamente no SQL Server.

O SSMS é um download separado, útil para criar e executar procedimentos armazenados no SQL Server, incluindo aqueles que contêm código Python. Praticamente qualquer código Python que você escreva nos Jupyter Notebooks poderá ser inserido em um procedimento armazenado. Você pode percorrer outros guias de início rápido para saber mais sobre [SSMS e Python inserido](../tutorials/quickstart-python-create-script.md).

## <a name="1---install-python-packages"></a>1 – Instalar pacotes do Python

As estações de trabalho locais devem ter as mesmas versões de pacote do Python que aquelas no SQL Server, incluindo o Anaconda 4.2.0 básico com a distribuição 3.5.2 do Python e pacotes específicos da Microsoft.

Um script de instalação adiciona três bibliotecas específicas da Microsoft ao cliente Python. O script instala [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), usado para definir objetos de fonte de dados e o contexto de computação. Ele instala [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package), fornecendo algoritmos de aprendizado de máquina. O pacote [azureml](/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) também está instalado, mas se aplica a tarefas de operacionalização associadas a um contexto de Machine Learning Server autônomo (não de instância) e o uso dele para análise no banco de dados pode ser limitado.

1. Baixe um script de instalação.

   + [https://aka.ms/mls-py](https://aka.ms/mls-py) instala a versão 9.2.1 dos pacotes do Microsoft Python. Essa versão corresponde a uma instância do SQL Server padrão. 

   + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) instala a versão 9.3 dos pacotes do Microsoft Python. Essa versão será uma opção melhor se a instância de SQL Server remota estiver [associada ao Machine Learning Server 9.3](../install/upgrade-r-and-python.md).

2. Abra uma janela do PowerShell com permissões de administrador elevadas (clique com o botão direito do mouse em **Executar como administrador**).

3. Vá para a pasta em que você baixou o instalador e execute o script. Adicione o argumento de linha de comando `-InstallFolder` para especificar uma localização de pasta para as bibliotecas. Por exemplo: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

Se você omitir a pasta de instalação, o padrão será C:\Program Files\Microsoft\PyForMLS.

A instalação leva algum tempo para ser concluída. Você pode monitorar o progresso na janela do PowerShell. Quando a instalação for concluída, você terá um conjunto completo de pacotes. 

> [!Tip] 
> Recomendamos as [Perguntas frequentes sobre o Python no Windows](https://docs.python.org/3/faq/windows.html) para obter informações gerais sobre a execução de programas Python no Windows.

## <a name="2---locate-executables"></a>2 – Localizar os executáveis

Ainda no PowerShell, liste o conteúdo da pasta de instalação para confirmar se o Python.exe, os scripts e outros pacotes estão instalados. 

1. Insira `cd \` para ir para a unidade raiz e, em seguida, insira o caminho especificado para `-InstallFolder` na etapa anterior. Se você omitir esse parâmetro durante a instalação, o padrão será `cd C:\Program Files\Microsoft\PyForMLS`.

2. Insira `dir *.exe` para listar os executáveis. Você deve ver **python.exe**, **pythonw.exe** e **uninstall-anaconda.exe**.

   ![Lista de executáveis do Python](media/powershell-python-exe.png)
   
Em sistemas com várias versões do Python, lembre-se de usar esse Python. exe específico se você quiser carregar **revoscalepy** e outros pacotes da Microsoft.

> [!Note] 
> O script de instalação não modifica a variável de ambiente PATH no seu computador, o que significa que o novo interpretador do Python e os módulos que você acabou de instalar não ficam automaticamente disponíveis para outras ferramentas que você possa ter. Para obter ajuda sobre como vincular o interpretador do Python e as bibliotecas a ferramentas, confira [Instalar um IDE](#install-ide).

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3 – Abrir Jupyter Notebooks

O Anaconda inclui Jupyter Notebooks. Como uma próxima etapa, crie um notebook e execute código Python contendo as bibliotecas que você acabou de instalar.

1. No prompt do PowerShell, ainda no diretório C:\Program Files\Microsoft\PyForMLS, abra Jupyter Notebooks da pasta Scripts:

   ```powershell
   .\Scripts\jupyter-notebook
   ```

   Um notebook deve ser aberto no navegador padrão em `https://localhost:8889/tree`.

   Outra maneira de começar é clicar duas vezes em **jupyter-notebook.exe**. 

2. Clique em **Novo** e em **Python 3**.

   ![Jupyter Notebook com a seleção Novo – Python 3](media/jupyter-notebook-new-p3.png)

3. Insira `import revoscalepy` e execute o comando para carregar uma das bibliotecas específicas da Microsoft.

4. Insira e execute `print(revoscalepy.__version__)` para retornar as informações de versão. Você deverá ver 9.2.1 ou 9.3.0. Você pode usar qualquer uma dessas versões com [revoscalepy no servidor](../package-management/r-package-information.md).

4. Insira uma série mais complexa de instruções. Este exemplo gera estatísticas de resumo usando [rx_summary](/machine-learning-server/python-reference/revoscalepy/rx-summary) em um conjunto de dados local. Outras funções obtêm a localização dos dados de exemplo e criam um objeto de fonte de dados para um arquivo .xdf local.

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

A captura de tela a seguir mostra a entrada e uma parte da saída, reduzida para fins de brevidade.

  ![Jupyter Notebook mostrando entradas e saída do revoscalepy](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4 – Obter Permissões do SQL

Para se conectar a uma instância do SQL Server para executar scripts e fazer upload de dados, você deve ter um logon válido no servidor de banco de dados. Você pode usar um logon SQL ou a autenticação integrada do Windows. Geralmente, é recomendável usar a autenticação integrada do Windows, mas usar o logon do SQL é mais simples para alguns cenários, especialmente quando o script contém cadeias de conexão para dados externos.

No mínimo, a conta usada para executar o código deve ter permissão para ler os bancos de dados com os quais você está trabalhando, além da permissão especial EXECUTE ANY EXTERNAL SCRIPT. A maioria dos desenvolvedores também exige permissões para criar procedimentos armazenados e para gravar dados em tabelas que contêm dados de treinamento ou dados pontuados. 

Peça ao administrador do banco de dados para [configurar as permissões a seguir para sua conta](../security/user-permission.md), no banco de dados em que você usa o Python:

+ **EXECUTE ANY EXTERNAL SCRIPT** para executar o Python no servidor.
+ Privilégios de **db_datareader** para executar as consultas usadas para treinar o modelo.
+ **db_datawriter** para gravar dados de treinamento ou dados pontuados.
+ **db_owner** para criar objetos como procedimentos armazenados, tabelas e funções. 
  Você também precisa de **db_owner** para criar bancos de dados de exemplo e de teste. 

Se o código exigir pacotes que não sejam instalados por padrão com o SQL Server, providencie junto ao administrador de banco de dados para que os pacotes sejam instalados com a instância. O SQL Server é um ambiente seguro e há restrições sobre onde os pacotes podem ser instalados. A instalação ad hoc de pacotes como parte do seu código não é recomendada, mesmo que você tenha direitos para tal. Além disso, sempre considere cuidadosamente as implicações de segurança antes de instalar novos pacotes na biblioteca do servidor.


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5 – Criar dados de teste

Se tiver permissões para criar um banco de dados no servidor remoto, você poderá executar o código a seguir para criar o banco de dados de demonstração Iris usado para as etapas restantes neste artigo.

### <a name="1---create-the-irissql-database-remotely"></a>1 – Criar o banco de dados irissql remotamente

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

### <a name="2---import-iris-sample-from-sklearn"></a>2 – Importar o exemplo do Iris de SkLearn

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3 – Usar APIs Revoscalepy para criar uma tabela e carregar os dados do Iris

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6 – Testar a conexão remota

Antes de tentar esta próxima etapa, verifique se você tem permissões na instância do SQL Server e uma cadeia de conexão para o [banco de dados de exemplo do Iris](../tutorials/demo-data-iris-in-sql.md). Se o banco de dados não existir e você tiver permissões suficientes, você poderá [Criar um banco de dados usando essas instruções embutidas](#create-iris-remotely).

Substitua a cadeia de conexão por valores válidos. O código de exemplo usa `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"`, mas seu código deve especificar um servidor remoto, possivelmente com um nome de instância, bem como uma opção de credencial que mapeie para o logon de usuário do banco de dados.

### <a name="define-a-function"></a>Definir uma função

O código a seguir define uma função que você enviará para o SQL Server em uma etapa posterior. Quando executado, ele usa dados e bibliotecas (revoscalepy, pandas, matplotlib) no servidor remoto para criar gráficos de dispersão do conjunto de dados Iris. Ele retorna o fluxo de bytes do .png para os Jupyter Notebooks para que ele seja renderizado no navegador.

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

Neste exemplo, crie o contexto de computação remota e, em seguida, envie a execução da função para o SQL Server com [rx_exec](/machine-learning-server/python-reference/revoscalepy/rx-exec). A função **rx_exec** é útil porque aceita um contexto de computação como um argumento. Qualquer função que você desejar executar remotamente deverá ter um argumento de contexto de computação. Algumas funções, tais como [rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), oferecem suporte direto a esse argumento. Para operações que não oferecem, você pode usar **rx_exec** para entregar seu código em um contexto de computação remota.

Neste exemplo, nenhum dado bruto foi transferido do SQL Server para o Jupyter Notebook. Toda a computação ocorre no banco de dados Iris e apenas o arquivo de imagem é retornado ao cliente.

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

A captura de tela a seguir mostra a entrada e a saída de gráfico de dispersão.

  ![Jupyter Notebook mostrando a saída de gráfico de dispersão](media/jupyter-notebook-scatterplot.png)


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7 – Iniciar o Python por meio das ferramentas

Já que os desenvolvedores muitas vezes trabalham com várias versões do Python, a instalação não adiciona o Python ao seu PATH. Para usar o executável do Python e as bibliotecas instaladas juntamente com a instalação principal, vincule o IDE a **Python.exe** no caminho que também fornece **revoscalepy** e **microsoftml**. 

### <a name="command-line"></a>Linha de comando

Quando você executa **Python.exe** de C:\Program Files\Microsoft\PyForMLS (ou qualquer localização especificada para a instalação da biblioteca de clientes do Python), você tem acesso à distribuição completa do Anaconda e aos módulos do Microsoft Python, **revoscalepy** e **microsoftml**.

1. Acesse C:\Program Files\Microsoft\PyForMLS e clique duas vezes em **Python. exe**.
2. Abra a ajuda interativa: `help()`
3. Digite o nome de um módulo no prompt de ajuda: `help> revoscalepy`. A ajuda retorna o nome, o conteúdo do pacote, a versão e a localização do arquivo.
4. Retorne as informações de versão e de pacote no prompt **ajuda>** : `revoscalepy`. Pressione Enter algumas vezes para sair da ajuda.
5. Importar um módulo: `import revoscalepy`


### <a name="jupyter-notebooks"></a>Jupyter Notebooks

Este artigo usa Jupyter Notebooks internos para demonstrar chamadas de função para **revoscalepy**. Caso não esteja familiarizado com essa ferramenta, a captura de tela a seguir ilustra como as peças se encaixam e por que tudo "simplesmente funciona". 

A pasta pai C:\Program Files\Microsoft\PyForMLS contém o Anaconda e os pacotes da Microsoft. Os Jupyter Notebooks estão incluídos no Anaconda (na pasta scripts) e os executáveis do Python são registrados automaticamente com Jupyter Notebooks. Os pacotes encontrados em pacotes de site podem ser importados para um notebook, incluindo os três pacotes da Microsoft usados para ciência de dados e aprendizado de máquina.

  ![Executáveis e bibliotecas](media/jupyter-notebook-python-registration.png)

Se você estiver usando outro IDE, será necessário vincular os executáveis do Python e as bibliotecas de funções à sua ferramenta. As seções a seguir contêm instruções sobre ferramentas usadas com frequência.

### <a name="visual-studio"></a>Visual Studio

Se você tiver o [Python no Visual Studio](https://code.visualstudio.com/docs/languages/python), use as opções de configuração a seguir para criar um ambiente do Python que inclua os pacotes do Microsoft Python.

| Definição de configuração | value |
|-----------------------|-------|
| **Caminho do prefixo** | C:\Program Files\Microsoft\PyForMLS |
| **Caminho do interpretador** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **Interpretador em janelas** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

Para obter ajuda na configuração de um ambiente Python, confira [Gerenciar ambientes Python no Visual Studio](/visualstudio/python/managing-python-environments-in-visual-studio).

### <a name="pycharm"></a>PyCharm

No PyCharm, defina o interpretador para o executável do Python instalado pelo Machine Learning Server.

1. Em um novo projeto, em Configurações, clique em **Adicionar Local**.

2. Digite `C:\Program Files\Microsoft\PyForMLS\`.

Agora você pode importar os módulos **revoscalepy**, **microsoftml** ou **azureml**. Você também pode escolher **Ferramentas** > **Console do Python** para abrir uma Janela interativa.

## <a name="next-steps"></a>Próximas etapas

Agora que você tem ferramentas e uma conexão funcional com o SQL Server, expanda suas habilidades percorrendo os guias de início rápido do Python usando o [SSMS (SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md).

> [!div class="nextstepaction"]
> [Início Rápido: Criar e executar scripts Python simples com os Serviços de Machine Learning do SQL Server](../tutorials/quickstart-python-create-script.md)