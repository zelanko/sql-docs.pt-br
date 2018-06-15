---
title: Componentes de integração do Python com o aprendizado de máquina do SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f00735c78b59a9eec41f8ef4ae77fb6accf013d1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31204678"
---
# <a name="components-in-sql-server-to-support-python-integration"></a>Componentes do SQL Server para dar suporte à integração do Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A partir do SQL Server 2017, serviços de aprendizado de máquina dá suporte a Python como uma linguagem externa que pode ser executada de T-SQL ou executado remotamente usando o SQL Server como o contexto de computação.

Especificamente, este tópico descreve os componentes no SQL Server 2017 que oferecem suporte à extensibilidade em geral e a linguagem Python.

## <a name="sql-server-components-and-providers"></a>Provedores e componentes do SQL Server

Para configurar o SQL Server 2017 para permitir a execução de script de Python é um processo de várias etapa.

1. Instale o recurso de extensibilidade.
2. Habilite o recurso de execução do script externo.
3. Reinicie o serviço de mecanismo de banco de dados.

Podem ser necessárias etapas adicionais para permitir a execução de script remoto.

Para obter mais informações, consulte [instalar o SQL Server 2017 Machine Learning Services (no banco de dados)](../install/sql-machine-learning-services-windows-install.md).

### <a name="launchpad"></a>Launchpad

O Launchpad do SQL Server confiável é um serviço introduzido no SQL Server 2016 que gerencia e executa scripts externos, semelhantes ao modo que o serviço de indexação e consulta de texto completo inicia um host separado para processar consultas de texto completo.

O serviço Launchpad pode iniciar somente os iniciadores confiáveis que são publicados pela Microsoft, ou que tenham sido certificados pela Microsoft como atendem às necessidades de desempenho e gerenciamento de recursos.

+ 2017 do SQL Server dá suporte a R e 3.5 do Python
+ SQL Server 2016 dá suporte a R

O serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é executado em sua própria conta de usuário.

> [!TIP]
> Se você alterar a conta que executa a barra inicial, certifique-se de fazer isso usar o SQL Server Configuration Manager, para garantir que as alterações são gravadas em arquivos relacionados.

Para executar tarefas em um determinado idioma com suporte, a barra inicial obtém uma conta de trabalho protegidos do pool e inicia um processo de satélite para gerenciar o tempo de execução externo:

+ RLauncher.dll para a linguagem R
+ Pythonlauncher.dll para Python 3.5

Cada processo de satélite herda a conta de usuário da barra inicial e usa a conta de trabalho para a duração da execução do script. Se o script de Python usa processos paralelos, eles são criados sob a conta de trabalho mesmo, único.

Para obter mais informações sobre o contexto de segurança da barra inicial, consulte [segurança](security-overview-sql-server-python-services.md).

### <a name="bxlserver-and-sql-satellite"></a>BxlServer e satélite SQL

Se você executar [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) enquanto um trabalho de Python é executado, você poderá ver uma ou várias instâncias do BxlServer.

**BxlServer** é um executável fornecido pela Microsoft que gerencia a comunicação entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e Python (ou R). Ele cria os objetos de trabalho do Windows que são usados para conter as sessões do script externo, pastas de trabalho segura provisões para cada trabalho de script externo e usa satélite de SQL para gerenciar a transferência de dados entre o tempo de execução externo e [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

Na verdade, BxlServer é um complemento para Python que funciona com [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para transferir dados e gerenciar tarefas. BXL significa linguagem Exchange binário e refere-se para o formato de dados usado para mover dados de forma eficiente entre o SQL Server e processos externos. BxlServer também é uma parte importante da Microsoft R Client e Microsoft R Server.

**Satélite de SQL** é uma API de extensibilidade, incluído no mecanismo de banco de dados, começando com o SQL Server 2016, que oferece suporte a código externo ou tempos de execução externos implementados usando C ou C++.

O BxlServer usa o Satélite SQL para estas tarefas:

+ Ler dados de entrada
+ Gravar dados de saída
+ Obter argumentos de entrada
+ Gravar argumentos de saída
+ Manipulação de erros
+ Gravar STDOUT e STDERR de volta para o cliente

Satélite de SQL usa um formato de dados personalizado que é otimizado para a transferência de dados rápidos entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e linguagens de script externo. Ele executa conversões de tipo e define os esquemas de conjuntos de dados de entrada e saídos durante as comunicações entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e o tempo de execução do script externo.

O satélite de SQL pode ser monitorado usando estendidos (xEvents) de eventos do windows. Para obter mais informações, consulte [eventos estendidos para R](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md).

## <a name="communication-channels-between-components"></a>Canais de comunicação entre os componentes

+ **TCP/IP**

  Por padrão, as comunicações internas entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e o satélite de SQL usar TCP/IP.

+ **Pipes nomeados**

  O transporte de dados internos entre o BxlServer e o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] por meio do Satélite SQL usa um formato de dados proprietários e compactados para melhorar o desempenho. Dados são trocados entre Python e o BxlServer no formato BXL, usando Pipes nomeados.

+ **ODBC**

  As comunicações entre clientes de ciência de dados externa e a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instância usar o ODBC. A conta que envia o script de trabalhos para [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] deve ter as permissões para se conectar à instância e executar scripts externos.

  Além disso, dependendo da tarefa, a conta talvez seja necessário essas permissões:

  + Leitura de dados usados pelo trabalho
  + Gravar dados em tabelas: por exemplo, quando salvar resultados em uma tabela
  + Criar objetos de banco de dados: por exemplo, se for salvar o script externo como parte de um novo procedimento armazenado.

  Quando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] é usado como o contexto de computação para execução de script de Python de um cliente remoto e o executável do Python deve recuperar dados de uma fonte externa, o ODBC é usado para write-back. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mapeia a identidade do usuário que emite o comando remoto para a identidade do usuário na instância atual e executa o comando ODBC usando as credenciais do usuário. A cadeia de conexão necessária para executar essa chamada ODBC é obtida do código cliente.

