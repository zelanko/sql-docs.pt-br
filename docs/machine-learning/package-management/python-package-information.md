---
title: Obter informações sobre o pacote do Python
description: Saiba como obter informações sobre os pacotes do Python instalados, incluindo versões e locais de instalação, nos Serviços de Machine Learning do SQL Server.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/03/2020
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 9bb55bf9bac934f78b0a309663ced729a8ef6534
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869744"
---
# <a name="get-python-package-information"></a>Obter informações sobre o pacote do Python

[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Este artigo descreve como obter informações sobre os pacotes do Python instalados, incluindo versões e locais de instalação, nos [Serviços de Machine Learning no SQL Server](../sql-server-machine-learning-services.md) e em [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md). Os exemplos de scripts do Python mostram como listar informações de pacote, como o caminho e a versão de instalação.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Este artigo descreve como obter informações sobre os pacotes do Python instalados, incluindo versões e locais de instalação, nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md). Os exemplos de scripts do Python mostram como listar informações de pacote, como o caminho e a versão de instalação.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Este artigo descreve como obter informações sobre os pacotes do Python instalados, incluindo versões e locais de instalação, nos [Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview). Os exemplos de scripts do Python mostram como listar informações de pacote, como o caminho e a versão de instalação.
::: moniker-end

## <a name="default-python-library-location"></a>Localização da biblioteca padrão do Python

Quando você instala o aprendizado de máquina com o SQL Server, uma única biblioteca de pacotes é criada no nível de instância para cada linguagem instalada. A biblioteca de instâncias é uma pasta protegida registrada no SQL Server.

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

::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
> [!IMPORTANT]
> Na Instância Gerenciada de SQL do Azure, a execução dos comandos sp_configure e RECONFIGURE dispara uma reinicialização do SQL Server para que as configurações de RG entrem em vigor. Isso pode causar indisponibilidade por alguns segundos.
::: moniker-end

Execute a instrução SQL a seguir para verificar a biblioteca padrão para a instância atual. Este exemplo retorna a lista de pastas incluídas na variável `sys.path` do Python. A lista inclui o diretório atual e o caminho da biblioteca padrão.

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

Para obter mais informações sobre a variável `sys.path` e como ela é usada para definir o caminho de pesquisa do interpretador para módulos, confira [O caminho de pesquisa do módulo](https://docs.python.org/2/tutorial/modules.html#the-module-search-path).

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
> [!NOTE]
> Não tente instalar pacotes do Python diretamente na biblioteca de pacotes do SQL usando **pip** ou métodos semelhantes. Em vez disso, use **sqlmlutils** para instalar pacotes em uma instância SQL. Para obter mais informações, confira [Instalar pacotes do Python com o sqlmlutils](install-additional-python-packages-on-sql-server.md).
::: moniker-end

## <a name="default-microsoft-python-packages"></a>Pacotes do Python padrão da Microsoft

Os pacotes do Python da Microsoft a seguir são instalados com os Serviços de Machine Learning do SQL Server quando você seleciona o recurso do Python durante a instalação.

| Pacotes | Versão |  Descrição |
| ---------|---------|--------------|
| [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.4.7 | Usada para contextos de computação remota, streaming, execução paralela de funções rx para importação e transformação de dados, modelagem, visualização e análise. |
| [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.4.7 | Adiciona algoritmos de aprendizado de máquina em Python. |

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
import pandas
OutputDataSet = pandas.DataFrame(sorted([(i.key, i.version) for i in pkg_resources.working_set]))'
WITH result sets((Package NVARCHAR(128), Version NVARCHAR(128)));
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
pkg_name = "scikit-learn"
try:
    version = pkg_resources.get_distribution(pkg_name).version
    print("Package " + pkg_name + " is version " + version)
except:
    print("Package " + pkg_name + " not found")
'
```

Resultado:

```text
STDOUT message(s) from external script: Package scikit-learn is version 0.20.2
```

<a name="bkmk_SQLPythonVersion"></a>
## <a name="view-the-version-of-python"></a>Exibir a versão do Python

O código de exemplo a seguir retorna a versão do Python instalada na instância do SQL Server.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import sys
print(sys.version)
'
```

## <a name="next-steps"></a>Próximas etapas

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
+ [Instalar pacotes com ferramentas do Python](install-python-packages-standard-tools.md)
::: moniker-end
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
+ [Instalar novos pacotes de Python com sqlmlutils](install-additional-r-packages-on-sql-server.md)
::: moniker-end