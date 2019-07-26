---
title: Obter informações do pacote R e Python
description: Determine a versão do pacote do R e do Python, verifique a instalação e obtenha uma lista de pacotes instalados em SQL Server R Services ou Serviços de Machine Learning.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: cec029f4ffb047a49ff9902c430c4bd98aa03850
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470283"
---
#  <a name="get-r-and-python-package-information"></a>Obter informações do pacote R e Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Às vezes, quando você trabalha com vários ambientes ou instalações de R ou Python, precisa verificar se o código que está sendo executado está usando o ambiente esperado para Python ou o espaço de trabalho correto para R. Por exemplo, se você tiver [atualizado R ou Python](../install/upgrade-r-and-python.md), o caminho para a biblioteca do R pode estar em uma pasta diferente da padrão. Além disso, se você instalar o cliente R ou uma instância do servidor autônomo, poderá ter várias bibliotecas de R em seu computador.

Exemplos de script R e Python neste artigo mostram como obter o caminho e a versão dos pacotes usados pelo SQL Server.

## <a name="get-the-r-library-location"></a>Obter o local da biblioteca do R

Para qualquer versão do SQL Server, execute a seguinte instrução para verificar a biblioteca padrão do pacote R para a instância atual:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Opcionalmente, você pode usar o [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) em versões mais recentes do RevoScaleR no SQL Server 2017 serviços de Machine Learning ou [r Services tiver atualizado o r para pelo menos RevoScaleR 9.0.1](../install/upgrade-r-and-python.md). Esse procedimento armazenado retorna o caminho da biblioteca de instâncias e a versão do RevoScaleR usada pelo SQL Server:

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
> A função [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) pode ser executada somente no computador local. A função não pode retornar caminhos de biblioteca para conexões remotas.

**Resultados**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>Obter o local da biblioteca do Python

Para **Python** no SQL Server 2017, execute a instrução a seguir para verificar a biblioteca padrão para a instância atual. Este exemplo retorna a lista de pastas incluídas na variável do `sys.path` Python. A lista inclui o diretório atual e o caminho da biblioteca padrão.

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

Para obter mais informações sobre a `sys.path` variável e como ela é usada para definir o caminho de pesquisa do intérprete para os módulos, consulte a [documentação do python](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>Listar todos os pacotes

Há várias maneiras pelas quais você pode obter uma lista completa dos pacotes atualmente instalados. Uma vantagem de executar os comandos da lista de pacotes do sp_execute_external_script é que você tem a garantia de obter os pacotes instalados na biblioteca de instâncias.

### <a name="r"></a>R

O exemplo a seguir usa a função `installed.packages()` R em [!INCLUDE[tsql](../../includes/tsql-md.md)] um procedimento armazenado para obter uma matriz de pacotes que foram instalados na biblioteca R_SERVICES para a instância atual. Esse script retorna os campos de nome e versão do pacote no arquivo de descrição, somente o nome é retornado.

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

Para obter mais informações sobre os campos opcionais e padrão para o campo de descrição do [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)pacote R, consulte.

### <a name="python"></a>Python

O `pip` módulo é instalado por padrão e oferece suporte a muitas operações para listar pacotes instalados, além daqueles com suporte do Python padrão. É claro que `pip` você pode executar a partir de um prompt de comando do Python, mas também pode chamar algumas `sp_execute_external_script`funções PIP do.

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

Ao executar `pip` a partir da linha de comando, há muitas outras funções úteis `pip list` : Obtém todos os pacotes que estão instalados `pip freeze` , enquanto lista os pacotes `pip`instalados pelo e não lista os pacotes que o próprio Pip depende de. Você também pode usar `pip freeze` para gerar um arquivo de dependência.

## <a name="find-a-single-package"></a>Localizar um único pacote

Se você instalou um pacote e deseja verificar se ele está disponível para uma instância específica do SQL Server, você pode executar a chamada de procedimento armazenado a seguir para carregar o pacote e retornar apenas as mensagens.

### <a name="r"></a>R

Este exemplo procura e carrega a biblioteca RevoScaleR, se disponível.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ Se o pacote for encontrado, uma mensagem será retornada: "Comandos concluídos com êxito."

+ Se o pacote não puder ser localizado ou carregado, você receberá um erro contendo o texto: "não há um pacote chamado ' MissingPackageName '"

### <a name="python"></a>Python

A verificação equivalente do Python pode ser executada no Shell do Python, usando `conda` comandos `pip` ou. Como alternativa, execute esta instrução em um procedimento armazenado:

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

## <a name="get-package-version"></a>Obter versão do pacote

Você pode obter informações de versão do pacote R e Python usando Management Studio.

### <a name="r-package-version"></a>Versão do pacote R

Essa instrução retorna a versão do pacote RevoScaleR e a versão base do R.

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("RevoScaleR"))
print(packageDescription("base"))
'
```

### <a name="python-package-version"></a>Versão do pacote do Python

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

+ [Instalar os novos pacotes R](../r/install-additional-r-packages-on-sql-server.md)
+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)