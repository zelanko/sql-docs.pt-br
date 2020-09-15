---
title: Extensão da linguagem Python
description: Saiba mais sobre a extensão do Python para executar scripts de Python externos com os Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9263d11f271249d7fa31b1a3f3af83a21c04c793
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88173289"
---
# <a name="python-language-extension-in-sql-server-machine-learning-services"></a>Extensão da linguagem Python nos Serviços de Machine Learning do SQL Server
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

Este artigo descreve a extensão do Python para executar scripts de Python externos com os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md). A extensão adiciona:

- Um ambiente de execução de Python
- Uma distribuição do Anaconda com o runtime e o interpretador do Python 3.5
- Bibliotecas e ferramentas padrão
- Pacotes de Python da Microsoft:
  - [revoscalepy](../python/ref-py-revoscalepy.md) para análise em escala.
  - [microsoftml](../python/ref-py-microsoftml.md) para algoritmos de machine learning.

A instalação do interpretador e do runtime do Python 3.5 garante a compatibilidade quase completa com soluções Python padrão. O Python é executado em um processo separado do SQL Server, a fim de garantir que as operações de banco de dados não sejam comprometidas.

## <a name="python-components"></a>Componentes do Python

O SQL Server inclui pacotes de software livre e proprietários. O runtime do Python instalado pela instalação é Anaconda 4.2 com Python 3.5. O runtime do Python é instalado independentemente das ferramentas SQL e é executado fora dos processos do mecanismo principal, na estrutura de extensibilidade. Como parte da instalação dos Serviços de Machine Learning com o Python, você deve consentir com os termos da Licença Pública de GNU. 

