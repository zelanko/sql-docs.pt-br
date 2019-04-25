---
title: Obter informações de pacote de R e Python - serviços do SQL Server Machine Learning
description: Determinar a versão do pacote de R e Python, verificar a instalação e obter uma lista de pacotes instalados no SQL Server R Services ou serviços de Machine Learning.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/08/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 3e7dd580cd7d03235be704a7c46e5171a6526ae8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506218"
---
#  <a name="get-r-and-python-package-information"></a>Obter informações de pacote de R e Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Às vezes, quando você estiver trabalhando com vários ambientes ou instalações do R ou Python, você precisa verificar se o código que você está executando está usando o ambiente esperado para o Python ou o espaço de trabalho correto para R. Por exemplo, se você tiver atualizado os componentes por meio de aprendizado de máquina [associação](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md), o caminho para a biblioteca de R pode ser em uma pasta diferente do padrão. Além disso, se você instalar o cliente do R ou uma instância de servidor autônomo, você pode ter várias bibliotecas do R em seu computador.

Exemplos de script de R e Python neste artigo mostram como obter o caminho e a versão de pacotes usados pelo SQL Server.

## <a name="get-the-r-library-location"></a>Obter o local da biblioteca de R

Para qualquer versão do SQL Server, execute a seguinte instrução para verificar se o [biblioteca de pacote padrão do R](installing-and-managing-r-packages.md) para a instância atual:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Opcionalmente, você pode usar [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) nas versões mais recentes do RevoScaleR nos serviços de aprendizado de máquina do SQL Server 2017 ou [serviços de R atualizados R para pelo menos RevoScaleR 9.0.1](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). Esse procedimento armazenado retorna o caminho da biblioteca de instância e a versão do RevoScaleR usada pelo SQL Server:

```sql
EXECUTE sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> O [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) função pode ser executada somente no computador local. A função não pode retornar os caminhos de biblioteca para conexões remotas.

**Resultados**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>Obter o local de biblioteca do Python

Para **Python** no SQL Server 2017, execute a seguinte instrução para verificar se a biblioteca padrão para a instância atual. Este exemplo retorna a lista de pastas incluídas no Python `sys.path` variável. A lista inclui o diretório atual e o caminho da biblioteca padrão.

```sql
EXECUTE sp_execute_external_script
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

Para obter mais informações sobre a variável `sys.path` e como ele é usado para definir o caminho de pesquisa do interpretador para módulos, consulte o [documentação do Python](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>Listar todos os pacotes

Há várias maneiras que você pode obter uma lista completa dos pacotes atualmente instalados. Uma vantagem de executar comandos de lista do pacote de sp_execute_external_script é que há garantia para obter os pacotes instalados na biblioteca de instância.

### <a name="r"></a>R

O exemplo a seguir usa a função R `installed.packages()` em um [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimento armazenado para obter uma matriz de pacotes que foram instalados na biblioteca R_SERVICES da instância atual. Esse script retorna campos de nome e a versão do pacote no arquivo de descrição, apenas o nome é retornado.

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

Para obter mais informações sobre opcional e campos padrão para o campo de descrição do pacote de R, consulte [ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

### <a name="python"></a>Python

O `pip` módulo é instalado por padrão e dá suporte a muitas operações para a listagem instalado pacotes, além daqueles suportados pelo Python padrão. Você pode executar `pip` de um Python prompt de comando, é claro, mas você também pode chamar algumas funções de pip do `sp_execute_external_script`.

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
  import pip
  import pandas as pd
  installed_packages = pip.get_installed_distributions()
  installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
  df = pd.DataFrame(installed_packages_list)
  OutputDataSet = df'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

Ao executar `pip` da linha de comando, há muitas outras funções úteis: `pip list` obtém todos os pacotes que estão instalados, enquanto `pip freeze` lista os pacotes instalados por `pip`e não listar os pacotes do pip em si depende. Você também pode usar `pip freeze` para gerar um arquivo de dependência.

## <a name="find-a-single-package"></a>Localizar um único pacote

Se você tiver instalado um pacote e certifique-se de que ele esteja disponível para uma determinada instância do SQL Server, você pode executar a seguinte chamada de procedimento armazenado para carregar o pacote e retornar apenas as mensagens.

### <a name="r"></a>R

Este exemplo procura e carrega a biblioteca RevoScaleR, se disponível.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ Se o pacote for encontrado, uma mensagem será retornada: "Comandos concluídos com êxito".

+ Se o pacote não pode ser localizado ou carregado, você obterá um erro que contém o texto: "não há nenhum pacote chamado 'MissingPackageName'"

### <a name="python"></a>Python

A verificação de equivalente para o Python pode ser realizada com o Python de shell, usando `conda` ou `pip` comandos. Como alternativa, execute esta instrução em um procedimento armazenado:

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
  import pip
  import pkg_resources
  pckg_name = "revoscalepy"
  pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
  installed_pckg = pckgs.query(''key == @pckg_name'')
  print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")'
```

<a name="get-package-vers"></a>

## <a name="get-package-version"></a>Obter a versão do pacote

Você pode obter o R e Python usando o Management Studio de informações de versão do pacote.

### <a name="r-package-version"></a>Versão do pacote de R

Essa instrução retorna a versão do pacote RevoScaleR e a versão base do R.

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("RevoScaleR"))
print(packageDescription("base"))
'
```

### <a name="python-package-version"></a>Versão do pacote Python

Essa instrução retorna a versão do pacote revoscalepy e a versão do Python.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import revoscalepy
import sys
print(revoscalepy.__version__)
print(sys.version)
'
```

## <a name="next-steps"></a>Próximas etapas

+ [Instalar os novos pacotes R](install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)