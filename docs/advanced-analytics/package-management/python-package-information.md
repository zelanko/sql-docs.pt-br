---
title: Obter informações do pacote do Python
description: Saiba como obter informações sobre os pacotes python instalados, incluindo versões e locais de instalação, em SQL Server Serviços de Machine Learning.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bccfc97fe75a718ce76ea0d1292bfc7ea6cb6564
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641173"
---
# <a name="get-python-package-information"></a>Obter informações do pacote do Python

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como obter informações sobre os pacotes python instalados, incluindo versões e locais de instalação, em SQL Server Serviços de Machine Learning. Scripts Python de exemplo mostram como listar informações do pacote, como o caminho de instalação e a versão.

## <a name="default-python-library-location"></a>Local da Biblioteca Python padrão

Quando você instala o Machine Learning com o SQL Server, uma única biblioteca de pacote é criada no nível da instância para cada idioma que você instalar. No Windows, a biblioteca de instâncias é uma pasta segura registrada com SQL Server.

Todo script ou código executado no banco de dados no SQL Server deve carregar funções da biblioteca de instâncias. SQL Server não pode acessar pacotes instalados em outras bibliotecas. Isso também se aplica a clientes remotos: qualquer código Python em execução no contexto de computação do servidor só pode usar pacotes instalados na biblioteca de instâncias.
Para proteger ativos de servidor, a biblioteca de instância padrão pode ser modificada somente por um administrador de computador.

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
O caminho padrão dos binários para Python é:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
O caminho padrão dos binários para Python é:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

Isso pressupõe a instância SQL padrão, MSSQLSERVER. Se SQL Server for instalado como uma instância nomeada definida pelo usuário, o nome fornecido será usado em seu lugar.

Execute a instrução a seguir para verificar a biblioteca padrão da instância atual. Este exemplo retorna a lista de pastas incluídas na variável do `sys.path` Python. A lista inclui o diretório atual e o caminho da biblioteca padrão.

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

Para obter mais informações sobre a `sys.path` variável e como ela é usada para definir o caminho de pesquisa do intérprete para os módulos, consulte [o caminho de pesquisa do módulo](https://docs.python.org/2/tutorial/modules.html#the-module-search-path).

## <a name="default-python-packages"></a>Pacotes python padrão

Os seguintes pacotes do Python são instalados com SQL Server Serviços de Machine Learning quando você seleciona o recurso Python durante a instalação.

| Packages | Versão |  Descrição |
| ---------|---------|--------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9,2 | Usado para contextos de computação remota, streaming, execução paralela de funções RX para importação e transformação de dados, modelagem, visualização e análise. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9,2 | Adiciona algoritmos de aprendizado de máquina em Python. |

### <a name="component-upgrades"></a>Atualizações de componentes

Por padrão, os pacotes do Python são atualizados por meio de Service Packs e atualizações cumulativas. Pacotes adicionais e atualizações de versão completa dos principais componentes do Python são possíveis apenas por meio de atualizações de produto ou ligando o suporte do Python ao Microsoft Machine Learning Server.

Para obter mais informações, consulte [upgrade R and Python Components in SQL Server](../install/upgrade-r-and-python.md).

## <a name="default-open-source-python-packages"></a>Pacotes python de código-fonte aberto padrão

Quando você seleciona a opção idioma do Python durante a instalação, a distribuição do Anaconda 4,2 (sobre o Python 3,5) é instalada. Além das bibliotecas de código do Python, a instalação padrão inclui dados de exemplo, testes de unidade e scripts de exemplo.

> [!IMPORTANT]
> Você nunca deve substituir manualmente a versão do Python instalada pelo SQL Server instalação com versões mais recentes na Web. Os pacotes python da Microsoft são baseados em versões específicas do Anaconda. Modificar sua instalação pode desestabilizar.

## <a name="list-all-installed-python-packages"></a>Listar todos os pacotes python instalados

O `pip` módulo é instalado por padrão e oferece suporte a muitas operações para listar pacotes instalados, além daqueles com suporte do Python padrão. Você pode executar `pip` a partir de um prompt de comando do Python, mas também pode chamar algumas `sp_execute_external_script`funções PIP do.

O script de exemplo a seguir exibe uma lista de pacotes instalados e suas versões.

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
OutputDataSet = df
  '
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

## <a name="find-a-single-python-package"></a>Localizar um único pacote do Python

Se você instalou um pacote do Python e deseja garantir que ele esteja disponível para uma instância específica do SQL Server, você pode executar um procedimento armazenado para carregar o pacote e retornar as mensagens.

Por exemplo, o código a seguir procura o `scikit-learn` pacote.
Se o pacote for encontrado, o código retornará a mensagem "o pacote scikit-Learn está instalado".

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pip
import pkg_resources
pckg_name = "scikit-learn"
pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")
  '
```

<a name="get-package-vers"></a>

O exemplo a seguir retorna as versões do pacote revoscalepy e do Python.

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

+ [Instalar os novos pacotes Python](../python/install-additional-python-packages-on-sql-server.md)
+ [Obter informações do pacote do R](r-package-information.md)
+ [Instalar os novos pacotes R](../r/install-additional-r-packages-on-sql-server.md)
+ [Tutoriais de R e Python](../tutorials/machine-learning-services-tutorials.md)
