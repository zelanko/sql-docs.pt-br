---
title: Visão geral de segurança para extensibilidade
description: Visão geral de segurança para a estrutura de extensibilidade nos Serviços de Machine Learning do SQL Server. Segurança para contas de usuário e logon, SQL Server Launchpad serviço, contas de trabalho, execução de vários scripts e permissões de arquivo.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f2e2d696a09e5b5bb321da583efd76f580759ce6
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78338889"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>Visão geral de segurança para a estrutura de extensibilidade nos Serviços de Machine Learning do SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este artigo descreve a arquitetura de segurança geral usada para integrar o mecanismo de banco de dados do SQL Server e os componentes relacionados a ele com a estrutura de extensibilidade. Ele examina os protegíveis, os serviços, a identidade do processo e as permissões. Para obter mais informações sobre os principais conceitos e componentes de extensibilidade no SQL Server, confira [Arquitetura de extensibilidade no Serviços de Machine Learning do SQL Server](extensibility-framework.md)].

## <a name="securables-for-external-script"></a>Protegíveis para script externo

Um script externo escrito em R ou Python é enviado como um parâmetro de entrada para um [procedimento armazenado do sistema](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) criado para essa finalidade ou é encapsulado em um procedimento armazenado definido por você. Como alternativa, você pode ter modelos que são pré-treinados e armazenados em um formato binário em uma tabela de banco de dados, chamáveis em uma função [PREDICT](../../t-sql/queries/predict-transact-sql.md) do T-SQL.

Como o script é fornecido por meio de objetos de esquema de banco de dados existentes, procedimentos armazenados e tabelas, não há nenhum novo objeto [protegível](../../relational-databases/security/securables.md) para os Serviços de Machine Learning do SQL Server.

Independentemente de como você estiver usando o script ou do que ele consistir, os objetos de banco de dados serão criados e provavelmente salvos, mas nenhum novo tipo de objeto será introduzido para armazenamento de script. Como resultado, a capacidade de consumir, criar e salvar objetos de banco de dados depende amplamente das permissões de banco de dados já definidas para os seus usuários.

<a name="permissions"></a>

## <a name="permissions"></a>Permissões

O modelo de segurança de dados do SQL Server de logons e funções de banco de dados se estende para o script R e Python. É necessário ter um logon do SQL Server ou uma conta de usuário do Windows para executar scripts externos que usam dados do SQL Server ou que são executados em um contexto de computação do SQL Server. Os usuários de banco de dados com permissões para executar uma consulta ad hoc podem acessar os mesmos dados por meio do script R ou Python.

O logon ou a conta de usuário identifica a *entidade de segurança*, a qual pode precisar de vários níveis de acesso, dependendo dos requisitos do script externo:

+ Permissão para acessar o banco de dados em que os scripts externos estão habilitados.
+ Permissões para ler dados de objetos protegidos, tais como tabelas.
+ A capacidade de gravar novos dados em uma tabela, tal como um modelo ou resultados de pontuação.
+ A capacidade de criar novos objetos, assim como tabelas, procedimentos armazenados que usam o script externo ou funções personalizadas que usam um trabalho de R ou Python.
+ O direito de instalar novos pacotes no computador do SQL Server ou usar pacotes fornecidos para um grupo de usuários.

Cada pessoa que executa um script externo usando SQL Server como o contexto de execução deve ser mapeada para um usuário no banco de dados. Em vez de definir individualmente permissões de usuário de banco de dados, você pode criar funções para gerenciar conjuntos de permissões e atribuir usuários a essas funções, em vez de definir permissões de usuário individualmente.

Para obter mais informações, confira [Conceder aos usuários permissão para os Serviços de Machine Learning do SQL Server](../../advanced-analytics/security/user-permission.md).

## <a name="permissions-when-using-an-external-client-tool"></a>Permissões ao usar uma ferramenta de cliente externo

Os usuários que estiverem usando o R ou o Python em uma ferramenta de cliente externo deverão ter seu logon ou conta mapeada para um usuário no banco de dados se precisarem executar um script externo no banco de dados ou acessar dados e objetos de banco de dados. Essas mesmas permissões serão necessárias se o script externo for enviado de um cliente de ciência de dados remoto ou executado usando um procedimento armazenado T-SQL.

