---
title: Visão geral de segurança para extensões R e Python
description: Visão geral de segurança para a estrutura de extensibilidade no SQL Server Serviços de Machine Learning. Segurança para contas de usuário e logon, SQL Server Launchpad serviço, contas de trabalho, executando vários scripts e permissões de arquivo.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 51587878d4a16145ff53eaa397da69130c04d7d5
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343366"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>Visão geral de segurança para a estrutura de extensibilidade no SQL Server Serviços de Machine Learning

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve a arquitetura de segurança geral usada para integrar o mecanismo de banco de dados SQL Server e os componentes relacionados com a estrutura de extensibilidade. Ele examina os protegíveis, os serviços, a identidade do processo e as permissões. Para obter mais informações sobre os principais conceitos e componentes de extensibilidade no SQL Server, consulte [arquitetura de extensibilidade no SQL Server serviços de Machine Learning](extensibility-framework.md)].

## <a name="securables-for-external-script"></a>Protegíveis para script externo

Um script externo escrito em R ou Python é enviado como um parâmetro de entrada para um [procedimento armazenado do sistema](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) criado para essa finalidade ou é encapsulado em um procedimento armazenado que você define. Como alternativa, você pode ter modelos que são previamente treinados e armazenados em um formato binário em uma tabela de banco de dados, que podem ser chamados em uma função de [previsão](../../t-sql/queries/predict-transact-sql.md) de T-SQL.

Como o script é fornecido por meio de objetos de esquema de banco de dados existentes, procedimentos armazenados e tabelas, não há novos [protegíveis](../../relational-databases/security/securables.md) para SQL Server serviços de Machine Learning.

Independentemente de como você estiver usando script ou o que consistem, os objetos de banco de dados serão criados e provavelmente salvos, mas nenhum novo tipo de objeto será introduzido para o armazenamento de script. Como resultado, a capacidade de consumir, criar e salvar objetos de banco de dados depende amplamente das permissões de banco de dados já definidas para seus usuários.

<a name="permissions"></a>

## <a name="permissions"></a>Permissões

O modelo de segurança de dados do SQL Server de logons e funções de banco de dado se estende para o script R e Python. Um logon SQL Server ou conta de usuário do Windows é necessário para executar scripts externos que usam SQL Server dados ou que são executados com SQL Server como o contexto de computação. Os usuários de banco de dados com permissões para executar uma consulta ad hoc podem acessar os mesmos dados do script R ou Python.

O logon ou a conta de usuário identifica a *entidade de segurança*, que pode precisar de vários níveis de acesso, dependendo dos requisitos de script externo:

+ Permissão para acessar o banco de dados em que os scripts externos estão habilitados.
+ Permissões para ler dados de objetos protegidos, como tabelas.
+ A capacidade de gravar novos dados em uma tabela, como um modelo ou resultados de pontuação.
+ A capacidade de criar novos objetos, como tabelas, procedimentos armazenados que usam o script externo ou funções personalizadas que usam o trabalho de R ou Python.
+ O direito de instalar novos pacotes no computador SQL Server ou usar pacotes fornecidos para um grupo de usuários.

Cada pessoa que executa um script externo usando SQL Server como o contexto de execução deve ser mapeada para um usuário no banco de dados. Em vez de definir individualmente permissões de usuário de banco de dados, você pode criar funções para gerenciar conjuntos de permissões e atribuir usuários a essas funções, em vez de definir permissões de usuário individualmente.

Para obter mais informações, consulte [conceder aos usuários permissão para SQL Server serviços de Machine Learning](../../advanced-analytics/security/user-permission.md).

## <a name="permissions-when-using-an-external-client-tool"></a>Permissões ao usar uma ferramenta de cliente externo

Os usuários que estiverem usando o R ou o Python em uma ferramenta de cliente externo deverão ter seu logon ou conta mapeada para um usuário no banco de dados se precisarem executar um script externo no banco de dados, ou acessar objetos de banco de dados e os mesmos. As mesmas permissões são necessárias se o script externo for enviado de um cliente de ciência de dados remoto ou executado usando um procedimento armazenado T-SQL.

