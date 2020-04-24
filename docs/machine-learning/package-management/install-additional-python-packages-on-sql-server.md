---
title: Instalar pacotes de Python com sqlmlutils
description: Saiba como usar o Python pip para instalar novos pacotes de Python em uma instância dos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/30/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4e72ded2e2f2a51805403132c662bff3d70c97ce
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487099"
---
# <a name="install-python-packages-with-sqlmlutils"></a>Instalar pacotes de Python com sqlmlutils

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como usar funções no pacote [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) para instalar novos pacotes de Python em uma instância dos Serviços de Machine Learning do SQL Server. Os pacotes que você instalar poderão ser usados em scripts de Python em execução no banco de dados usando a instrução T-SQL [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql).

Para obter mais informações sobre a localização e os caminhos de instalação do pacote, confira [Obter informações do pacote de Python](../package-management/python-package-information.md).

> [!NOTE]
> O comando de Python padrão `pip install` não é recomendado para adicionar pacotes de Python do SQL Server 2019. Em vez disso, use **sqlmlutils**, conforme descrito neste artigo.

## <a name="prerequisites"></a>Pré-requisitos

+ Você precisa ter os [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md) instalados com a opção de linguagem do Python.

+ Instale o [Python](https://www.python.org/) no computador cliente que você usa para se conectar ao SQL Server. Você também pode querer um ambiente de desenvolvimento de Python, como o [Visual Studio Code](https://code.visualstudio.com/download) com a [extensão de Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python). 

+ Instale o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) ou o [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) no computador cliente que você usa para se conectar ao SQL Server. Você pode usar outras ferramentas de consulta ou gerenciamento de banco de dados, mas este artigo pressupõe o Azure Data Studio ou o SSMS.

### <a name="other-considerations"></a>Outras considerações

+ Os pacotes devem estar em conformidade com a sua versão do Python. Para obter mais informações sobre qual versão do Python está incluída em cada versão do SQL Server, confira as [versões Python e R em O que são os Serviços de Machine Learning do SQL Server (Python e R)?](../sql-server-machine-learning-services.md#versions)

+ A biblioteca de pacotes de Python está localizada na pasta Arquivos de Programas de sua instância do SQL Server e, por padrão, a instalação nessa pasta requer permissões de administrador. Para obter mais informações, confira [Localização da biblioteca de pacotes](../package-management/python-package-information.md#default-python-library-location).

+ A instalação do pacote é feita por instância. Se tiver várias instâncias do Serviços de Machine Learning, você deverá adicionar o pacote a cada uma delas.

+ Antes de adicionar um pacote, considere se ele é uma boa opção para o ambiente do SQL Server.

  + Recomendamos que você use o Python no banco de dados para tarefas que se beneficiam da forte integração com o mecanismo de banco de dados, como o aprendizado de máquina, em vez de tarefas que simplesmente consultam o banco de dados.

  + Se você adicionar pacotes que colocam muita pressão computacional sobre o servidor, o desempenho será prejudicado.

  + Em um ambiente do SQL Server protegido, talvez você queira evitar o seguinte:
    + Pacotes que exigem acesso à rede
    + Pacotes que exigem acesso elevado ao sistema de arquivos
    + Pacotes usados para desenvolvimento Web ou outras tarefas que não se beneficiam da execução dentro do SQL Server

## <a name="install-sqlmlutils-on-the-client-computer"></a>Instalar sqlmlutils no computador cliente

Para usar **sqlmlutils**, primeiro você precisa instalá-lo no computador cliente que usa para se conectar ao SQL Server. Verifique se você tem `pip` instalado, confira a [instalação de pip](https://pip.pypa.io/en/stable/installing/) para obter mais informações.

1. Baixe o arquivo zip mais recente do **sqlmlutils** do https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist para o computador cliente. Não descompacte o arquivo.

1. Abra um **Prompt de Comando** e execute os comandos a seguir para instalar o pacote do **sqlmlutils**. Substitua o caminho completo para o arquivo zip do **sqlmlutils** que você baixou – este exemplo supõe que o arquivo baixado seja `c:\temp\sqlmlutils-1.0.0.zip`.

   ```console
   pip install "pymssql<3.0"
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils-1.0.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>Adicionar um pacote de Python ao SQL Server

No exemplo a seguir, você adicionará o pacote [text-tools](https://pypi.org/project/text-tools/) ao SQL Server.

### <a name="add-the-package-online"></a>Adicionar o pacote online

Se o computador cliente que você usa para se conectar ao SQL Server tiver acesso à Internet, você poderá usar **sqlmlutils** para localizar o pacote **text-tools** e qualquer dependência pela Internet e, em seguida, instalar o pacote em uma instância do SQL Server remotamente.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

1. No computador cliente, abra o **Python** ou um ambiente de Python.

1. Use os comandos a seguir para instalar o pacote **text-tools**. Substitua suas informações de conexão de banco de dados SQL Server (se você usar a autenticação do Windows, não precisará dos parâmetros `uid` e `pwd`).

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

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

## <a name="use-the-package-in-sql-server"></a>Usar o pacote no SQL Server

Agora, você pode usar o pacote em um script de Python no SQL Server. Por exemplo:

```python
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

## <a name="see-also"></a>Confira também

+ Para exibir informações sobre os pacotes de Python instalados nos Serviços de Machine Learning do SQL Server, confira [Obter informações sobre o pacote de Python](../package-management/python-package-information.md).

+ Para obter informações sobre como instalar pacotes de R nos Serviços de Machine Learning do SQL Server, confira [Instalar novos pacotes de R no SQL Server](install-additional-r-packages-on-sql-server.md).
