---
title: Obter informações sobre o pacote do Python
description: Saiba como obter informações sobre os pacotes do Python instalados, incluindo versões e locais de instalação, nos Serviços de Machine Learning do SQL Server.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/01/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fb08940a9a6c9c15d8c633f5b3c439514bc43646
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83605948"
---
# <a name="get-python-package-information"></a>Obter informações sobre o pacote do Python

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve como obter informações sobre os pacotes do Python instalados, incluindo versões e locais de instalação, nos Serviços de Machine Learning do SQL Server. Os exemplos de scripts do Python mostram como listar informações de pacote, como o caminho e a versão de instalação.

## <a name="default-python-library-location"></a>Localização da biblioteca padrão do Python

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
Quando você instala o aprendizado de máquina com o SQL Server, uma única biblioteca de pacotes é criada no nível de instância para cada linguagem instalada. A biblioteca de instâncias é uma pasta protegida registrada no SQL Server.
::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"
Quando você instala o aprendizado de máquina com o SQL Server, uma única biblioteca de pacotes é criada no nível de instância para cada linguagem instalada.
::: moniker-end

Todo script ou código executado no banco de dados no SQL Server deve carregar funções da biblioteca de instâncias. O SQL Server não pode acessar pacotes instalados em outras bibliotecas. Isso se aplica a clientes remotos também: qualquer código do Python em execução no contexto de computação do servidor só pode usar pacotes instalados na biblioteca de instâncias.
Para proteger os ativos do servidor, a biblioteca de instâncias padrão pode ser modificada apenas por um administrador do computador.

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
O caminho padrão dos binários para Python é:

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

Isso pressupõe a instância SQL padrão, MSSQLSERVER. Se o SQL Server estiver instalado como uma instância nomeada definida pelo usuário, o nome fornecido será usado.
::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
O caminho padrão dos binários para Python é:

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`

Isso pressupõe a instância SQL padrão, MSSQLSERVER. Se o SQL Server estiver instalado como uma instância nomeada definida pelo usuário, o nome fornecido será usado.
::: moniker-end

Habilite scripts externos executando os seguintes comandos SQL:

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH override;
```

Execute a instrução a seguir para verificar a biblioteca padrão para a instância atual. Este exemplo retorna a lista de pastas incluídas na variável `sys.path` do Python. A lista inclui o diretório atual e o caminho da biblioteca padrão.

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

Para obter mais informações sobre a variável `sys.path` e como ela é usada para definir o caminho de pesquisa do interpretador para módulos, confira [O caminho de pesquisa do módulo](https://docs.python.org/2/tutorial/modules.html#the-module-search-path).

## <a name="default-microsoft-python-packages"></a>Pacotes do Python padrão da Microsoft

Os pacotes do Python da Microsoft a seguir são instalados com os Serviços de Machine Learning do SQL Server quando você seleciona o recurso do Python durante a instalação.

| Pacotes | Versão |  Descrição |
| ---------|---------|--------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.4.7 | Usada para contextos de computação remota, streaming, execução paralela de funções rx para importação e transformação de dados, modelagem, visualização e análise. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.4.7 | Adiciona algoritmos de aprendizado de máquina em Python. |

Confira mais informações sobre qual versão do Python está incluída nas [versões de Python e R](../sql-server-machine-learning-services.md#versions).

### <a name="component-upgrades"></a>Atualizações de componentes

Por padrão, os pacotes do Python são atualizados por meio de service packs e atualizações cumulativas. Pacotes adicionais e atualizações de versão completa dos principais componentes do Python são possíveis apenas por meio de atualizações de produto ou pela associação do suporte ao Python para Microsoft Machine Learning Server.

Para obter mais informações, confira [Atualizar componentes do R e do Python no SQL Server](../install/upgrade-r-and-python.md).

## <a name="default-open-source-python-packages"></a>Pacotes do Python de software livre padrão

Quando você seleciona a opção de linguagem do Python durante a instalação, a distribuição do Anaconda 4.2 (no Python 3.5) é instalada. Além das bibliotecas de códigos do Python, a instalação padrão inclui dados de exemplo, testes de unidade e scripts de exemplo.

> [!IMPORTANT]
> Você nunca deve substituir manualmente a versão do Python instalada pelo SQL Server por versões mais recentes na Web. Os pacotes do Python da Microsoft são baseados em versões específicas do Anaconda. Modificar sua instalação pode desestabilizá-la.

## <a name="list-all-installed-python-packages"></a>Listar todos os pacotes do Python instalados

O script de exemplo a seguir exibe uma lista de todos os pacotes do Python instalados na instância do SQL Server.

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
import pkg_resources
import pandas as pd
installed_packages = pkg_resources.working_set
installed_packages_list = sorted(["%s==%s" % (i.key, i.version) for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

## <a name="find-a-single-python-package"></a>Localizar um único pacote do Python

Se você tiver instalado um pacote do Python e desejar garantir que ele esteja disponível para uma instância específica do SQL Server, poderá executar um procedimento armazenado para procurar o pacote e retornar as mensagens.

Por exemplo, o código a seguir procura o pacote `scikit-learn`.
Se o pacote for encontrado, o código imprimirá a versão do pacote.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pkg_name = "pandas"
try:
    version = pkg_resources.get_distribution(pkg_name).version
    print("Package " + pkg_name + " is version " + version)
except:
    print("Package " + pkg_name + " not found")
'
```

Resultado:

```text
STDOUT message(s) from external script: Package pandas is version 0.23.4
```

O exemplo a seguir imprime a versão do pacote `pandas`.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pkg_name = "pandas"
print(pkg_name + " package is version " + pkg_resources.get_distribution(pkg_name).version)
'
```

O exemplo a seguir retorna a versão do Python.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import sys
print(sys.version)
'
```

## <a name="next-steps"></a>Próximas etapas

::: moniker range="<=sql-server-2017||=sqlallproducts-allversions"
+ [Instalar pacotes com ferramentas do Python](install-python-packages-standard-tools.md)
::: moniker-end
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
+ [Instalar novos pacotes de Python com sqlmlutils](install-additional-r-packages-on-sql-server.md)
::: moniker-end