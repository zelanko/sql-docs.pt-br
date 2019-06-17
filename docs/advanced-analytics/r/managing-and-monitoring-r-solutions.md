---
title: Gerenciar e integrar cargas de trabalho de aprendizado de máquina - serviços de aprendizado de máquina do SQL Server
description: Como um DBA do SQL Server, examine as tarefas administrativas para a implantação de um subsistema de R e Python em uma instância do mecanismo de banco de dados de aprendizado de máquina.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: a53056f1f169224b222a07a062f6ddd88cb24b81
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66454679"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>Gerenciar e integrar cargas de trabalho de aprendizado de máquina no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo destina-se a administradores de banco de dados do SQL Server que são responsáveis por implantar uma infraestrutura de ciência de dados eficiente em um ativo do servidor que dão suporte a várias cargas de trabalho. Ele quadros o espaço do problema administrativo relevante para o gerenciamento de R e execução no SQL Server de código do Python. 

## <a name="what-is-feature-integration"></a>O que é a integração de recursos

R e Python de aprendizado de máquina é fornecido pelo [serviços de aprendizado de máquina do SQL Server](../what-is-sql-server-machine-learning.md) como uma extensão para uma instância do mecanismo de banco de dados. A integração é principalmente por meio de camada de segurança e a linguagem de definição de dados resumido da seguinte maneira:

+ Procedimentos armazenados são equipados com a capacidade de aceitar o R e como parâmetros de entrada de código do Python. Os desenvolvedores e cientistas de dados podem usar um [procedimento armazenado do sistema](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017) ou criar um procedimento personalizado que encapsula o seu código.
+ Funções T-SQL (ou seja, [PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)) que pode consumir um modelo de dados previamente treinada. Essa funcionalidade está disponível por meio do T-SQL. Como tal, ele pode ser chamado em um sistema que não tenha especificamente as extensões instaladas de aprendizado de máquina.
+ Logons de banco de dados existentes e as permissões baseadas em função abrangem os scripts invocado pelo usuário utilizando esses mesmos dados. Como regra geral, se os usuários não podem acessar dados por meio de uma consulta, eles não podem acessá-lo por meio de script ou.

## <a name="feature-availability"></a>Disponibilidade de recursos

Integração de R e Python se torna disponível por meio de uma sucessão de etapas. A primeira é a instalação, quando você [incluem ou adicione o **serviços de Machine Learning** ](../install/sql-machine-learning-services-windows-install.md) recurso para uma instância do mecanismo de banco de dados. Como uma etapa posterior, você deve habilitar scripts externos na instância do mecanismo de banco de dados (ele está desativado por padrão).

Neste momento, somente os administradores de banco de dados têm permissão total para criar e executar scripts externos, adicionar ou excluir pacotes e criar procedimentos armazenados e outros objetos.

Todos os outros usuários devem ter permissão EXECUTE ANY EXTERNAL SCRIPT. Adicional [permissões de banco de dados padrão](../security/user-permission.md) determinar se os usuários podem criar objetos, executar scripts, consumir modelos treinados e serializados e assim por diante. 

## <a name="resource-allocation"></a>Alocação de recursos

Procedimentos armazenados e consultas T-SQL que invocam processamento externo usam os recursos disponíveis para o pool de recursos padrão. Como parte da configuração padrão, os processos externos, como sessões de R e Python são permitidos até 20% da memória total no sistema host. 

Se você quiser reajustar a alocação de recursos, você pode modificar o pool padrão, com um efeito correspondente em cargas de trabalho de aprendizado de máquina em execução no sistema.

Outra opção é criar um pool de recursos externos personalizado para sessões provenientes de programas específicos, hosts ou que ocorrem durante determinados intervalos de tempo de atividade de captura. Para obter mais informações, consulte [governança de recursos para modificar os níveis de recursos para execução de R e Python](../administration/resource-governance.md) e [como criar um pool de recursos](../administration/how-to-create-a-resource-pool.md) para obter instruções passo a passo.

## <a name="isolation-and-containment"></a>Isolamento e confinamento

A arquitetura de processamento é projetada para isolar o processamento do mecanismo básico de scripts externos. Scripts de R e Python executados como processos separados, em contas de trabalho local. No Gerenciador de tarefas, você pode monitorar processos de R e Python, em execução em uma conta de usuário local de baixo privilégio, diferente da conta de serviço do SQL Server. 

A execução de processos de R e Python em contas individuais de baixo privilégio tem os seguintes benefícios:

+ Isola os principais processos de mecanismo de sessões R e Python, que você pode encerrar um processo de R ou Python sem afetar as operações de banco de dados principal. 

+ Reduz os privilégios dos processos de tempo de execução de script externo no computador host.

Contas de usuário sem privilégios administrativos são criadas durante a instalação e colocadas em um Windows *pool de contas de usuário* chamado **SQLRUserGroup**. Por padrão, esse grupo tem permissão para usar conjuntos de dados internos, bibliotecas e executáveis na pasta do programa para R e Python no SQL Server. 

Como um DBA, você pode usar a segurança de dados do SQL Server para especificar quem tem permissão para executar scripts e que os dados usados em trabalhos sejam gerenciados sob as mesmas funções de segurança que controlam o acesso por meio de consultas T-SQL. Como um administrador do sistema, você pode negar explicitamente **SQLRUserGroup** acesso a dados confidenciais no servidor local com a criação de ACLs.