Por exemplo, suponha que você criou um script externo que é executado em seu computador local e você deseja executar esse script no SQL Server. Você deve certificar-se de que as seguintes condições sejam atendidas:

+ O banco de dados permite conexões remotas.
+ A conta do Windows ou o logon do SQL que você usou para acesso ao banco de dados foi adicionado ao SQL Server no nível da instância.
+ O logon SQL ou o usuário do Windows deve ter permissão para executar scripts externos. Em geral, essa permissão só pode ser adicionada por um administrador de banco de dados.
+ O logon SQL ou o usuário do Windows deverá ser adicionado como um usuário, com as permissões apropriadas, em cada banco de dados em que o script externo realiza qualquer uma destas operações:
  + Recuperação de dados.
  + Gravação ou atualização de dados.
  + Criação de novos objetos, tais como tabelas ou procedimentos armazenados.

Depois que a conta de usuário do Windows ou o logon tiver sido provisionado e tiver as permissões necessárias, você poderá executar um script externo no SQL Server usando um objeto de fonte de dados no R ou a biblioteca **revoscalepy** no Python ou então chamando um procedimento armazenado que contenha o script externo.

Sempre que um script externo for iniciado do SQL Server, a segurança do mecanismo de banco de dados obtém o contexto de segurança do usuário que iniciou o trabalho e gerencia os mapeamentos do usuário ou logon para objetos protegíveis.

Portanto, todos os scripts externos iniciados de um cliente remoto devem especificar as informações de logon ou usuário como parte da cadeia de conexão.

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>Serviços usados no processamento externo (Launchpad)

