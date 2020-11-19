---
title: Arquitetura de segurança para extensibilidade
description: Este artigo descreve a arquitetura de segurança para a estrutura de extensibilidade nos Serviços de Machine Learning do SQL Server. Isso inclui segurança para as contas de usuário e logon, o serviço SQL Server Launchpad, as contas de trabalho, a execução de vários scripts e as permissões de arquivo.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.custom: contperfq1, seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: eb5ab3d1f6408bb63d194b964626bf303ba9e249
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869990"
---
# <a name="security-architecture-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>Arquitetura de segurança para a estrutura de extensibilidade nos Serviços de Machine Learning do SQL Server

[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Este artigo descreve a arquitetura de segurança usada para integrar o mecanismo de banco de dados do SQL Server e os componentes relacionados a ele com a estrutura de extensibilidade nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md). Ele examina os protegíveis, os serviços, a identidade do processo e as permissões. Os principais pontos abordados neste artigo incluem a finalidade das contas de trabalho, do launchpad e do SQLRUserGroup, o isolamento do processo de scripts externos e o modo como as identidades de usuário são mapeadas para as contas de trabalho.

Para obter mais informações sobre os principais conceitos e componentes de extensibilidade no SQL Server, confira [Arquitetura de extensibilidade no Serviços de Machine Learning do SQL Server](extensibility-framework.md).

## <a name="securables-for-external-script"></a>Protegíveis para script externo

Um script externo é enviado como um parâmetro de entrada para um [procedimento armazenado do sistema](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) criado para essa finalidade ou é encapsulado em um procedimento armazenado definido por você. O script pode ser escrito em R, Python ou em linguagens externas, como Java ou .NET. Como alternativa, você pode ter modelos que são pré-treinados e armazenados em um formato binário em uma tabela de banco de dados, chamáveis em uma função [PREDICT](../../t-sql/queries/predict-transact-sql.md) do T-SQL.

Como o script é fornecido por meio de objetos de esquema de banco de dados existentes, procedimentos armazenados e tabelas, não há nenhum novo objeto [protegível](../../relational-databases/security/securables.md) para os Serviços de Machine Learning do SQL Server.

Independentemente de como você estiver usando o script ou do que ele consistir, os objetos de banco de dados serão criados e provavelmente salvos, mas nenhum novo tipo de objeto será introduzido para armazenamento de script. Como resultado, a capacidade de consumir, criar e salvar objetos de banco de dados depende amplamente das permissões de banco de dados já definidas para os seus usuários.

<a name="permissions"></a>

## <a name="permissions"></a>Permissões

O modelo de segurança de dados do SQL Server de logons e funções de banco de dados se estende para os scripts externos. É necessário ter um logon do SQL Server ou uma conta de usuário do Windows para executar scripts externos que usam dados do SQL Server ou que são executados em um contexto de computação do SQL Server. Os usuários de banco de dados com permissões para executar uma consulta podem acessar os mesmos dados por meio do script externo.

O logon ou a conta de usuário identifica a *entidade de segurança*, a qual pode precisar de vários níveis de acesso, dependendo dos requisitos do script externo:

+ Permissão para acessar o banco de dados em que os scripts externos estão habilitados.
+ Permissões para ler dados de objetos protegidos, tais como tabelas.
+ A capacidade de gravar novos dados em uma tabela, tal como um modelo ou resultados de pontuação.
+ A capacidade de criar novos objetos, assim como tabelas, procedimentos armazenados que usam o script externo ou funções personalizadas que usam um trabalho de script externo.
+ O direito de instalar novos pacotes no computador do SQL Server ou usar pacotes fornecidos para um grupo de usuários.

Cada pessoa que executa um script externo usando SQL Server como o contexto de execução deve ser mapeada para um usuário no banco de dados. Em vez de definir individualmente permissões de usuário de banco de dados, você pode criar funções para gerenciar conjuntos de permissões e atribuir usuários a essas funções, em vez de definir permissões de usuário individualmente.

Para obter mais informações, confira [Conceder aos usuários permissão para os Serviços de Machine Learning do SQL Server](../../machine-learning/security/user-permission.md).

## <a name="permissions-when-using-an-external-client-tool"></a>Permissões ao usar uma ferramenta de cliente externo

Os usuários que estiverem usando o script em uma ferramenta de cliente externo deverão ter seu logon ou conta mapeada para um usuário no banco de dados se precisarem executar um script externo no banco de dados ou acessar dados e objetos de banco de dados. Essas mesmas permissões serão necessárias se o script externo for enviado de um cliente de ciência de dados remoto ou executado usando um procedimento armazenado T-SQL.

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

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"

