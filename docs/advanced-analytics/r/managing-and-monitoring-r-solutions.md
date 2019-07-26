---
title: Gerenciar e integrar cargas de trabalho do Machine Learning
description: Como DBA SQL Server, examine as tarefas administrativas para implantar um subsistema R e Python de Machine Learning em uma instância do mecanismo de banco de dados.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 705df9d06a7dbf4563df3670894351d15c0962a5
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470092"
---
# <a name="manage-and-integrate-machine-learning-workloads-on-sql-server"></a>Gerenciar e integrar cargas de trabalho de aprendizado de máquina em SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo destina-se a administradores de banco de dados SQL Server que são responsáveis por implantar uma infraestrutura eficiente de ciência de dado em um ativo de servidor com suporte a várias cargas de trabalho. Ele codifica o espaço de problema administrativo relevante para o gerenciamento de execução de código R e Python em SQL Server. 

## <a name="what-is-feature-integration"></a>O que é integração de recursos

O aprendizado de máquina R e Python é fornecido pelo [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md) como uma extensão para uma instância do mecanismo de banco de dados. A integração é principalmente por meio da camada de segurança e da linguagem de definição de dados, resumida da seguinte maneira:

+ Os procedimentos armazenados são equipados com a capacidade de aceitar código R e Python como parâmetros de entrada. Os desenvolvedores e os cientistas de dados podem usar um [procedimento armazenado do sistema](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql?view=sql-server-2017) ou criar um procedimento personalizado que encapsula seu código.
+ Funções T-SQL (ou seja, [previsão](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)) que podem consumir um modelo de dados treinado anteriormente. Esse recurso está disponível por meio do T-SQL. Como tal, ele pode ser chamado em um sistema que não tenha especificamente as extensões de Machine Learning instaladas.
+ Os logons de banco de dados existentes e as permissões baseadas em função abrangem os scripts invocados pelo usuário que utilizam esses mesmos dados. Como regra geral, se os usuários não puderem acessar dados por meio de uma consulta, eles também não poderão acessá-lo por meio de script.

## <a name="feature-availability"></a>Disponibilidade de recursos

A integração com o R e o Python se torna disponível por meio de uma sucessão de etapas. A primeira é a configuração, quando você [inclui ou adiciona o recurso de **serviços de Machine Learning** ](../install/sql-machine-learning-services-windows-install.md) a uma instância do mecanismo de banco de dados. Como uma etapa subsequente, você deve habilitar o script externo na instância do mecanismo de banco de dados (está desativado por padrão).

Neste ponto, somente os administradores de banco de dados têm permissão total para criar e executar scripts externos, adicionar ou excluir pacotes e criar procedimentos armazenados e outros objetos.

Todos os outros usuários devem receber a permissão executar qualquer SCRIPT externo. [Permissões de banco de dados padrão](../security/user-permission.md) adicionais determinam se os usuários podem criar objetos, executar scripts, consumir modelos serializados e treinados e assim por diante. 

## <a name="resource-allocation"></a>Alocação de recursos

Os procedimentos armazenados e as consultas T-SQL que invocam o processamento externo usam os recursos disponíveis para o pool de recursos padrão. Como parte da configuração padrão, processos externos, como sessões de R e Python, têm permissão de até 20% da memória total no sistema host. 

Se você quiser reajustar a origem, poderá modificar o pool padrão, com o efeito correspondente nas cargas de trabalho de aprendizado de máquina em execução nesse sistema.

Outra opção é criar um pool de recursos externos personalizado para capturar sessões provenientes de programas, hosts ou atividades específicas que ocorrem durante intervalos de tempo específicos. Para obter mais informações, consulte [governança de recursos para modificar os níveis de recursos para a execução de R e Python](../administration/resource-governance.md) e [como criar um pool de recursos](../administration/how-to-create-a-resource-pool.md) para obter instruções passo a passo.

## <a name="isolation-and-containment"></a>Isolamento e confinamento

A arquitetura de processamento é projetada para isolar scripts externos do processamento principal do mecanismo. Os scripts R e Python são executados como processos separados, em contas de trabalho locais. No Gerenciador de tarefas, você pode monitorar os processos de R e Python, executando sob uma conta de usuário local com poucos privilégios, diferente da conta de serviço do SQL Server. 

A execução de processos de R e Python em contas de baixo privilégio individuais tem os seguintes benefícios:

+ Isola os processos do mecanismo principal de sessões do R e do Python, você pode encerrar um processo de R ou Python sem afetar as operações de banco de dados principal. 

+ Reduz os privilégios dos processos de tempo de execução de script externo no computador host.

Contas com privilégios mínimos são criadas durante a instalação e colocadas em um *pool de contas de usuário* do Windows chamado **SQLRUserGroup**. Por padrão, esse grupo tem permissão para usar arquivos executáveis, bibliotecas e conjuntos de d-in na pasta programa para R e Python em SQL Server. 

Como DBA, você pode usar SQL Server segurança de dados para especificar quem tem permissão para executar scripts e que os dados usados em trabalhos são gerenciados sob as mesmas funções de segurança que controlam o acesso por meio de consultas T-SQL. Como administrador do sistema, você pode negar explicitamente o acesso **SQLRUserGroup** a dados confidenciais no servidor local criando ACLs.