A estrutura de extensibilidade adiciona um novo serviço NT à [lista de serviços](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details) em uma instalação do SQL Server: [**SQL Server Launchpad (MSSSQLSERVER)** ](extensibility-framework.md#launchpad).

O mecanismo de banco de dados usa o serviço SQL Server Launchpad para instanciar uma sessão do R ou do Python como um processo separado. O processo é executado em uma conta com privilégios baixos e de modo distinto do SQL Server, do Launchpad propriamente dito e da identidade do usuário sob a qual o procedimento armazenado ou a consulta de host foi executada. Executar o script em um processo separado, em uma conta de privilégios baixos, é a base do modelo de segurança e de isolamento para R e Python no SQL Server.

Além de iniciar processos externos, o Launchpad também é responsável por acompanhar a identidade do usuário de chamada e mapear essa identidade para a conta de trabalho com privilégios baixos usada para iniciar o processo. Em alguns cenários, em que o script ou o código retorna a chamada para o SQL Server para dados e operações, o Launchpad geralmente é capaz de gerenciar a transferência de identidade com perfeição. O script que contiver instruções SELECT ou funções de chamada e outros objetos de programação normalmente será bem-sucedido se o usuário de chamada tiver permissões suficientes.

> [!NOTE]
> Por padrão, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é configurado para ser executado em **NT Service\MSSQLLaunchpad**, que é provisionada com todas as permissões necessárias para executar scripts externos. Para obter mais informações sobre as opções configuráveis, confira [Configuração do serviço SQL Server Launchpad](../security/sql-server-launchpad-service-account.md).

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>Identidades usadas no processamento (SQLRUserGroup)

O **SQLRUserGroup** (grupo de usuários ocm restrições do SQL) é criado pela instalação do SQL Server e contém um pool de contas de usuário locais do Windows com privilégios baixos. Quando um processo externo é necessário, o Launchpad usa uma conta de trabalho disponível e a usa para executar um processo. Mais especificamente, o Launchpad ativa uma conta de trabalho disponível, mapeia-a para a identidade do usuário de chamada e executa o script na conta de trabalho.

+ O **SQLRUserGroup** está vinculado a uma instância específica. Um pool separado de contas de trabalho é necessário para cada instância em que o aprendizado de máquina foi habilitado. Contas não podem ser compartilhadas entre instâncias.

+ O tamanho do pool de conta de usuário é estático e o valor padrão é 20, o que dá suporte a 20 sessões simultâneas. O número de sessões de runtime externas que podem ser iniciadas simultaneamente é limitado pelo tamanho desse pool de conta de usuário. 

+ Os nomes de conta de trabalho no pool estão no formato SQLInstanceName*nn*. Por exemplo, em uma instância padrão, **SQLRUserGroup** contém contas chamadas MSSQLSERVER01, MSSQLSERVER02 e assim por diante, até MSSQLSERVER20.

As tarefas paralelizadas não consomem contas adicionais. Por exemplo, se um usuário executar uma tarefa de pontuação que usa processamento paralelo, a mesma conta de trabalho será reutilizada para todos os threads. Se pretende fazer uso intensivo do aprendizado de máquina, você pode aumentar o número de contas usadas para executar scripts externos. Para saber mais, confira [Modificar o pool de contas de usuário para o aprendizado de máquina](../../advanced-analytics/administration/modify-user-account-pool.md).

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>Isolamento do AppContainer no SQL Server 2019

No SQL Server 2019, a instalação não cria mais contas de trabalho para **SQLRUserGroup**. Em vez disso, o isolamento é obtido por meio de [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). No tempo de execução, quando um script externo é detectado em um procedimento armazenado ou consulta, o SQL Server chama o Launchpad com uma solicitação para um inicializador específico a uma extensão. O Launchpad invoca o ambiente de runtime apropriado em um processo sob sua identidade e instancia um AppContainer para contê-lo. Essa alteração é benéfica porque o gerenciamento de conta local e de senha não é mais necessário. Além disso, em instalações em que as contas de usuário local são proibidas, a eliminação da dependência de conta de usuário local significa que agora você pode usar esse recurso.

Conforme implementado pelo SQL Server, os AppContainers são um mecanismo interno. Embora você não veja evidências físicas de AppContainers no monitor de processos, pode encontrá-las em regras de firewall de saída criadas pela instalação para impedir que processos façam chamadas de rede. Para obter mais informações, confira [Configuração de firewall para os Serviços de Machine Learning do SQL Server](../../advanced-analytics/security/firewall-configuration.md).

> [!Note]
> No SQL Server 2019, **SQLRUserGroup** tem apenas um membro que agora é a única conta de serviço do SQL Server Launchpad, em vez de várias contas de trabalho.
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>Permissões concedidas a SQLRUserGroup

Por padrão, os membros de **SQLRUserGroup** têm permissões de leitura e de execução em arquivos nos diretórios **Binn**, **R_SERVICES** e **PYTHON_SERVICES** do SQL Server, com acesso a executáveis, bibliotecas e conjuntos de dados internos nas distribuições do R e do Python instaladas com o SQL Server. 

Para proteger recursos confidenciais no SQL Server, você pode, opcionalmente, definir uma ACL (lista de controle de acesso) que nega acesso ao **SQLRUserGroup**. Por outro lado, você também pode conceder permissões a recursos de dados locais que existem no computador host, além do SQL Server propriamente dito. 

Por design, **SQLRUserGroup** não tem um logon de banco de dados nem permissões para nenhum dado. Em determinadas circunstâncias, talvez você queira criar um logon para permitir conexões de loopback, especialmente quando uma identidade confiável do Windows é o usuário de chamada. Essa funcionalidade é chamada de [*autenticação implícita*](#implied-authentication). Para obter mais informações, confira [Adicionar SQLRUserGroup como um usuário de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

## <a name="identity-mapping"></a>Mapeamento de identidade

Quando uma sessão é iniciada, o Launchpad mapeia a identidade do usuário de chamada para uma conta de trabalho. O mapeamento de um usuário externo do Windows ou logon SQL válido para uma conta de trabalho é válido somente pelo tempo de vida do procedimento armazenado do SQL que executa o script externo. Consultas paralelas do mesmo logon são mapeadas para a mesma conta de trabalho do usuário.

Durante a execução, o Launchpad cria pastas temporárias para armazenar dados de sessão, excluindo-os quando a sessão termina. O acesso aos diretórios é restrito. No R, o RLauncher executa essa tarefa. No Python, o PythonLauncher executa essa tarefa. Cada conta de trabalho individual é restrita à sua própria pasta e não pode acessar arquivos em pastas acima do seu próprio nível. No entanto, a conta de trabalho pode ler, gravar ou excluir filhos contidos na pasta de trabalho de sessão que foi criada. Se você for um administrador no computador, você poderá exibir os diretórios criados para cada processo. Cada diretório é identificado por seu GUID de sessão.

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>Autenticação implícita (solicitações de loopback)

*A autenticação implícita* descreve o comportamento de solicitação de conexão sob o qual processos externos, em execução como contas de trabalho com privilégios baixos, são apresentados como uma identidade de usuário confiável para o SQL Server em solicitações de loopback para dados ou operações. Como um conceito, a autenticação implícita é exclusiva da autenticação do Windows, em cadeias de conexão do SQL Server que especificam uma conexão confiável, em solicitações originadas de processos externos, tais como o script R ou Python. Às vezes, isso também é chamado de *loopback*.

As conexões confiáveis podem ser utilizadas do script R e Python, mas apenas com uso de configuração adicional. Na arquitetura de extensibilidade, os processos do R e do Python são executados em contas de trabalho, herdando permissões do **SQLRUserGroup** pai. Quando uma cadeia de conexão especifica `Trusted_Connection=True`, a identidade da conta de trabalho é apresentada na solicitação de conexão, que é desconhecida por padrão para o SQL Server.

Para que as conexões confiáveis sejam bem-sucedidas, você deve criar um logon de banco de dados para o **SQLRUserGroup**. Depois de fazer isso, qualquer conexão confiável de qualquer membro de **SQLRUserGroup** tem direitos de logon para o SQL Server. Para obter instruções detalhadas, confira [Adicionar SQLRUserGroup a um logon de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

As conexões confiáveis não são a formulação mais amplamente usada de uma solicitação de conexão. Quando o script R ou Python especifica uma conexão, caso essa conexão seja para uma fonte de dados ODBC, pode ser mais comum usar um logon do SQL ou um nome de usuário e senha totalmente especificados.

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>Como a autenticação implícita funciona para sessões do R e do Python

O diagrama a seguir mostra a interação dos componentes do SQL Server com o runtime do R e como ele faz a autenticação implícita para o R.

![Autenticação implícita para o R](../security/media/implied-auth-rsql.png)

O diagrama a seguir mostra a interação dos componentes do SQL Server com o runtime do Python e como ele faz a autenticação implícita para o Python.

![Autenticação implícita para o Python](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>Não há suporte para Transparent Data Encryption em repouso

A [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md) não é compatível com os dados enviados para um runtime de script externo ou recebidos de um runtime desse tipo. O motivo é que o processo externo (R ou Python) é executado fora do processo do SQL Server. Portanto, os dados usados pelo runtime externo não são protegidos pelos recursos de criptografia do mecanismo de banco de dados. Esse comportamento não é diferente de nenhum outro cliente em execução no computador do SQL Server que lê dados do banco de dados e faz uma cópia.

Como consequência, o TDE **não será** aplicado a nenhum dado que você usar em scripts de R ou Python, a nenhum dado salvo em disco e a nenhum resultado intermediário persistente. No entanto, outros tipos de criptografia, tais como criptografia BitLocker do Windows ou criptografia de terceiros aplicada no nível de arquivo ou de pasta, ainda se aplicam.

No caso do [Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md), os runtimes externos não têm acesso às chaves de criptografia. Portanto, os dados não podem ser enviados para os scripts.

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você aprendeu quais são os componentes e o modelo de interação da arquitetura de segurança criada na [estrutura de extensibilidade](../../advanced-analytics/concepts/extensibility-framework.md). Os principais pontos abordados neste artigo incluem a finalidade das contas de trabalho, do Launchpad e do SQLRUserGroup, o isolamento do processo do R e do Python e o modo como as identidades de usuário são mapeadas para as contas de trabalho. 

Como uma próxima etapa, examine as instruções para [conceder permissões](../../advanced-analytics/security/user-permission.md). Para servidores que usam a autenticação do Windows, você também deve examinar [Adicionar um SQLRUserGroup a um logon de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md) para saber quando uma configuração adicional é necessária.