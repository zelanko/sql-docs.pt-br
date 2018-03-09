---
title: Exibindo R ou pacotes Python instalados no SQL Server | Microsoft Docs
ms.custom: 
ms.date: 02/19/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 0a9be77fc7d7a61761a91d231aba2eaf36af8f56
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2018
---
# <a name="viewing-r-or-python-packages-installed-on-sql-server"></a>Exibindo R ou pacotes Python instalados no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Se você instalou vários ambientes de Python, ou usa várias ferramentas de R, é fácil de instalar um pacote para a biblioteca incorreta ou o ambiente e, em seguida, não poderá encontrá-lo mais tarde. 

Este artigo fornece algumas consultas que você pode usar para determinar a versão atual e para listar os pacotes que estão instalados no ambiente atual do SQL Server.

## <a name="verify-the-current-default-library"></a>Verifique se a biblioteca padrão atual

Para **R** no SQL Server, execute a seguinte instrução para verificar se a biblioteca padrão para a instância atual:

```sql
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Para **Python** no SQL Server, execute a seguinte instrução para verificar se a biblioteca padrão para a instância atual:

```sql
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

## <a name="generate-a-package-list-using-a-stored-procedure"></a>Gerar uma lista de pacote usando um procedimento armazenado

Há várias maneiras que você pode obter uma lista completa dos pacotes instalados no momento. Uma vantagem de executar os comandos da lista de pacote de sp_execute_external_script é que você terá garantia de obter pacotes instalados na biblioteca de instância.

### <a name="r"></a>R

O exemplo a seguir usa a função R `installed.packages()` em uma [!INCLUDE [tsql](..\..\includes\tsql-md.md)] procedimento armazenado para obter uma matriz de pacotes que foram instalados na biblioteca do R_SERVICES para a instância atual. Para evitar a análise dos campos no arquivo DESCRIPTION, somente o nome será retornado.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

