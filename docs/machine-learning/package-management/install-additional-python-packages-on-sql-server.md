---
title: Instalar pacotes de Python com sqlmlutils
description: Saiba como usar o Python pip para instalar novos pacotes de Python em uma instância dos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/26/2020
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 229b0843fc8602457328921eaa6ff8991f4b5655
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956707"
---
# <a name="install-python-packages-with-sqlmlutils"></a>Instalar pacotes de Python com sqlmlutils

[!INCLUDE [SQL Server 2019 SQL MI](../../includes/applies-to-version/sqlserver2019-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Este artigo descreve como usar funções no pacote [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) para instalar novos pacotes do Python em uma instância dos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) e em [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md). Os pacotes que você instalar poderão ser usados em scripts de Python em execução no banco de dados usando a instrução T-SQL [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
::: moniker-end

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Este artigo descreve como usar funções no pacote [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) para instalar novos pacotes do Python em uma instância dos [Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview). Os pacotes que você instalar poderão ser usados em scripts de Python em execução no banco de dados usando a instrução T-SQL [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
::: moniker-end

Para obter mais informações sobre a localização e os caminhos de instalação do pacote, confira [Obter informações do pacote de Python](../package-management/python-package-information.md).

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
> [!NOTE]
> O pacote **sqlmlutils** descrito neste artigo é usado para adicionar pacotes do Python ao SQL Server 2019 ou posterior. Para o SQL Server 2017 e anterior, consulte [Instalar pacotes com ferramentas do Python](./install-python-packages-standard-tools.md?view=sql-server-2017).
::: moniker-end

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
+ Você precisa ter os [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md) instalados com a opção de linguagem do Python.
::: moniker-end

+ Instale o [Azure Data Studio](../../azure-data-studio/what-is.md) no computador cliente que você usa para se conectar ao SQL Server. Você pode usar outras ferramentas de consulta ou gerenciamento de banco de dados, mas este artigo pressupõe o uso do Azure Data Studio.

+ Instale o kernel do Python no Azure Data Studio. Instale e use o Python na linha de comando. O ideal é usar um ambiente de desenvolvimento do Python, como o [Visual Studio Code](https://code.visualstudio.com/download) com a [Extensão do Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python).

### <a name="other-considerations"></a>Outras considerações

+ Os pacotes precisam estar em conformidade com a versão existente do Python, e a versão do Python no servidor precisa corresponder à versão do Python no computador cliente. Para saber mais sobre qual versão do Python está incluída em cada versão do SQL Server, confira as [versões Python e R](../sql-server-machine-learning-services.md#versions). Para confirmar a versão do Python em uma instância SQL específica, confira [Exibir a versão do Python](python-package-information.md#bkmk_SQLPythonVersion).

+ A biblioteca de pacotes de Python está localizada na pasta Arquivos de Programas de sua instância do SQL Server e, por padrão, a instalação nessa pasta requer permissões de administrador. Para obter mais informações, confira [Localização da biblioteca de pacotes](../package-management/python-package-information.md#default-python-library-location).

+ A instalação do pacote é específica da instância SQL, do banco de dados e dos usuários indicados por você nas informações de conexão fornecidas para **sqlmlutils**. Se quiser usar o pacote em várias instâncias ou bancos de dados SQL ou para diferentes usuários, você precisará instalá-lo para cada um. Com uma exceção: se o pacote for instalado por um membro de `dbo`, ele será *público* e compartilhado com todos os usuários. Se um usuário instalar uma versão mais recente de um pacote público, este não será afetado, mas o usuário terá acesso à versão mais recente.

+ Antes de adicionar um pacote, considere se ele é uma boa opção para o ambiente do SQL Server.

  + Recomendamos que você use o Python no banco de dados para tarefas que se beneficiam da forte integração com o mecanismo de banco de dados, como o aprendizado de máquina, em vez de tarefas que simplesmente consultam o banco de dados.

  + Se você adicionar pacotes que colocam muita pressão computacional sobre o servidor, o desempenho será prejudicado.

  + Em um ambiente do SQL Server protegido, talvez você queira evitar o seguinte:
    + Pacotes que exigem acesso à rede
    + Pacotes que exigem acesso elevado ao sistema de arquivos
    + Pacotes usados para desenvolvimento Web ou outras tarefas que não se beneficiam da execução dentro do SQL Server

  + O pacote **tensorflow** do Python não pode ser instalado por meio do sqlmlutils. Para obter mais informações e uma solução alternativa, confira [Problemas conhecidos nos Serviços de Machine Learning do SQL Server](../troubleshooting/known-issues-for-sql-server-machine-learning-services.md#9-cannot-install-tensorflow-package-using-sqlmlutils).

## <a name="install-sqlmlutils-on-the-client-computer"></a>Instalar sqlmlutils no computador cliente

Para usar **sqlmlutils**, primeiro você precisa instalá-lo no computador cliente que usa para se conectar ao SQL Server.

### <a name="in-azure-data-studio"></a>No Azure Data Studio

Se você estiver usando **sqlmlutils** no Azure Data Studio, instale-o usando o recurso Gerenciar Pacotes em um notebook do kernel do Python.

1. Em um [notebook do kernel do Python no Azure Data Studio](../../azure-data-studio/notebooks/notebooks-python-kernel.md), clique em **Gerenciar Pacotes**.
1. Clique em **Adicionar nova**.
1. Insira "sqlmlutils" no campo **Pesquisar pacotes Pip** e clique em **Pesquisar**.
1. Selecione a **Versão do Pacote** que deseja instalar (a última versão é recomendada).
1. Clique em **Instalar** e em **Fechar**.

### <a name="from-python-command-line"></a>Na linha de comando do Python

Se você estiver usando o **sqlmlutils** em um IDE ou um prompt de comando do Python, instale o sqlmlutils com um comando **pip** simples:

```console
pip install sqlmlutils
```

Instale também o **sqlmlutils** por meio de um arquivo zip:

1. Verifique se o **Pip** está instalado. Confira [Instalação do Pip](https://pip.pypa.io/en/stable/installing/) para obter mais informações.
1. Baixe o arquivo zip mais recente do **sqlmlutils** do https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist para o computador cliente. Não descompacte o arquivo.
1. Abra um **Prompt de Comando** e execute os comandos a seguir para instalar o pacote do **sqlmlutils**. Substitua o caminho completo para o arquivo zip do **sqlmlutils** que você baixou – este exemplo supõe que o arquivo baixado seja `c:\temp\sqlmlutils-1.0.0.zip`.
   ```console
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils-1.0.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>Adicionar um pacote de Python ao SQL Server

Usando o **sqlmlutils**, você pode adicionar pacotes do Python a uma instância SQL. Depois, você poderá usar esses pacotes no código Python em execução na instância SQL. O **sqlmlutils** usa [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md) para instalar o pacote e cada uma de suas dependências.

No exemplo a seguir, você adicionará o pacote [text-tools](https://pypi.org/project/text-tools/) ao SQL Server.

### <a name="add-the-package-online"></a>Adicionar o pacote online

Se o computador cliente que você usa para se conectar ao SQL Server tiver acesso à Internet, você poderá usar **sqlmlutils** para localizar o pacote **text-tools** e qualquer dependência pela Internet e, em seguida, instalar o pacote em uma instância do SQL Server remotamente.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

1. No computador cliente, abra o **Python** ou um ambiente de Python.

1. Use os comandos a seguir para instalar o pacote **text-tools**. Substitua suas informações de conexão de banco de dados SQL Server (se você usar a autenticação do Windows, não precisará dos parâmetros `uid` e `pwd`).

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"

1. No computador cliente, abra o **Python** ou um ambiente de Python.

1. Use os comandos a seguir para instalar o pacote **text-tools**. Substitua suas informações de conexão de banco de dados do SQL Server.

::: moniker-end

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="server", database="database", uid="username", pwd="password")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>Adicionar o pacote offline

Se o computador cliente que você usa para se conectar ao SQL Server não tiver uma conexão com a Internet, você poderá usar o **pip** em um computador com acesso à Internet para baixar o pacote e qualquer pacote dependente em uma pasta local. Em seguida, copie a pasta para o computador cliente onde você pode instalar o pacote offline.

#### <a name="on-a-computer-with-internet-access"></a>Em um computador com acesso à Internet

1. Abra um **Prompt de Comando** e execute o comando a seguir para criar uma pasta local que contenha o pacote **text-tools**. Este exemplo cria a pasta `c:\temp\text-tools`.

   ```console
   pip download text-tools -d c:\temp\text-tools
   ```

1. Copie a pasta `text-tools` para o computador cliente. O exemplo a seguir pressupõe que você a copiou para `c:\temp\packages\text-tools`.

#### <a name="on-the-client-computer"></a>No computador cliente

Use **sqlmlutils** para instalar cada pacote (arquivo WHL) encontrado na pasta local que o **pip** criou. A ordem em que os pacotes são instalados não é importante.

Neste exemplo, **text-tools** não tem dependências, portanto, há apenas um arquivo da pasta `text-tools` para instalação. Por outro lado, um pacote como **scikit-plot** tem 11 dependências, de modo que você encontraria 12 arquivos na pasta (o pacote **scikit-plot** e os 11 pacotes dependentes) e instalaria cada um deles.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

Execute o script Python a seguir. Substitua o caminho do arquivo real e o nome do pacote, bem como suas informações de conexão de banco de dados SQL Server (se você usar a autenticação do Windows, não precisará dos parâmetros `uid` e `pwd`). Repita a instrução `sqlmlutils.SQLPackageManager` para cada arquivo de pacote na pasta.

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

Execute o script Python a seguir. Substitua o caminho de arquivo real e o nome do pacote, bem como suas informações de conexão de Banco de Dados do SQL Server. Repita a instrução `sqlmlutils.SQLPackageManager` para cada arquivo de pacote na pasta.

::: moniker-end

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="username", pwd="password"))
sqlmlutils.SQLPackageManager(connection).install("text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package"></a>Usar o pacote

Agora, você pode usar o pacote em um script de Python no SQL Server. Por exemplo:

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
from text_tools.finders import find_best_string
corpus = "Lorem Ipsum text"
query = "Ipsum"
first_match = find_best_string(query, corpus)
print(first_match)
  '
```

## <a name="remove-the-package-from-sql-server"></a>Remover o pacote do SQL Server

Se quiser remover o pacote **text-tools**, use o comando de Python a seguir no computador cliente, usando a mesma variável de conexão definida anteriormente.

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="next-steps"></a>Próximas etapas

+ Para saber mais sobre os pacotes do Python instalados nos Serviços de Machine Learning do SQL Server, confira [Obter informações sobre o pacote do Python](../package-management/python-package-information.md).

+ Para obter informações sobre como instalar pacotes de R nos Serviços de Machine Learning do SQL Server, confira [Instalar novos pacotes de R no SQL Server](install-additional-r-packages-on-sql-server.md).