Por exemplo, suponha que você criou um script externo que é executado em seu computador local e deseja executar esse script em SQL Server. Você deve certificar-se de que as seguintes condições sejam atendidas:

+ O banco de dados permite conexões remotas.
+ O logon do SQL ou a conta do Windows que você usou para acesso ao banco de dados foi adicionado ao SQL Server no nível da instância.
+ O logon do SQL ou o usuário do Windows deve ter a permissão para executar scripts externos. Em geral, essa permissão só pode ser adicionada por um administrador de banco de dados.
+ O logon do SQL ou o usuário da janela deve ser adicionado como um usuário, com as permissões apropriadas, em cada banco de dados em que o script externo executa qualquer uma dessas operações:
  + Recuperando dados.
  + Gravando ou atualizando dados.
  + Criar novos objetos, como tabelas ou procedimentos armazenados.

Depois que o logon ou a conta de usuário do Windows tiver sido provisionado e receber as permissões necessárias, você poderá executar um script externo em SQL Server usando um objeto de fonte de dados no R ou a biblioteca **revoscalepy** no Python ou chamando um procedimento armazenado que contém o script externo.

Sempre que um script externo é iniciado a partir de SQL Server, a segurança do mecanismo de banco de dados Obtém o contexto de segurança do usuário que iniciou o trabalho e gerencia os mapeamentos do usuário ou logon em objetos protegíveis.

Portanto, todos os scripts externos que são iniciados a partir de um cliente remoto devem especificar as informações de logon ou de usuário como parte da cadeia de conexão.

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>Serviços usados no processamento externo (Launchpad)

A estrutura de extensibilidade adiciona um novo serviço NT à [lista de serviços](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details) em uma instalação SQL Server: [**SQL Server Launchpad (MSSSQLSERVER)** ](extensibility-framework.md#launchpad).

O mecanismo de banco de dados usa o serviço de SQL Server Launchpad para instanciar uma sessão R ou Python como um processo separado. O processo é executado sob uma conta de baixo privilégio; DISTINCT de SQL Server, Launchpad em si e a identidade do usuário sob a qual o procedimento armazenado ou a consulta de host foi executada. Executar o script em um processo separado, sob conta de baixo privilégio, é a base do modelo de segurança e isolamento para R e Python no SQL Server.

Além de iniciar processos externos, o Launchpad também é responsável por rastrear a identidade do usuário que está chamando e mapear essa identidade para a conta de trabalho de baixo privilégio usada para iniciar o processo. Em alguns cenários, em que o script ou o código chama de volta para SQL Server para dados e operações, o Launchpad geralmente é capaz de gerenciar a transferência de identidade de forma direta. O script que contém instruções SELECT ou funções de chamada e outros objetos de programação normalmente terá sucesso se o usuário que está chamando tiver permissões suficientes.

> [!NOTE]
> Por padrão, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] o é configurado para ser executado em **NT Service\MSSQLLaunchpad**, que é provisionado com todas as permissões necessárias para executar scripts externos. Para obter mais informações sobre as opções configuráveis, consulte [SQL Server Launchpad Service Configuration](../security/sql-server-launchpad-service-account.md).

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>Identidades usadas no processamento (SQLRUserGroup)

**SQLRUserGroup** (Grupo de usuários restritos do SQL) é criado pela instalação do SQL Server e contém um pool de contas de usuário locais do Windows de baixo privilégio. Quando um processo externo é necessário, o Launchpad usa uma conta de trabalho disponível e a usa para executar um processo. Mais especificamente, o Launchpad ativa uma conta de trabalho disponível, mapeia-a para a identidade do usuário que está chamando e executa o script na conta de trabalho.

+ **SQLRUserGroup** está vinculado a uma instância específica. Um pool separado de contas de trabalho é necessário para cada instância em que o Machine Learning foi habilitado. Contas não podem ser compartilhadas entre instâncias.

+ O tamanho do pool de contas de usuário é estático e o valor padrão é 20, que dá suporte a 20 sessões simultâneas. O número de sessões de tempo de execução externas que podem ser iniciadas simultaneamente é limitado pelo tamanho desse pool de contas de usuário. 

