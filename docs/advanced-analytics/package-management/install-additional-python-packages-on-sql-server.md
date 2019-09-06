---
title: Instalar pacotes do Python com Pip
description: Saiba como usar o Pip do Python para instalar novos pacotes do Python em uma instância do SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 90bc0d33b00f77f942dd736ff1e1904f5d2e7396
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2019
ms.locfileid: "70276459"
---
# <a name="install-python-packages-with-sqlmlutils"></a>Instalar pacotes do Python com o sqlmlutils

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como usar funções no pacote [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) para instalar novos pacotes do Python em uma instância do SQL Server serviços de Machine Learning. Os pacotes que você instala podem ser usados em scripts Python em execução no banco de dados usando a instrução T-SQL [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) .

Para obter mais informações sobre o local do pacote e caminhos de instalação, consulte [obter informações do pacote do Python](../package-management/python-package-information.md).

> [!NOTE]
> O comando Python `pip install` padrão não é recomendado para adicionar pacotes do Python em SQL Server. Em vez disso, use **sqlmlutils** conforme descrito neste artigo.

## <a name="prerequisites"></a>Pré-requisitos

+ Você deve ter [SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) instalado com a opção linguagem Python.

+ Instale o [Python](https://www.python.org/) no computador cliente que você usa para se conectar ao SQL Server. Você também pode querer um ambiente de desenvolvimento do Python, como [Visual Studio Code](https://code.visualstudio.com/download) com a [extensão do Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python). 

+ Instale o [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) ou o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS) no computador cliente que você usa para se conectar ao SQL Server. Você pode usar outras ferramentas de consulta e gerenciamento de banco de dados, mas este artigo pressupõe Azure Data Studio ou SSMS.

### <a name="other-considerations"></a>Outras considerações

+ Os pacotes devem ser compatíveis com Python 3,5 e ser executados no Windows.

+ A biblioteca de pacotes do Python está localizada na pasta arquivos de programas da sua SQL Server instância e, por padrão, a instalação nessa pasta requer permissões de administrador. Para obter mais informações, consulte [local da biblioteca de pacotes](../package-management/python-package-information.md#default-python-library-location).

+ A instalação do pacote é por instância. Se você tiver várias instâncias do Serviços de Machine Learning, deverá adicionar o pacote a cada uma delas.

+ Antes de adicionar um pacote, considere se o pacote é uma boa opção para o ambiente de SQL Server.

  + Recomendamos que você use o Python no banco de dados para tarefas que se beneficiam da forte integração com o mecanismo de banco de dados, como o Machine Learning, em vez de tarefas que simplesmente consultam o banco de dados.

  + Se você adicionar pacotes que colocam muita pressão computacional no servidor, o desempenho será prejudicado.

  + Em um ambiente de SQL Server protegido, talvez você queira evitar o seguinte:
    + Pacotes que exigem acesso à rede
    + Pacotes que exigem acesso elevado ao sistema de arquivos
    + Pacotes usados para desenvolvimento na Web ou outras tarefas que não se beneficiam com a execução dentro de SQL Server

## <a name="install-sqlmlutils-on-the-client-computer"></a>Instalar o sqlmlutils no computador cliente

Para usar o **sqlmlutils**, primeiro você precisa instalá-lo no computador cliente que você usa para se conectar ao SQL Server.

1. Baixe o arquivo zip **sqlmlutils** mais recente https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist do no computador cliente. Não Descompacte o arquivo.

1. Abra um **prompt de comando** e execute o comando a seguir para instalar o pacote **sqlmlutils** . Substitua o caminho completo para o arquivo zip **sqlmlutils** que você baixou-este exemplo supõe que o `c:\temp\sqlmlutils_0.6.0.zip`arquivo baixado é.

   ```console
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils_0.6.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>Adicionar um pacote do Python no SQL Server

No exemplo a seguir, você adicionará o pacote de [ferramentas de texto](https://pypi.org/project/text-tools/) a SQL Server.

### <a name="add-the-package-online"></a>Adicionar o pacote online

Se o computador cliente que você usa para se conectar ao SQL Server tiver acesso à Internet, você poderá usar o **sqlmlutils** para localizar o pacote de **ferramentas de texto** e quaisquer dependências pela Internet e, em seguida, instalar o pacote em uma instância de SQL Server remotamente.

1. No computador cliente, abra o **Python** ou um ambiente Python.

1. Use os comandos a seguir para instalar o pacote de **ferramentas de texto** . Substitua suas próprias informações de conexão de banco de dados SQL Server.

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>Adicionar o pacote offline

Se o computador cliente que você usa para se conectar ao SQL Server não tiver uma conexão com a Internet, você poderá usar o **Pip** em um computador com acesso à Internet para baixar o pacote e todos os pacotes dependentes para uma pasta local. Em seguida, copie a pasta para o computador cliente onde você pode instalar o pacote offline.

#### <a name="on-a-computer-with-internet-access"></a>Em um computador com acesso à Internet

1. Abra um **prompt de comando** e execute o comando a seguir para criar uma pasta local que contém o pacote de **ferramentas de texto** . Este exemplo cria a pasta `c:\temp\text-tools`.

   ```console
   pip download text-tools -d c:\temp\text-tools
   ```

1. Copie a `text-tools` pasta no computador cliente. O exemplo a seguir pressupõe que você o `c:\temp\packages\text-tools`copiou para.

#### <a name="on-the-client-computer"></a>No computador cliente

Use **sqlmlutils** para instalar cada pacote (arquivo WHL) encontrado na pasta local que o **Pip** criou. Não importa em que ordem os pacotes são instalados.

Neste exemplo, **Text-Tools** não tem dependências, portanto, há apenas um arquivo da `text-tools` pasta a ser instalada. Por outro lado, um pacote como **scikit** tem 11 dependências, portanto, você encontraria 12 arquivos na pasta (o pacote **scikit** e os 11 pacotes dependentes) e instalaria cada um deles.

Execute o script Python a seguir. Substitua suas próprias informações de conexão de banco de dados SQL Server e o caminho de arquivo real e o nome do pacote. Repita a `sqlmlutils.SQLPackageManager` instrução para cada arquivo de pacote na pasta.

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
sqlmlutils.SQLPackageManager(connection).install("c:/temp/packages/text-tools/text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package-in-sql-server"></a>Usar o pacote no SQL Server

Agora você pode usar o pacote em um script Python no SQL Server. Por exemplo:

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

## <a name="remove-the-package-from-sql-server"></a>Remover o pacote de SQL Server

Se você quiser remover o pacote de **ferramentas de texto** , use o comando do Python a seguir no computador cliente, usando a mesma variável de conexão definida anteriormente.

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="see-also"></a>Confira também

+ Para exibir informações sobre os pacotes do Python instalados no SQL Server Serviços de Machine Learning, consulte [obter informações do pacote do Python](../package-management/python-package-information.md).

+ Para obter informações sobre como instalar pacotes R no SQL Server Serviços de Machine Learning, consulte [instalar novos pacotes de r no SQL Server](../r/install-additional-r-packages-on-sql-server.md).
