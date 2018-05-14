---
title: Obter informações de pacote de R e Python no aprendizado de máquina do SQL Server | Microsoft Docs
description: Determinar a versão do pacote de R e Python, verifique se a instalação e obter uma lista de pacotes instalados no SQL Server R Services ou serviços de aprendizado de máquina.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 21975b4a59cbfaf1e3a203bc732543144856633f
ms.sourcegitcommit: df382099ef1562b5f2d1cd506c1170d1db64de41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/12/2018
---
#  <a name="get-r-and-python-package-information-on-sql-server"></a>Obter informações de pacote de R e Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Às vezes, quando você estiver trabalhando com vários ambientes ou instalações de R ou Python, você precisa verificar se o código que você está executando está usando o ambiente esperado para Python ou o espaço de trabalho correto para R. Por exemplo, se você atualizou a componentes usando associação de aprendizado de máquina, o caminho para a biblioteca R pode estar em uma pasta diferente do padrão. Além disso, se você instalar o cliente de R ou uma instância de servidor autônomo, você pode ter várias bibliotecas de R no seu computador.

Os exemplos neste artigo mostram como obter o caminho e a versão da biblioteca que está sendo usada pelo SQL Server.

## <a name="get-the-current-r-library"></a>Obter a biblioteca atual do R

Para **R** em qualquer versão do SQL Server, execute a seguinte instrução para verificar se a biblioteca padrão para a instância atual:

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

Opcionalmente, você pode usar rxSqlLibPaths nas versões mais recentes de RevoScaleR nos serviços de aprendizado de máquina do SQL Server de 2017 ou [R Services atualizado R no mínimo RevoScaleR 9.0.1](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md). Esse procedimento armazenado retorna o caminho da biblioteca de instância e a versão do RevoScaleR usada pelo SQL Server:

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

## <a name="get-the-current-python-library"></a>Obter a biblioteca do Python atual

Para **Python** no SQL Server de 2017, execute a seguinte instrução para verificar se a biblioteca padrão para a instância atual. Este exemplo retorna a lista de pastas incluídas no Python `sys.path` variável. A lista inclui o diretório atual e o caminho de biblioteca padrão.

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

