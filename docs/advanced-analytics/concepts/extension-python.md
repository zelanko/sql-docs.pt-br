---
title: Extensão do Python no SQL Server Machine Learning Services | Microsoft Docs
description: Saiba mais sobre a execução de código do Python e bibliotecas internas do Python no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 24d34ee2ca9220ca1569ea83bcb092030d1ef692
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892846"
---
# <a name="python-extension-in-sql-server"></a>Extensão do Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A extensão do Python é parte do complemento serviços do SQL Server Machine Learning para o mecanismo de banco de dados relacional. Ele adiciona um ambiente de execução do Python, distribuição do Anaconda com o tempo de execução do Python 3.5 e interpretador, ferramentas e bibliotecas padrão e as bibliotecas de produto da Microsoft para Python: [revoscalepy](../python/what-is-revoscalepy.md) para análise em escala e com [microsoftml](../using-the-microsoftml-package.md) algoritmos de aprendizado de máquina. 

Integração do Python é instalada como [serviços do SQL Server Machine Learning](../what-is-sql-server-machine-learning.md).

Instalação do tempo de execução do Python 3.5 e interpretador garante uma compatibilidade quase completa com soluções padrão do Python. Python é executado em um processo separado do SQL Server, para garantir que as operações de banco de dados não estão comprometidas.

## <a name="python-components"></a>Componentes do Python

O SQL Server inclui pacotes de software livre e proprietários. O tempo de execução do Python instalado pelo programa de instalação é Anaconda 4.2 com o Python 3.5. O tempo de execução do Python é instalado, independentemente das ferramentas do SQL e é executado fora do principais processos de mecanismo, na estrutura de extensibilidade. Como parte da instalação de serviços de Machine Learning com o Python, você deve concordar com os termos da licença pública GNU. 