>[!NOTE]
> Por padrão, o **SQLRUserGroup** não tem um logon ou permissões no SQL Server em si. As contas de trabalho devem exigir um logon para acesso a dados, você mesmo deve criá-la. Um cenário que chama especificamente a criação de um logon é dar suporte a solicitações de um script na execução, para dados ou operações na instância do mecanismo de banco de dado, quando a identidade do usuário é um usuário do Windows e a cadeia de conexão especifica um usuário confiável. Para obter mais informações, consulte [Adicionar SQLRUserGroup como um usuário de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

## <a name="disable-script-execution"></a>Desabilitar a execução de script

No caso de scripts de fuga, você pode desabilitar toda a execução do script, revertendo as etapas anteriormente executadas para habilitar a execução de script externo em primeiro lugar.

1. No SQL Server Management Studio ou outra ferramenta de consulta, execute este comando para `external scripts enabled` definir como 0 ou falso.

    ```sql
    EXEC sp_configure  'external scripts enabled', 0
    RECONFIGURE WITH OVERRIDE
    ```
2. Reinicie o serviço do mecanismo de banco de dados.

Depois de resolver o problema, lembre-se de reabilitar a execução de script na instância se quiser retomar o suporte de script R e Python na instância do mecanismo de banco de dados. Para obter mais informações, consulte [habilitar execução de script](../install/sql-machine-learning-services-windows-install.md#enable-script-execution)

## <a name="extend-functionality"></a>Estender funcionalidade

A ciência de dados geralmente apresenta novos requisitos para a implantação e a administração de pacotes. Para um cientista de dados, é uma prática comum aproveitar pacotes de código-fonte aberto e de terceiros em soluções personalizadas. Alguns desses pacotes terão dependências em outros pacotes, caso em que talvez seja necessário avaliar e instalar vários pacotes para alcançar seu objetivo.

Como DBA responsável por um ativo de servidor, implantar pacotes de R e Python arbitrários em um servidor de produção representa um desafio não familiar. Antes de adicionar pacotes, você deve avaliar se a funcionalidade fornecida pelo pacote externo é realmente necessária, sem equivalente na [linguagem R](r-libraries-and-data-types.md) interna e nas [bibliotecas do Python](../python/python-libraries-and-data-types.md) instaladas pela instalação do SQL Server. 

Como alternativa à instalação do pacote do servidor, um cientista de dados pode [criar e executar soluções em uma estação de trabalho externa](../r/set-up-a-data-science-client.md), recuperando dados de SQL Server, mas com todas as análises executadas localmente na estação de trabalho em vez de no servidor próprio. 

Se você determinar subsequentemente que as funções de biblioteca externa são necessárias e não representam um risco para operações de servidor ou dados como um todo, você pode escolher entre várias metodologias para adicionar pacotes. Na maioria dos casos, são necessários direitos de administrador para adicionar pacotes ao SQL Server. Para saber mais, confira [instalar pacotes do Python no SQL Server](../python/install-additional-python-packages-on-sql-server.md) e [instalar pacotes de R no SQL Server](install-additional-r-packages-on-sql-server.md).

> [!NOTE]
> Para pacotes de R, os direitos de administrador do servidor não são especificamente necessários para a instalação do pacote se você usar métodos alternativos. Consulte [instalar pacotes R no SQL Server](install-additional-r-packages-on-sql-server.md) para obter detalhes.

## <a name="monitoring-script-execution"></a>Monitorando a execução do script

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Os[!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] scripts de R e Python que são executados no são iniciados pela interface. No entanto, o Launchpad não é controlado por recursos ou monitorado separadamente, pois é um serviço seguro fornecido pela Microsoft que gerencia os recursos adequadamente.

Os scripts externos executados no serviço Launchpad são gerenciados usando o [objeto de trabalho do Windows](/windows/desktop/ProcThread/job-objects). Um objeto de trabalho permite que grupos de processos sejam gerenciados como uma unidade. Cada objeto de trabalho é hierárquico e controla os atributos de todos os processos associados a ele. As operações realizadas em um objeto de trabalho afetam todos os processos associados ao objeto de trabalho.

Portanto, se precisar encerrar um trabalho associado a um objeto, lembre-se de que todos os processos relacionados também serão encerrados. Se você estiver executando um script de R que é atribuído a um objeto de trabalho do Windows e esse script executa um trabalho ODBC relacionado que deve ser encerrado, o processo pai do script de R também será encerrado.

Se você iniciar um script externo que usa processamento paralelo, um único objeto de trabalho do Windows gerenciará todos os processos filho paralelos.

Para determinar se um processo está em execução em um trabalho, use a função `IsProcessInJob`.

## <a name="next-steps"></a>Próximas etapas

+ Examine os conceitos e componentes da [arquitetura de extensibilidade](../concepts/extensibility-framework.md) e [segurança](../concepts/security.md) para obter mais informações.

+ Como parte da instalação do recurso, talvez você já esteja familiarizado com o controle de acesso a dados do usuário final, mas, se não estiver, consulte [conceder permissões de usuário para SQL Server Machine Learning](../security/user-permission.md) para obter detalhes. 

+ Saiba como ajustar os recursos do sistema para cargas de trabalho de Machine Learning de computação intensiva. Para obter mais informações, consulte [como criar um pool de recursos](../administration/how-to-create-a-resource-pool.md).