Para obter mais informações sobre a variável `sys.path` e como ele é usado para definir o caminho de pesquisa do interpretador para módulos, consulte o [documentação Python](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>Lista todos os pacotes

Há várias maneiras que você pode obter uma lista completa dos pacotes instalados no momento. Uma vantagem de executar os comandos da lista de pacote de sp_execute_external_script é que você terá garantia de obter pacotes instalados na biblioteca de instância.

### <a name="r"></a>R

O exemplo a seguir usa a função R `installed.packages()` em uma [!INCLUDE [tsql](..\..\includes\tsql-md.md)] procedimento armazenado para obter uma matriz de pacotes que foram instalados na biblioteca do R_SERVICES para a instância atual. Esse script retorna campos de nome e versão do pacote no arquivo DESCRIPTION, somente o nome será retornado.

```SQL
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

O `pip` módulo é instalado por padrão e dá suporte a muitas operações de pacotes de listagem instalado, além daqueles suportados pelo Python padrão. Você pode executar `pip` de um Python prompt de comando, logicamente, mas você também pode chamar algumas funções de pip de `sp_execute_external_script`.

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

Ao executar `pip` na linha de comando, há muitas outras funções úteis: `pip list` obtém todos os pacotes que estão instalados, enquanto `pip freeze` lista os pacotes instalados por `pip`e não listar os pacotes pip próprio depende. Você também pode usar `pip freeze` para gerar um arquivo de dependência.

## <a name="find-a-single-package"></a>Localizar um único pacote

Se você tiver instalado um pacote e deseja ter certeza de que ele esteja disponível para uma determinada instância do SQL Server, você pode executar a seguinte chamada de procedimento armazenado para carregar o pacote e retornar apenas as mensagens.

### <a name="r"></a>R

Este exemplo procura e carrega a biblioteca RevoScaleR, se disponível.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ Se o pacote for encontrado, uma mensagem será retornada: "Comandos concluída com êxito."

+ Se o pacote não pode ser localizado ou carregado, você receberá um erro que contém o texto: "não há nenhum pacote chamado 'MissingPackageName'"

### <a name="python"></a>Python

A verificação de equivalente do Python pode ser executada de Python de shell, usando `conda` ou `pip` comandos. Como alternativa, execute esta instrução em um procedimento armazenado:

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

## <a name="get-package-information-in-r-and-python-tools"></a>Obter informações de pacote nas ferramentas de R e Python

Todas as instruções anteriores presumem que você esteja usando uma ferramenta como o Management Studio (SSMS) do SQL Server. Se você preferir usar ferramentas de R e Python, as instruções a seguir explicam como obter informações de biblioteca e o pacote de uma linha de comando de R ou Python.

### <a name="r-commands"></a>Comandos de R

A biblioteca de instância para R é \Program Files\Microsoft Server\MSSQL14 SQL. MSSQLSERVER\R_SERVICES\library.

Inicie as ferramentas de R padrão desses locais para garantir que os pacotes da biblioteca de instância são usados:

+ \MSSQL14. MSSQLSERVER\R_SERVICES\bin\R.exe para um prompt de comando de R
+ \MSSQL14. MSSQLSERVER\R_SERVICES\bin\x64\Rgui.exe para um aplicativo de console de R

Você pode usar comandos padrão de R ou comandos de RevoScaleR para obter informações sobre o pacote. O pacote RevoScaleR é carregado automaticamente. 

Retorne informações sobre o pacote RevoScaleR:

    > print(Revo.version)

Retorne uma lista de todos os pacotes instalados:

    > installed.packages()

Retornar a versão do r:

    > packageDescription("base")

### <a name="python-commands"></a>Comandos de Python

Suporte de Python só é 2017 do SQL Server. A biblioteca de instância para Python é \Program Files\Microsoft Server\MSSQL14 SQL. MSSQLSERVER\PYTHON_SERVICES\.

Abra a janela de comando do Python deste local para garantir que os pacotes da biblioteca de instância são usados:

+ \MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Python.exe

Abrir a Ajuda interativa:

    > help()

Digite um nome de módulo no prompt de ajuda para obter o conteúdo do pacote, a versão e o local do arquivo:

    help> revoscalepy

<a name="pip-conda"></a>

### <a name="python-package-managers-pip-and-conda"></a>Pacote de Python gerenciadores (Pip e Conda)

Anaconda inclui ferramentas Python para o gerenciamento de pacotes. Em um padrão instância, Pip, Conda e outras ferramentas podem ser encontradas em \Program Files\Microsoft Server\MSSQL14 SQL. MSSQLSERVER\PYTHON_SERVICES\Scripts.

Instalação do SQL Server não adiciona Pip ou Conda ao caminho do sistema e em uma instância do SQL Server de produção, manter os executáveis não essenciais do caminho é uma prática recomendada. No entanto, para ambientes de desenvolvimento e teste, você pode adicionar a pasta de Scripts para a variável de ambiente do caminho de sistema para executar o Pip e Conda no comando de qualquer local.

1. Vá para C:\Program Files\Microsoft SQL Server\MSSQL14. MSSQLSERVER\PYTHON_SERVICES\Scripts

1. Clique com botão direito **conda.exe** > **executar como administrador**e digite `conda list` para retornar uma lista de pacotes instalados no ambiente atual.

1. Da mesma forma, clique com botão direito **pip.exe** > **executar como administrador**e digite `pip list` para retornar as mesmas informações. 


## <a name="next-steps"></a>Próximas etapas

+ [Instalar novos pacotes de R](install-additional-r-packages-on-sql-server.md)
+ [Instalar novos pacotes do Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Tutoriais, exemplos, soluções](../tutorials/machine-learning-services-tutorials.md)