## <a name="services-used-in-external-processing-launchpad"></a>Serviços usados no processamento externo (launchpad)

A estrutura de extensibilidade adiciona um novo serviço NT à [lista de serviços](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details) em uma instalação do SQL Server: [**SQL Server Launchpad (MSSSQLSERVER)**](extensibility-framework.md#launchpad).

O mecanismo de banco de dados usa o serviço SQL Server **launchpad** para instanciar uma sessão de script externo como um processo separado. 
O processo é executado sob uma conta de baixo privilégio. Essa conta é diferente do SQL Server, do Launchpad propriamente dito e da identidade do usuário sob a qual o procedimento armazenado ou a consulta de host foi executada. Executar o script em um processo separado, em uma conta de baixo privilégio, é a base do modelo de segurança e de isolamento para scripts externos no SQL Server.

O SQL Server também mantém um mapeamento da identidade do usuário que está chamando para a conta de trabalho de baixo privilégio usada para iniciar o processo de satélite. Em alguns cenários, em que o script ou o código retorna a chamada para o SQL Server para dados e operações, o SQL Server é capaz de gerenciar a transferência de identidade com perfeição. O script que contiver instruções SELECT ou funções de chamada e outros objetos de programação normalmente será bem-sucedido se o usuário de chamada tiver permissões suficientes.

> [!NOTE]
> Por padrão, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é configurado para ser executado em **NT Service\MSSQLLaunchpad**, que é provisionada com todas as permissões necessárias para executar scripts externos. Para obter mais informações sobre as opções configuráveis, confira [Configuração do serviço de launchpad do SQL Server](../security/sql-server-launchpad-service-account.md).

::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

## <a name="services-used-in-external-processing-launchpad"></a>Serviços usados no processamento externo (launchpad)

A estrutura de extensibilidade adiciona um novo serviço NT à [lista de serviços](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details) em uma instalação do SQL Server: [**Launchpad do SQL Server (MSSSQLSERVER)**](extensibility-framework.md#launchpad).

O mecanismo de banco de dados usa o serviço SQL Server **launchpad** para instanciar uma sessão de script externo como um processo separado. 
O processo é executado sob a identidade do usuário do launchpad, mas com a restrição adicional de estar contido dentro de um AppContainer. Executar o script em um processo separado, no AppContainer, é a base do modelo de segurança e de isolamento para scripts externos no SQL Server.

O SQL Server também mantém um mapeamento da identidade do usuário que está chamando para a conta de trabalho de baixo privilégio usada para iniciar o processo de satélite. Em alguns cenários, em que o script ou o código retorna a chamada para o SQL Server para dados e operações, o SQL Server é capaz de gerenciar a transferência de identidade com perfeição. O script que contiver instruções SELECT ou funções de chamada e outros objetos de programação normalmente será bem-sucedido se o usuário de chamada tiver permissões suficientes.

> [!NOTE]
> Por padrão, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] é configurado para ser executado em **NT Service\MSSQLLaunchpad**, que é provisionada com todas as permissões necessárias para executar scripts externos. Para obter mais informações sobre as opções configuráveis, confira [Configuração do serviço de launchpad do SQL Server](../security/sql-server-launchpad-service-account.md).

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

## <a name="services-used-in-external-processing"></a>Serviços usados no processamento externo

A estrutura de extensibilidade adiciona um novo daemon em uma instalação do SQL Server: [mssql-launchpadd](extensibility-framework.md#launchpad). mssql-launchpadd é executado sob a conta de privilégios baixos mssql_launchpadd criada quando o pacote mssql-server-extensibility é instalado.

Há suporte para apenas uma instância do mecanismo de banco de dados e há um serviço de launchpadd associado à instância. Quando um script é executado, o serviço de launchpadd inicia um processo do launchpad separado com a conta de usuário com poucos privilégios mssql_satellite no próprio novo namespace de rede, montagem, IPC e PID. Cada processo satélite herda a conta de usuário mssql_satellite e usa essa conta durante a execução do script.

Para obter mais informações, confira [Arquitetura de extensibilidade no Serviços de Machine Learning do SQL Server](extensibility-framework.md).

::: moniker-end

<a name="sqlrusergroup"></a>

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"

## <a name="identities-used-in-processing-sqlrusergroup"></a>Identidades usadas no processamento (SQLRUserGroup)

O **SQLRUserGroup** (grupo de usuários ocm restrições do SQL) é criado pela instalação do SQL Server e contém um pool de contas de usuário locais do Windows com privilégios baixos. Quando um processo externo é necessário, o launchpad usa uma conta de trabalho disponível e a usa para executar um processo. Mais especificamente, o launchpad ativa uma conta de trabalho disponível, mapeia-a para a identidade do usuário de chamada e executa o script na conta de trabalho.

+ O **SQLRUserGroup** está vinculado a uma instância específica. Um pool separado de contas de trabalho é necessário para cada instância em que o aprendizado de máquina foi habilitado. Contas não podem ser compartilhadas entre instâncias.

+ O tamanho do pool de conta de usuário é estático e o valor padrão é 20, o que dá suporte a 20 sessões simultâneas. O número de sessões de runtime externas que podem ser iniciadas simultaneamente é limitado pelo tamanho desse pool de conta de usuário. 

+ Os nomes de conta de trabalho no pool estão no formato SQLInstanceName *nn*. Por exemplo, em uma instância padrão, **SQLRUserGroup** contém contas chamadas MSSQLSERVER01, MSSQLSERVER02 e assim por diante, até MSSQLSERVER20.

As tarefas paralelizadas não consomem contas adicionais. Por exemplo, se um usuário executar uma tarefa de pontuação que usa processamento paralelo, a mesma conta de trabalho será reutilizada para todos os threads. Se pretende fazer uso intensivo do aprendizado de máquina, você pode aumentar o número de contas usadas para executar scripts externos. Para obter mais informações, confira a [execução simultânea da escala de scripts externos nos Serviços de Machine Learning do SQL Server](../../machine-learning/administration/scale-concurrent-execution-external-scripts.md).

### <a name="permissions-granted-to-sqlrusergroup"></a>Permissões concedidas a SQLRUserGroup

Por padrão, os membros do **SQLRUserGroup** têm permissões de leitura e de execução em executáveis nos seguintes diretórios SQL Server: **Binn**, **R_SERVICES** e **PYTHON_SERVICES**. Isso inclui o acesso a executáveis, bibliotecas e conjuntos de arquivos internos nas distribuições do R e do Python instaladas com o SQL Server. 

Para proteger recursos confidenciais no SQL Server, você pode, opcionalmente, definir uma ACL (lista de controle de acesso) que nega acesso ao **SQLRUserGroup**. Por outro lado, você também pode conceder permissões a recursos de dados locais que existem no computador host, além do SQL Server propriamente dito. 

Por design, **SQLRUserGroup** não tem um logon de banco de dados nem permissões para nenhum dado. Em determinadas circunstâncias, talvez você queira criar um logon para permitir conexões de loopback, especialmente quando uma identidade confiável do Windows é o usuário de chamada. Essa funcionalidade é chamada de [*autenticação implícita*](#implied-authentication). Para obter mais informações, confira [Adicionar SQLRUserGroup como um usuário de banco de dados](../../machine-learning/security/create-a-login-for-sqlrusergroup.md).

## <a name="identity-mapping"></a>Mapeamento de identidade

Quando uma sessão é iniciada, o launchpad mapeia a identidade do usuário de chamada para uma conta de trabalho. O mapeamento de um usuário externo do Windows ou logon SQL válido para uma conta de trabalho é válido somente pelo tempo de vida do procedimento armazenado do SQL que executa o script externo. Consultas paralelas do mesmo logon são mapeadas para a mesma conta de trabalho do usuário.

Durante a execução, o launchpad cria pastas temporárias para armazenar dados de sessão, excluindo-os quando a sessão termina. O acesso aos diretórios é restrito. No R, o RLauncher executa essa tarefa. No Python, o PythonLauncher executa essa tarefa. Cada conta de trabalho individual é restrita à sua própria pasta e não pode acessar arquivos em pastas acima do seu próprio nível. No entanto, a conta de trabalho pode ler, gravar ou excluir filhos contidos na pasta de trabalho de sessão que foi criada. Se você for um administrador no computador, você poderá exibir os diretórios criados para cada processo. Cada diretório é identificado por seu GUID de sessão.

::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

## <a name="appcontainer-isolation"></a>Isolamento do AppContainer

O isolamento é obtido por meio de [AppContainers](/windows/desktop/secauthz/appcontainer-isolation). No tempo de execução, quando um script externo é detectado em um procedimento armazenado ou consulta, o SQL Server chama o launchpad com uma solicitação para um inicializador específico a uma extensão. O Launchpad invoca o ambiente de runtime apropriado em um processo sob sua identidade e instancia um AppContainer para contê-lo. Essa alteração é benéfica porque o gerenciamento de conta local e de senha não é mais necessário. Além disso, em instalações em que as contas de usuário local são proibidas, a eliminação da dependência de conta de usuário local significa que agora você pode usar esse recurso.

Conforme implementado pelo SQL Server, os AppContainers são um mecanismo interno. Embora você não veja evidências físicas de AppContainers no monitor de processos, pode encontrá-las em regras de firewall de saída criadas pela instalação para impedir que processos façam chamadas de rede. Para obter mais informações, confira [Configuração de firewall para os Serviços de Machine Learning do SQL Server](../../machine-learning/security/firewall-configuration.md).

## <a name="identity-mapping"></a>Mapeamento de identidade

Quando uma sessão é iniciada, o launchpad mapeia a identidade do usuário de chamada para um **AppContainer**.

> [!Note]
> No SQL Server 2019 e posteriores, o **SQLRUserGroup** tem apenas um membro que agora é a única conta de serviço de launchpad do SQL Server, em vez de várias contas de trabalho.

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

## <a name="identity-mapping"></a>Mapeamento de identidade

O daemon do **Launchpadd** (dois "d": [mssql-launchpadd](extensibility-framework.md#launchpad)) mapeia a identidade do usuário que está chamando para um processo de **launchpad** separado (um "d") com uma pasta "GUID do launchpad" e um certificado satélite. Essas pastas de GUID do launchpad são criadas em `/var/opt/mssql-extensibility/data/`. O processo do launchpad usa esse certificado para autenticar-se novamente no SQL e, em seguida, cria pastas temporárias para cada GUID de sessão na pasta GUID do launchpad. O processo satélite (R, Python ou ExtHost) pode acessar a pasta GUID do launchpad, o certificado abaixo dele e sua pasta GUID de sessão.

O script SQL a seguir imprime o conteúdo das pastas do launchpad.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    ,@script = N'
print("Contents of /var/opt/mssql-extensibility/data :");
print(system("ls -al /var/opt/mssql-extensibility/data"));
print("Contents of Launchpad GUID folder:");
print(system("ls -al /var/opt/mssql-extensibility/data/*"));
print(system("ls -al /var/opt/mssql-extensibility/data/*/*"))
'
    ,@input_data_1 = N'SELECT 1 AS hello'
```

::: moniker-end

<a name="implied-authentication"></a>

::: moniker range="=sql-server-2016||=sql-server-2017||=sqlallproducts-allversions"

## <a name="implied-authentication-loopback-requests"></a>Autenticação implícita (solicitações de loopback)

*A autenticação implícita* descreve o comportamento de solicitação de conexão sob o qual processos externos, em execução como contas de trabalho com privilégios baixos, são apresentados como uma identidade de usuário confiável para o SQL Server em solicitações de loopback para dados ou operações. Como um conceito, a autenticação implícita é exclusiva da autenticação do Windows, em cadeias de conexão do SQL Server que especificam uma conexão confiável, em solicitações originadas de processos externos, tais como o script R ou Python. Às vezes, isso também é chamado de *loopback*.

As conexões confiáveis podem ser utilizadas do script externo, mas apenas com uso de configuração adicional. Na arquitetura de extensibilidade, os processos externos são executados em contas de trabalho, herdando permissões do **SQLRUserGroup** pai. Quando uma cadeia de conexão especifica `Trusted_Connection=True`, a identidade da conta de trabalho é apresentada na solicitação de conexão, que é desconhecida por padrão para o SQL Server.

Para que as conexões confiáveis sejam bem-sucedidas, você deve criar um logon de banco de dados para o **SQLRUserGroup**. Depois de fazer isso, qualquer conexão confiável de qualquer membro de **SQLRUserGroup** tem direitos de logon para o SQL Server. Para obter instruções detalhadas, confira [Adicionar SQLRUserGroup a um logon de banco de dados](../../machine-learning/security/create-a-login-for-sqlrusergroup.md).

As conexões confiáveis não são a formulação mais amplamente usada de uma solicitação de conexão. Quando o script externo especifica uma conexão, caso essa conexão seja para uma fonte de dados ODBC, pode ser mais comum usar um logon do SQL ou um nome de usuário e senha totalmente especificados.

### <a name="how-implied-authentication-works-for-external-script-sessions"></a>Como funciona a autenticação implícita para sessões de script externo

O diagrama a seguir mostra a interação dos componentes do SQL Server com o runtime da linguagem e como ele faz a autenticação implícita no Windows.

![Autenticação implícita no Windows](../security/media/implied-auth-windows-2017.png)

::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

## <a name="implied-authentication-loopback-requests"></a>Autenticação implícita (solicitações de loopback)

*A autenticação implícita* descreve o comportamento de solicitação de conexão sob o qual processos externos em execução sob AppContainers são apresentados como uma identidade de usuário confiável para o SQL Server em solicitações de loopback para dados ou operações. Como um conceito, a autenticação implícita não é exclusiva da autenticação do Windows, em cadeias de conexão do SQL Server que especificam uma conexão confiável, em solicitações originadas de processos externos, tais como o script R ou Python. Às vezes, isso também é chamado de *loopback*.

Ao gerenciar identidade e credenciais, o AppContainer impede o uso de credenciais do usuário para obter acesso a recursos ou fazer logon em outros ambientes. O ambiente do AppContainer cria um identificador que usa as identidades combinadas do usuário e do aplicativo, portanto, as credenciais são exclusivas para cada emparelhamento de usuário/aplicativo e o aplicativo não pode representar o usuário. Para obter mais informações, confira [Isolamento do AppContainer](/windows/win32/secauthz/appcontainer-isolation).

Para obter mais detalhes sobre conexões de loopback, confira [Conexão de loopback para o SQL Server de um script Python ou R](../connect/loopback-connection.md).

### <a name="how-implied-authentication-works-for-external-script-sessions"></a>Como funciona a autenticação implícita para sessões de script externo

O diagrama a seguir mostra a interação dos componentes do SQL Server com o runtime da linguagem e como ele faz a autenticação implícita no Windows.

![Autenticação implícita no Windows](../security/media/implied-auth-windows.png)

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

## <a name="implied-authentication-loopback-requests"></a>Autenticação implícita (solicitações de loopback)

*A autenticação implícita* descreve o comportamento de solicitação de conexão sob o qual processos externos em execução como usuários do mssql_satellite com privilégios baixos nos próprios namespaces são apresentados como uma identidade de usuário confiável para o SQL Server em solicitações de loopback para dados ou operações. Às vezes, isso também é chamado de loopback.

Uma conexão de loopback é obtida usando o certificado satélite da pasta do GUID do launchpad para fazer a autenticação de volta para o SQL Server pelo processo de satélite. A identidade do usuário de chamada é mapeada para esse certificado e, portanto, o processo de satélite que se conecta de volta ao SQL Server usando o certificado pode ser mapeado de volta para o usuário de chamada.

Para obter mais informações, confira [Conexão de loopback para o SQL Server de um script Python ou R](../connect/loopback-connection.md).

### <a name="how-implied-authentication-works-for-external-script-sessions"></a>Como funciona a autenticação implícita para sessões de script externo

O diagrama a seguir mostra a interação dos componentes do SQL Server com o runtime da linguagem e como ele faz a autenticação implícita no Linux.

![Autenticação implícita no Linux](../security/media/implied-auth-linux.png)

::: moniker-end

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>Não há suporte para Transparent Data Encryption em repouso

A [TDE (Transparent Data Encryption)](../../relational-databases/security/encryption/transparent-data-encryption.md) não é compatível com os dados enviados para um runtime de script externo ou recebidos de um runtime desse tipo. O motivo é que o processo externo é executado fora do processo do SQL Server. Portanto, os dados usados pelo runtime externo não são protegidos pelos recursos de criptografia do mecanismo de banco de dados. Esse comportamento não é diferente de nenhum outro cliente em execução no computador do SQL Server que lê dados do banco de dados e faz uma cópia.

Como consequência, o TDE **não será** aplicado a nenhum dado que você usar em scripts externos, a nenhum dado salvo em disco e a nenhum resultado intermediário persistente. No entanto, outros tipos de criptografia, tais como criptografia BitLocker do Windows ou criptografia de terceiros aplicada no nível de arquivo ou de pasta, ainda se aplicam.

No caso do [Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md), os runtimes externos não têm acesso às chaves de criptografia. Portanto, os dados não podem ser enviados para os scripts.

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você aprendeu quais são os componentes e o modelo de interação da arquitetura de segurança criada na [estrutura de extensibilidade](../../machine-learning/concepts/extensibility-framework.md). Os principais pontos abordados neste artigo incluem a finalidade das contas de trabalho, do launchpad e do SQLRUserGroup, o isolamento do processo de scripts externos e o modo como as identidades de usuário são mapeadas para as contas de trabalho. 

Como uma próxima etapa, examine as instruções para [conceder permissões](../../machine-learning/security/user-permission.md). Para servidores que usam a autenticação do Windows, você também deve examinar [Adicionar um SQLRUserGroup a um logon de banco de dados](../../machine-learning/security/create-a-login-for-sqlrusergroup.md) para saber quando uma configuração adicional é necessária.