SQL Server não modifica os executáveis do Python, mas você deve usar a versão do Python instalado pelo programa de instalação porque essa versão é o que os pacotes de proprietários são criados e testados em. Para obter uma lista de pacotes com suporte pela distribuição Anaconda, consulte o site do Continuum analytics: [lista de pacotes do Anaconda](https://docs.continuum.io/anaconda/pkg-docs).

A distribuição Anaconda associada a uma instância do mecanismo de banco de dados específico pode ser encontrada na pasta associada à instância. Por exemplo, se você instalou o mecanismo de banco de dados do SQL Server 2017 com serviços de Machine Learning e o Python na instância padrão, procure em `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`.

Pacotes de Python adicionados pela Microsoft para cargas de trabalho paralelas e distribuídas incluem as seguintes bibliotecas.

| Biblioteca | Description |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Dá suporte à visualização e exploração de dados, manipulação, transformação e objetos de fonte de dados. Ele dá suporte à criação de contextos de computação remota, bem como um vários modelos de aprendizado de máquina escalonáveis, tais como **rxLinMod**. É equivalente do [ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) pacote para o Microsoft R. |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Contém algoritmos de aprendizado de máquina que foram otimizados para velocidade e precisão, bem como as transformações para trabalhar com imagens e texto em linha. Para obter mais informações, consulte [usando o pacote MicrosoftML com o SQL Server](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package). |

Microsoftml e revoscalepy estão firmemente acopladas; fontes de dados usadas em microsoftml são definidas como objetos revoscalepy. Limitações de contexto na transferência revoscalepy ao microsoftml de computação. Ou seja, toda a funcionalidade está disponível para operações locais, mas a mudança para um contexto de computação remota exige o RxInSqlServer.

## <a name="using-python-in-sql-server"></a>Usando o Python no SQL Server

Importar o **revoscalepy** módulo em seu código Python e, em seguida, chamam funções do módulo, como nenhuma outra função de Python.

Fontes de dados com suporte incluem bancos de dados ODBC, o SQL Server e o formato de arquivo XDF para trocar dados com outras fontes, ou com soluções de R. Dados de entrada para o Python devem ser tabulares. Todos os resultados de Python devem ser retornados na forma de um **pandas** quadro de dados.

Contextos de computação com suporte incluem o contexto de computação do SQL Server local ou remoto. Um contexto de computação remota refere-se a execução de código que começa em um computador, como uma estação de trabalho, mas, em seguida, opções de execução de um script para um computador remoto. Alternar o contexto de computação requer que ambos os sistemas tenham a mesma biblioteca revoscalepy.

Contexto de computação local, como você pode esperar, inclui a execução de código do Python no mesmo servidor como a instância do mecanismo de banco de dados, com o código de T-SQL ou inserido em um procedimento armazenado. Você também pode executar o código de um IDE Python local e têm o script executado no computador do SQL Server, o contexto de computação com a definição de um controle remoto.

## <a name="execution-architecture"></a>Arquitetura de execução

O diagrama a seguir mostra a interação de componentes do SQL Server com o tempo de execução do Python em cada um dos cenários com suporte: em execução a execução do script no banco de dados e remotos em um terminal de Python, usando um contexto de computação do SQL Server.

### <a name="python-scripts-executed-in-database"></a>Scripts de Python executado no banco de dados

Quando você executar o Python "dentro" do SQL Server, você deve encapsular o script de Python dentro de um procedimento de armazenado especial [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Depois que o script foi incorporado no procedimento armazenado, qualquer aplicativo que pode fazer um procedimento armazenado a chamada pode iniciar a execução do código Python.  Daí em diante do SQL Server gerencia a execução de código, conforme resumido no diagrama a seguir.

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Uma solicitação para o tempo de execução do Python é indicada pelo parâmetro `@language='Python'` passado para o procedimento armazenado. SQL Server envia essa solicitação ao serviço Launchpad.
2. O serviço Launchpad inicia o inicializador apropriado; Nesse caso, PythonLauncher.
3. PythonLauncher inicia o processo de Python35 externo.
4. O BxlServer coordena com o tempo de execução do Python para gerenciar a troca de dados e o armazenamento de resultados do trabalho.
5. Satélite SQL gerencia comunicações sobre processos com o SQL Server e tarefas relacionadas.
6. O BxlServer usa satélite SQL para se comunicar o status e os resultados para o SQL Server.
7. SQL Server obtém resultados e fecha os processos e tarefas relacionadas.

### <a name="python-scripts-executed-from-a-remote-client"></a>Scripts de Python executados a partir de um cliente remoto

Você pode executar scripts Python em um computador remoto, como um laptop e fazer com que elas são executadas no contexto do computador do SQl Server, se essas condições forem atendidas:

+ Projetar adequadamente os scripts
+ O computador remoto tiver instalado as bibliotecas de extensibilidade que são usadas pelos serviços de aprendizado de máquina. O [revoscalepy](../python/what-is-revoscalepy.md) pacote é necessário para usar contextos de computação remota.

O diagrama a seguir resume o fluxo de trabalho geral, quando os scripts são enviados de um computador remoto.

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. Para as funções que têm suporte no **revoscalepy**, o tempo de execução do Python chama uma função de vinculação, que por sua vez, chama BxlServer.
2. O BxlServer é incluído com os serviços do Machine Learning (no banco de dados) e é executado em um processo separado do tempo de execução do Python.
3. O BxlServer determina o destino de conexão e inicia uma conexão usando o ODBC, passando as credenciais fornecidas como parte da cadeia de conexão no script do Python.
4. O BxlServer abre uma conexão à instância do SQL Server.
5. Quando um tempo de execução do script externo é chamado, o serviço Launchpad é chamado, que por sua vez inicia o inicializador apropriado: nesse caso, PythonLauncher.dll. Depois disso, o processamento de código do Python é tratado em um fluxo de trabalho semelhante ao que quando o código do Python é invocado de um procedimento armazenado no T-SQL.
6. PythonLauncher faz uma chamada para a instância do Python que está instalado no computador do SQL Server.
7. Os resultados são retornados ao BxlServer.
8. Satélite SQL gerencia a comunicação com o SQL Server e a limpeza dos objetos de trabalho relacionados.
9. SQL Server passa os resultados ao cliente.

## <a name="see-also"></a>Confira também

+ [O que é revoscalepy](../python/what-is-revoscalepy.md) 
+ [Estrutura de extensibilidade no SQL Server](extensibility-framework.md)
+ [R e machine learning extensões no SQL Server](extension-r.md)