## <a name="interaction-of-components"></a>Interação de componentes

Os diagramas a seguir descrevem a interação de componentes do SQL Server com o tempo de execução do Python em cada um dos cenários com suporte: executando a execução do script no banco de dados e remota de um terminal Python, usando um contexto de computação do SQL Server.

### <a name="python-scripts-executed-in-database"></a>Scripts de Python executados no banco de dados

Quando você executa o Python "internos" [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], você deve encapsular o script de Python dentro de um procedimento de armazenado especial, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Depois que o script foi incorporado no procedimento armazenado, qualquer aplicativo que pode fazer um procedimento armazenado chamada pode iniciar a execução do código Python.  Depois disso [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] gerencia a execução de código, como resumido no diagrama a seguir.

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Uma solicitação para o tempo de execução do Python é indicada pelo parâmetro `@language='Python'` passado para o procedimento armazenado. SQL Server envia a solicitação para o serviço Launchpad.
2. O serviço Launchpad inicia o iniciador apropriado; Nesse caso, PythonLauncher.
3. PythonLauncher inicia o processo de Python35 externo.
4. BxlServer coordena com o tempo de execução do Python para gerenciar a troca de dados e o armazenamento de resultados de trabalho.
5. Satélite de SQL gerencia comunicações sobre tarefas relacionadas e processa a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
6. O BxlServer usa Satélite SQL para comunicar o status e os resultados para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
7. O [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] obtém resultados e fecha os processos e tarefas relacionados.

### <a name="python-scripts-executed-from-a-remote-client"></a>Scripts de Python executados a partir de um cliente remoto

Você pode executar scripts Python em um computador remoto, como um laptop e sejam executadas no contexto do computador do SQl Server, se essas condições forem atendidas:

+ Criar scripts adequadamente
+ O computador remoto tiver instalado as bibliotecas de extensibilidade que são usadas por serviços de aprendizado de máquina. O [revoscalepy](what-is-revoscalepy.md) pacote é necessário usar os contextos de computação remota.

O diagrama a seguir resume o fluxo de trabalho geral quando os scripts forem enviados de um computador remoto.

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. Para as funções que têm suporte em **revoscalepy**, o tempo de execução do Python chama uma função de vinculação, que por sua vez chama BxlServer.
2. BxlServer está incluído com os serviços de aprendizado de máquina (no banco de dados) e é executado em um processo separado do tempo de execução do Python.
3. BxlServer determina o destino de conexão e inicia uma conexão usando o ODBC, passando as credenciais fornecidas como parte da cadeia de conexão no script de Python.
4. O BxlServer abre uma conexão para a instância do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
5. Quando um tempo de execução do script externo é chamado, o serviço Launchpad é chamado, o que por sua vez inicia o iniciador apropriado: nesse caso, PythonLauncher.dll. Depois disso, o processamento de código Python é tratado em um fluxo de trabalho semelhante à que quando o código Python é chamado de um procedimento armazenado no T-SQL.
6. PythonLauncher faz uma chamada para a instância do Python que está instalado no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] computador.
7. Os resultados são retornados ao BxlServer.
8. O Satélite SQL gerencia a comunicação com o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e a limpeza dos objetos de trabalho relacionados.
9. O [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] passa os resultados de volta para o cliente.

## <a name="next-steps"></a>Próximas etapas

[Visão geral da arquitetura de Python no SQL Server](architecture-overview-sql-server-python.md)