>[!NOTE]
> Por padrão, o **SQLRUserGroup** não tem um logon ou permissões no próprio SQL Server. Contas de trabalho devem exigir um logon para acesso a dados, você deve criá-lo. Um cenário que chama especificamente para a criação de um logon é dar suporte a solicitações de um script em execução, para dados ou operações na instância do mecanismo de banco de dados, quando a identidade do usuário é um usuário do Windows e a cadeia de caracteres de conexão Especifica um usuário confiável. Para obter mais informações, consulte [adicionar SQLRUserGroup como um usuário de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

## <a name="disable-script-execution"></a>Desabilitar a execução de script

No caso de fuga scripts, você pode desativar toda a execução de script, revertendo as etapas anteriormente assumidas para habilitar a execução de script externo em primeiro lugar.

1. No SQL Server Management Studio ou outra ferramenta de consulta, execute este comando para definir `external scripts enabled` como 0 ou FALSE.

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. Reinicie o serviço de mecanismo de banco de dados.

Depois de resolver o problema, lembre-se de habilitar novamente a execução do script na instância se você deseja retomar o R e o suporte do Python de script na instância do mecanismo de banco de dados. Para obter mais informações, consulte [habilitar a execução do script](../install/sql-machine-learning-services-windows-install.md#enable-script-execution)

## <a name="extend-functionality"></a>Estender a funcionalidade

Ciência de dados geralmente introduz novos requisitos para implantação de pacote e a administração. Para um cientista de dados, ele é uma prática comum para aproveitar os pacotes de código-fonte aberto e de terceiros em soluções personalizadas. Alguns desses pacotes terão as dependências em outros pacotes, nesse caso, talvez você precise avaliar e instalar vários pacotes para alcançar seu objetivo.

Como um DBA responsável por um ativo do servidor, implantando pacotes de R e Python arbitrários em um servidor de produção representa um desafio desconhecido. Antes de adicionar pacotes, você deve avaliar se a funcionalidade fornecida pelo pacote externo é realmente necessária, com nenhum equivalente em internos [linguagem R](r-libraries-and-data-types.md) e [bibliotecas Python](../python/python-libraries-and-data-types.md) instalado Instalação do SQL Server. 

Como uma alternativa para a instalação do pacote de servidor, um cientista de dados pode conseguir [compilar e executar soluções em uma estação de trabalho externa](../r/set-up-a-data-science-client.md), recuperando dados do SQL Server, mas com toda a análise realizada localmente na estação de trabalho em vez de no próprio servidor. 

Se você subsequentemente determinar que as funções de biblioteca externa são necessárias e não apresentam um risco para operações de servidor ou de dados como um todo, podem ser escolhidos várias metodologias para adicionar pacotes. Na maioria dos casos, são necessários direitos de administrador para adicionar pacotes ao SQL Server. Para obter mais informações, consulte [instalar pacotes Python no SQL Server](../python/install-additional-python-packages-on-sql-server.md) e [instalar pacotes R no SQL Server](install-additional-r-packages-on-sql-server.md).

> [!NOTE]
> Para pacotes de R, direitos de administrador do servidor não são especificamente necessários para a instalação do pacote se você usar métodos alternativos. Ver [instalar pacotes R no SQL Server](install-additional-r-packages-on-sql-server.md) para obter detalhes.

## <a name="monitoring-script-execution"></a>Monitorando a execução do script

Scripts de R e Python que são executados no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] são iniciados com o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] interface. No entanto, o Launchpad não tem recursos controlados ou monitorados separadamente, pois ele é um serviço seguro fornecido pela Microsoft que gerencia os recursos adequadamente.

Scripts externos executados sob o serviço Launchpad são gerenciados usando o [objeto de trabalho do Windows](/windows/desktop/ProcThread/job-objects). Um objeto de trabalho permite que grupos de processos sejam gerenciados como uma unidade. Cada objeto de trabalho é hierárquico e controla os atributos de todos os processos associados a ele. As operações realizadas em um objeto de trabalho afetam todos os processos associados ao objeto de trabalho.

Portanto, se precisar encerrar um trabalho associado a um objeto, lembre-se de que todos os processos relacionados também serão encerrados. Se você estiver executando um script de R que é atribuído a um objeto de trabalho do Windows e esse script executa um trabalho ODBC relacionado que deve ser encerrado, o processo pai do script de R também será encerrado.

Se você iniciar um script externo que usa processamento paralelo, um único objeto de trabalho do Windows gerencia todos os processos filho paralelos.

Para determinar se um processo está em execução em um trabalho, use a função `IsProcessInJob`.

## <a name="next-steps"></a>Próximas etapas

+ Examine os conceitos e componentes do [arquitetura de extensibilidade](../concepts/extensibility-framework.md) e [segurança](../concepts/security.md) para obter mais informações.

+ Como parte da instalação do recurso, você pode já estar familiarizado com o usuário final a dados de controle de acesso, mas caso contrário, consulte [conceder permissões de usuário para o aprendizado de máquina do SQL Server](../security/user-permission.md) para obter detalhes. 

+ Saiba como ajustar os recursos do sistema para cargas de trabalho de aprendizado de máquina de computação intensiva. Para obter mais informações, consulte [como criar um pool de recursos](../administration/how-to-create-a-resource-pool.md).