O SQL Server não modifica os executáveis do Python, mas você deve usar a versão do Python instalada pela instalação, pois essa versão é aquela na qual os pacotes proprietários são compilados e testados. Para obter uma lista de pacotes compatíveis com a distribuição do Anaconda, confira o site de Análise de continuidade: [Lista de pacotes do Anaconda](https://docs.continuum.io/anaconda/packages/pkg-docs).

A distribuição do Anaconda associada a uma determinada instância do mecanismo de banco de dados pode ser encontrada na pasta associada à instância. Por exemplo, se você tiver instalado o mecanismo de banco de dados do SQL Server 2017 com os Serviços de Machine Learning e o Python na instância padrão, procure em `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`.

Os pacotes do Python adicionados pela Microsoft para cargas de trabalho paralelas e distribuídas incluem as bibliotecas a seguir.

| Biblioteca | Descrição |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | É compatível com objetos de fonte de dados e exploração, manipulação, transformação e visualização de dados. Ele é compatível com a criação de contextos de computação remota, bem como com vários modelos de machine learning escalonáveis, como **rxLinMod**. Para obter mais informações, confira o [módulo revoscalepy com o SQL Server](../python/ref-py-revoscalepy.md).  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Contém algoritmos de aprendizado de máquina que foram otimizados para velocidade e precisão, bem como transformações em linha para trabalhar com texto e imagens. Para obter mais informações, confira o [módulo microsoftml com o SQL Server](../python/ref-py-microsoftml.md). |

Microsoftml e revoscalepy estão rigidamente acoplados; as fontes de dados usadas em microsoftml são definidas como objetos revoscalepy. Limitações de contexto de computação na transferência do revoscalepy para microsoftml. Ou seja, todas as funcionalidades estão disponíveis para operações locais, mas alternar para um contexto de computação remota requer o RxInSqlServer.

## <a name="using-python-in-sql-server"></a>Como usar o Python no SQL Server

Você importa o módulo **revoscalepy** para o código Python e, em seguida, chama funções do módulo, como ocorre com qualquer outra função do Python.

As fontes de dados compatíveis incluem bancos de dados ODBC, SQL Server e formato de arquivo XDF para trocar dados com outras fontes ou com soluções de R. Os dados de entrada para Python devem ser tabulares. Todos os resultados do Python devem ser retornados na forma de um quadro de dados do **Pandas**.

Os contextos de computação compatíveis incluem o contexto de computação local ou remota do SQL Server. Um contexto de computação remota refere-se à execução de código que começa em um computador, como uma estação de trabalho, mas, em seguida, alterna a execução do script para um computador remoto. Alternar o contexto de computação requer que ambos os sistemas tenham a mesma biblioteca revoscalepy.

O contexto de computação local, como você pode esperar, inclui a execução do código Python no mesmo servidor que a instância do mecanismo de banco de dados, com o código dentro de T-SQL ou inserido em um procedimento armazenado. Você também pode executar o código de um IDE Python local e fazer com que o script seja executado no computador SQL Server, definindo um contexto de computação remota.

## <a name="execution-architecture"></a>Arquitetura de execução

Os diagramas a seguir descrevem a interação dos componentes do SQL Server com o runtime do Python em cada um dos cenários compatíveis: execução de script no banco de dados e execução remota de um terminal do Python, usando um contexto de computação do SQL Server.

### <a name="python-scripts-executed-in-database"></a>Scripts Python executados no banco de dados

Ao executar o Python "dentro" do SQL Server, você precisa encapsular o script Python dentro de um procedimento armazenado especial, o [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Depois que o script tiver sido inserido no procedimento armazenado, qualquer aplicativo que possa fazer uma chamada de procedimento armazenado poderá iniciar a execução do código Python.  Então, o SQL Server gerencia a execução de código, conforme resumido no diagrama a seguir.

![script-in-db-python](../../machine-learning/python/media/script-in-db-python2.png)

1. Uma solicitação para o runtime de Python é indicada pelo parâmetro `@language='Python'` passado para o procedimento armazenado. O SQL Server envia essa solicitação para o serviço Launchpad.
No Linux, o SQL usa um serviço **Launchpad** para se comunicar com um processo Launchpad separado para cada usuário. Veja o [Diagrama da arquitetura de extensibilidade](extensibility-framework.md#architecture-diagram) para obter detalhes.
2. O serviço Launchpad inicia o inicializador apropriado; neste caso, PythonLauncher.
3. O PythonLauncher inicia o processo Python35 externo.
4. O BxlServer coordena-se com o runtime do Python para gerenciar a troca de dados e o armazenamento de resultados funcionais.
5. O Satélite SQL gerencia as comunicações sobre processos e tarefas relacionadas com o SQL Server.
6. O BxlServer usa Satélite SQL para comunicar o status e os resultados ao SQL Server.
7. O SQL Server obtém resultados e fecha os processos e tarefas relacionados.

### <a name="python-scripts-executed-from-a-remote-client"></a>Scripts Python executados de um cliente remoto

Você pode executar scripts Python de um computador remoto, tal como um laptop, fazendo com que eles sejam executados no contexto do computador do SQL Server, se estas condições forem atendidas:

+ Você cria os scripts adequadamente
+ O computador remoto instalou as bibliotecas de extensibilidade usadas pelo Serviços de Machine Learning. O pacote [revoscalepy](../python/ref-py-revoscalepy.md) é necessário para usar contextos de computação remota.

O diagrama a seguir resume o fluxo de trabalho geral quando os scripts são enviados de um computador remoto.

![remote-sqlcc-from-python](../../machine-learning/python/media/remote-sqlcc-from-python3.png)

1. Para funções compatíveis com o **revoscalepy**, o runtime do Python chama uma função de vinculação que, por sua vez, chama o BxlServer.
2. O BxlServer está incluído com Serviços de Machine Learning (no banco de dados) e é executado em um processo separado do runtime do Python.
3. O BxlServer determina o destino da conexão e inicia uma conexão usando o ODBC, passando as credenciais fornecidas como parte da cadeia de conexão no script Python.
4. O BxlServer abre uma conexão para a instância do SQL Server.
5. Quando um runtime de script externo é chamado, o serviço Launchpad é invocado e, por sua vez, inicia o inicializador apropriado, que nesse caso é PythonLauncher.dll. Depois disso, o processamento do código Python é tratado em um fluxo de trabalho semelhante àquele de quando o código Python é invocado de um procedimento armazenado no T-SQL.
6. O PythonLauncher faz uma chamada para a instância do Python instalada no computador do SQL Server.
7. Os resultados são retornados ao BxlServer.
8. O Satélite SQL gerencia a comunicação com o SQL Server e a limpeza dos objetos de trabalho relacionados.
9. O SQL Server passa os resultados de volta para o cliente.

## <a name="next-steps"></a>Próximas etapas

+ [módulo revoscalepy no SQL Server](../python/ref-py-revoscalepy.md)
+ [referência de função revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [Estrutura de extensibilidade no SQL Server](extensibility-framework.md)
+ [Extensões de aprendizado de máquina e R no SQL Server](extension-r.md)
+ [Obter informações sobre o pacote do Python](../package-management/python-package-information.md)
+ [Instalar pacotes Python com o sqlmlutils](../package-management/install-additional-python-packages-on-sql-server.md)