+ Os nomes de conta de trabalho no pool são do formato SQLINSTANCENAME*NN*. Por exemplo, em uma instância padrão, **SQLRUserGroup** contém contas chamadas MSSQLSERVER01, MSSQLSERVER02 e assim por diante em até MSSQLSERVER20.

As tarefas paralelizadas não consomem contas adicionais. Por exemplo, se um usuário executar uma tarefa de pontuação que usa processamento paralelo, a mesma conta de trabalho será reutilizada para todos os threads. Se você pretende fazer uso intensivo do aprendizado de máquina, pode aumentar o número de contas usadas para executar scripts externos. Para obter mais informações, consulte [Modificar o pool de contas de usuário para aprendizado de máquina](../../advanced-analytics/administration/modify-user-account-pool.md).

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>Isolamento do AppContainer no SQL Server 2019

No SQL Server 2019, a instalação não cria mais contas de trabalho para **SQLRUserGroup**. Em vez disso, o isolamento é obtido por meio de [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). Em tempo de execução, quando um script externo é detectado em um procedimento armazenado ou consulta, SQL Server chama o Launchpad com uma solicitação para um iniciador específico da extensão. O Launchpad invoca o ambiente de tempo de execução apropriado em um processo sob sua identidade e cria uma instância de um AppContainer para contê-lo. Essa alteração é benéfica porque o gerenciamento de conta local e de senha não é mais necessário. Além disso, em instalações em que as contas de usuário local são proibidas, a eliminação da dependência de conta de usuário local significa que agora você pode usar esse recurso.

Conforme implementado por SQL Server, AppContainers são um mecanismo interno. Embora você não veja evidências físicas de AppContainers no monitor de processos, pode encontrá-las em regras de firewall de saída criadas pela instalação para impedir que processos façam chamadas de rede. Para obter mais informações, consulte [configuração de firewall para SQL Server serviços de Machine Learning](../../advanced-analytics/security/firewall-configuration.md).

> [!Note]
> No SQL Server 2019, **SQLRUserGroup** tem apenas um membro que agora é a única conta de serviço de SQL Server Launchpad em vez de várias contas de trabalho.
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>Permissões concedidas a SQLRUserGroup

Por padrão, os membros de **SQLRUserGroup** têm permissões de leitura e execução em arquivos nos diretórios SQL Server **Binn**, **R_SERVICES**e **PYTHON_SERVICES** , com acesso a executáveis, bibliotecas e conjuntos de arquivos internos no R e distribuições do Python instaladas com o SQL Server. 

Para proteger recursos confidenciais no SQL Server, você pode, opcionalmente, definir uma lista de controle de acesso (ACL) que nega o acesso ao **SQLRUserGroup**. Por outro lado, você também pode conceder permissões a recursos de dados locais que existem no computador host, além do SQL Server em si. 