Para obter mais informações sobre opcional e campos padrão para o campo de descrição do pacote de R, consulte [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

### <a name="python"></a>Python

O `pip` módulo é instalado por padrão e dá suporte a muitas operações de pacotes de listagem instalado, além daqueles suportados pelo Python padrão. Você pode executar `pip` de um Python prompt de comando, logicamente, mas você também pode chamar algumas funções de pip de `sp_execute_external_script`.

```sql
execute sp_execute_external_script 
@language = N'Python', 
@script = N'
import pip
import pandas as pd
installed_packages = pip.get_installed_distributions()
installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

Ao executar `pip` na linha de comando, há muitas outras funções úteis: `pip list` obtém todos os pacotes que estão instalados, enquanto `pip freeze` lista os pacotes instalados por `pip`e não listar os pacotes pip próprio depende. Você também pode usar `pip freeze` para gerar um arquivo de dependência.

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>Verificar se um pacote está instalado com uma instância

Se você tiver instalado um pacote e deseja ter certeza de que ele esteja disponível para uma determinada instância do SQL Server, você pode executar a seguinte chamada de procedimento armazenado para carregar o pacote e retornar apenas as mensagens.

### <a name="r"></a>R

Este exemplo procura e carrega a biblioteca RevoScaleR, se disponível.

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'require("RevoScaleR")'
GO
```

+ Se o pacote for encontrado, uma mensagem será retornada: "Comandos concluída com êxito."

+ Se o pacote não pode ser localizado ou carregado, você receberá um erro que contém o texto: "não há nenhum pacote chamado 'MissingPackageName'"

### <a name="python"></a>Python

A verificação de equivalente do Python pode ser executada de Python de shell, usando `conda` ou `pip` comandos. Como alternativa, execute esta instrução em um procedimento armazenado:

```sql
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import pip
import pkg_resources
pckg_name = "revoscalepy"
pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")
```

## <a name="view-installed-packages-using-a-utility-or-ide"></a>Exibir os pacotes instalados usando um utilitário ou um IDE

A maioria das ferramentas de desenvolvimento fornecem um pesquisador de objetos ou uma lista de pacotes instalados ou carregados no espaço de trabalho atual ou do ambiente. Esta seção fornece algumas dicas curtas para usar ferramentas populares de R ou Python.

### <a name="r-tools"></a>Ferramentas de R

Há várias maneiras de obter uma lista de pacotes instalados ou carregados usando utilitários R. 

+ Do utilitário local do R, use uma função de base R, como `installed.packages()`, que está incluído o `utils` pacote. Para obter uma lista que é precisa para uma instância, você deve especificar explicitamente o caminho da biblioteca ou usar as ferramentas de R associadas com a biblioteca de instância.

### <a name="python-tools"></a>Ferramentas do Python

Extensões do Python para Visual Studio facilitam muito exibir os pacotes instalados no ambiente atual, ou em outros ambientes virtuais listadas no IDE. Você pode configurar vários ambientes, escolha um ambiente de uma lista e exibir os pacotes ou instalar novos pacotes nesse ambiente.

+ [Ambientes de Python](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

Código do Visual Studio é um editor livre que oferece suporte a Python, com várias linters Python disponíveis. Embora o código VS não fornece um navegador de pacote como o Visual Studio, oferece suporte à configuração e entre vários ambientes.

+ [Python no código do Visual Studio](https://code.visualstudio.com/docs/languages/python)

Algumas configurações adicionais podem ser necessárias para executar **revoscalepy** comandos de um cliente remoto:

+ [Instalar o interpretador e pacotes do Python personalizados localmente no Windows](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)

Este blog fornece algumas dicas úteis sobre como configurar outros ambientes de Python, incluindo PyCharm, para trabalhar com **revoscalepy**.

+ [Introdução aos serviços Web de Python usando o servidor de aprendizado de máquina](https://blogs.msdn.microsoft.com/mlserver/2017/12/13/getting-started-with-python-web-services-using-machine-learning-server/)

## <a name="use-functions-from-machine-learning-server"></a>Usar as funções de servidor de aprendizado de máquina

Porque as bibliotecas usadas com a execução de suporte do SQL Server de código de um cliente remoto, você pode usar essas funções para descobrir quais pacotes estão instalados em um ambiente remoto.

### <a name="revoscaler"></a>RevoScaleR

Se você estiver trabalhando em um cliente remoto e não tem acesso ao servidor, você ainda pode obter uma lista de pacotes que estão instalados no SQL Server, usando funções de RevoScaleR. Especifique o SQL Server como um contexto de computação, o que exige que você tenha permissão para se conectar ao servidor. 

+ [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) localiza o caminho para um pacote no contexto de computação remota.

+ [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) obtém informações sobre os pacotes instalados em um contexto de computação.

Por exemplo, execute o seguinte código de R para obter uma lista de pacotes disponíveis no contexto de computação do SQL Server especificado.

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```

O exemplo a seguir obtém a localização da biblioteca de RevoScaleR no contexto de computação local e a versão do pacote.

```R
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

### <a name="revoscalepy"></a>revoscalepy

Funções semelhantes de RevoScaleR não estão disponíveis no momento. Procure-as em uma versão posterior do **revoscalepy**.

## <a name="get-library-location-and-version"></a>Obter a versão e o local da biblioteca

Às vezes, quando você estiver trabalhando com vários ambientes ou instalações de R ou Python, você precisa verificar se o código que você está executando está usando o ambiente correto para Python ou o espaço de trabalho correto para R.

Por exemplo, se você atualizou a componentes usando associação de aprendizado de máquina, o caminho para a biblioteca R pode estar em uma pasta diferente do padrão. Além disso, se você instalar o cliente de R ou uma instância de servidor autônomo, você pode ter várias bibliotecas de R no seu computador.

Estes exemplos mostram como obter o caminho e a versão da biblioteca que está sendo usada pelo SQL Server.

### <a name="r"></a>R

Esse procedimento armazenado retorna o caminho da biblioteca de instância e a versão do pacote RevoScaleR usado pelo SQL Server:

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> O [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) função pode ser executada somente no computador de destino. A função não pode retornar os caminhos de biblioteca para conexões remotas.

**Resultados**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```

### <a name="python"></a>Python

Este exemplo retorna a lista de pastas incluídas no Python `sys.path` variável. A lista inclui o diretório atual e o caminho de biblioteca padrão.

```sql
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**Resultados**

```text
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

Para obter mais informações sobre a variável `sys.path` e como ele é usado para definir o caminho de pesquisa do interpretador para módulos, consulte o [documentação Python](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