Por design, o **SQLRUserGroup** não tem um logon de banco de dados nem permissões para nenhum dado. Em determinadas circunstâncias, talvez você queira criar um logon para permitir conexões de back-loop, particularmente quando uma identidade confiável do Windows é o usuário de chamada. Esse recurso é chamado de [*autenticação implícita*](#implied-authentication). Para obter mais informações, consulte [Adicionar SQLRUserGroup como um usuário de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

## <a name="identity-mapping"></a>Mapeamento de identidade

Quando uma sessão é iniciada, Launchpad mapeia a identidade do usuário que está chamando para uma conta de trabalho. O mapeamento de um usuário externo do Windows ou logon SQL válido para uma conta de trabalho é válido somente pelo tempo de vida do procedimento armazenado SQL que executa o script externo. Consultas paralelas do mesmo logon são mapeadas para a mesma conta de trabalho do usuário.

Durante a execução, o Launchpad cria pastas temporárias para armazenar dados de sessão, excluindo-os quando a sessão termina. Os diretórios têm acesso restrito. Para R, o RLauncher executa essa tarefa. Para Python, o PythonLauncher executa essa tarefa. Cada conta de trabalho individual é restrita à sua própria pasta e não pode acessar arquivos em pastas acima do seu próprio nível. No entanto, a conta de trabalho pode ler, gravar ou excluir filhos na pasta de trabalho de sessão que foi criada. Se você for um administrador no computador, você poderá exibir os diretórios criados para cada processo. Cada diretório é identificado por seu GUID de sessão.

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>Autenticação implícita (solicitações de loop posterior)

A *autenticação implícita* descreve o comportamento de solicitação de conexão sob o qual os processos externos em execução como contas de trabalho de baixo privilégio são apresentados como uma identidade de usuário confiável para SQL Server em solicitações de retorno de loop para dados ou operações. Como um conceito, a autenticação implícita é exclusiva da autenticação do Windows, em SQL Server cadeias de conexão que especificam uma conexão confiável, em solicitações originadas de processos externos, como o script R ou Python. Às vezes, ele também é conhecido como um *loop de volta*.

As conexões confiáveis são inviávels do script R e Python, mas apenas com configuração adicional. Na arquitetura de extensibilidade, os processos R e Python são executados em contas de trabalho, herdando permissões do **SQLRUserGroup**pai. Quando uma cadeia de conexão `Trusted_Connection=True`especifica, a identidade da conta de trabalho é apresentada na solicitação de conexão, que é desconhecida por padrão para SQL Server.

Para que as conexões confiáveis sejam bem-sucedidas, você deve criar um logon de banco de dados para o **SQLRUserGroup**. Depois de fazer isso, qualquer conexão confiável de qualquer membro de **SQLRUserGroup** tem direitos de logon para SQL Server. Para obter instruções detalhadas, consulte [Adicionar SQLRUserGroup a um logon de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

As conexões confiáveis não são a formulação mais amplamente usada de uma solicitação de conexão. Quando o script R ou Python especifica uma conexão, pode ser mais comum usar um logon do SQL ou um nome de usuário e senha totalmente especificados se a conexão for para uma fonte de dados ODBC.

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>Como funciona a autenticação implícita para sessões do R e do Python

O diagrama a seguir mostra a interação de SQL Server componentes com o tempo de execução de R e como ele faz a autenticação implícita para R.

![Autenticação implícita para R](../security/media/implied-auth-rsql.png)

O próximo diagrama mostra a interação de SQL Server componentes com o tempo de execução do Python e como ele faz a autenticação implícita para Python.

![Autenticação implícita para Python](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>Não há suporte para Transparent Data Encryption em repouso

Não há suporte para [Transparent Data Encryption (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) para dados enviados ou recebidos do tempo de execução de script externo. O motivo é que o processo externo (R ou Python) é executado fora do processo de SQL Server. Portanto, os dados usados pelo tempo de execução externo não são protegidos pelos recursos de criptografia do mecanismo de banco de dados. Esse comportamento não é diferente de qualquer outro cliente em execução no computador SQL Server que lê dados do banco e faz uma cópia.

Como consequência, o TDE **não é** aplicado a nenhum dado que você use em scripts R ou Python, ou a quaisquer dados salvos em disco ou a quaisquer resultados intermediários persistentes. No entanto, outros tipos de criptografia, como criptografia BitLocker do Windows ou criptografia de terceiros aplicados no nível de arquivo ou pasta, ainda se aplicam.

No caso de [Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md), os tempos de execução externos não têm acesso às chaves de criptografia. Portanto, os dados não podem ser enviados para os scripts.

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você aprendeu os componentes e o modelo de interação da arquitetura de segurança criada na [estrutura de extensibilidade](../../advanced-analytics/concepts/extensibility-framework.md). Os principais pontos abordados neste artigo incluem a finalidade das contas Launchpad, SQLRUserGroup e Worker, o isolamento do processo de R e Python e como as identidades de usuário são mapeadas para as contas de trabalho. 

Como uma próxima etapa, examine as instruções para [conceder permissões](../../advanced-analytics/security/user-permission.md). Para servidores que usam a autenticação do Windows, você também deve examinar [Adicionar SQLRUserGroup a um logon de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md) para saber quando é necessária uma configuração adicional.