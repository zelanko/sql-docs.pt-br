---
title: Visão geral de segurança para extensões de R e Python – Machine Learning do SQL Server
description: Visão geral de segurança para a estrutura de extensibilidade em serviços do SQL Server Machine Learning. Segurança para contas de usuário e logon, o serviço Launchpad do SQL Server, contas de trabalho que executam vários scripts e permissões de arquivo.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1f19e3322b8aee78fdb5a76a29a719148cc6a0c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66454542"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>Visão geral de segurança para a estrutura de extensibilidade em serviços do SQL Server Machine Learning

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve a arquitetura geral de segurança que é usada para integrar o mecanismo de banco de dados do SQL Server e componentes relacionados com a estrutura de extensibilidade. Ele examina a protegíveis, serviços, identidade de processo e permissões. Para obter mais informações sobre os principais conceitos e componentes de extensibilidade no SQL Server, consulte [arquitetura de extensibilidade no SQL Server Machine Learning Services](extensibility-framework.md)].

## <a name="securables-for-external-script"></a>Protegíveis de script externo

Um script externo escrito em R ou Python é enviado como um parâmetro de entrada para um [procedimento armazenado do sistema](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) criada para essa finalidade, ou é encapsulado em um procedimento armazenado que você definir. Como alternativa, você pode ter modelos pré-treinado e armazenados em um formato binário em uma tabela de banco de dados, que pode ser chamado em um T-SQL [PREDICT](../../t-sql/queries/predict-transact-sql.md) função.

Como o script é fornecido por meio de objetos existentes do esquema de banco de dados, tabelas e procedimentos armazenados, há nenhum novo [protegíveis](../../relational-databases/security/securables.md) para serviços do SQL Server Machine Learning.

Independentemente de como você está usando um script ou, o que eles consistem em, objetos de banco de dados serão criados e salvo provavelmente, mas nenhum novo tipo de objeto é apresentado para armazenar o script. Como resultado, a capacidade de consumir, criar e salvar o banco de dados de objetos depende em grande parte permissões de banco de dados já definidas para seus usuários.

<a name="permissions"></a>

## <a name="permissions"></a>Permissões

Estender o modelo de segurança de dados do SQL Server de logons de banco de dados e funções para o script de R e Python. Um logon do SQL Server ou a conta de usuário do Windows é necessário para executar scripts externos que usam dados do SQL Server ou que são executados com o SQL Server como o contexto de computação. Os usuários de banco de dados que têm permissões para executar uma consulta ad hoc podem acessar os mesmos dados de script R ou Python.

A conta de usuário ou logon identifica o *entidade de segurança*, que talvez seja necessário vários níveis de acesso, dependendo dos requisitos de script externo:

+ Permissão para acessar o banco de dados em que os scripts externos estão habilitados.
+ Permissões para ler dados de objetos protegidos, como tabelas.
+ A capacidade de gravar novos dados em uma tabela, como um modelo ou resultados de pontuação.
+ A capacidade de criar novos objetos, como tabelas, procedimentos armazenados que usam o script externo ou funções personalizadas do que usar o R ou o trabalho do Python.
+ O direito de instalar novos pacotes no computador do SQL Server, ou usar os pacotes fornecidos a um grupo de usuários.

Cada pessoa que executa um script externo usando o SQL Server como o contexto de execução deve ser mapeada para um usuário no banco de dados. Em vez de individualmente conjunto de banco de dados permissões de usuário, você pode criar funções para gerenciar conjuntos de permissões e atribuir usuários a essas funções, em vez de individualmente, definir permissões de usuário.

Para obter mais informações, consulte [aos usuários permissão para serviços do SQL Server Machine Learning](../../advanced-analytics/security/user-permission.md).

## <a name="permissions-when-using-an-external-client-tool"></a>Permissões ao usar uma ferramenta de cliente externo

Usuários que estão usando o R ou Python em uma ferramenta de cliente externo devem ter seu logon ou conta mapeada para um usuário no banco de dados se eles precisarem executar um script externo no banco de dados, ou acessar objetos de banco de dados e dados. As mesmas permissões são necessárias se o script externo for enviado de um cliente de ciência de dados remoto ou executadas usando um procedimento armazenado T-SQL.

Por exemplo, suponha que você criou um script externo que é executado no computador local, e você deseja executar esse script no SQL Server. Você deve certificar-se de que as seguintes condições sejam atendidas:

+ O banco de dados permite conexões remotas.
+ O logon SQL ou a conta do Windows que você usou para acesso ao banco de dados foi adicionada para o SQL Server no nível de instância.
+ O logon do SQL ou o usuário do Windows deve ter a permissão para executar scripts externos. Em geral, essa permissão só pode ser adicionada por um administrador de banco de dados.
+ O logon do SQL ou o usuário da janela deve ser adicionado como um usuário, com permissões apropriadas, em cada banco de dados em que o script externo executa qualquer uma dessas operações:
  + Recuperando dados.
  + Gravação ou a atualização de dados.
  + Criando novos objetos, como tabelas ou procedimentos armazenados.

Depois que o logon ou conta de usuário do Windows foi provisionada e recebeu as permissões necessárias, você pode executar um script externo no SQL Server usando um objeto de fonte de dados em R ou o **revoscalepy** biblioteca em Python ou chamando um armazenado procedimento que contém o script externo.

Sempre que um script externo é iniciado a partir do SQL Server, a segurança do mecanismo de banco de dados obtém o contexto de segurança do usuário que iniciou o trabalho e gerencia os mapeamentos do usuário ou logon para objetos protegíveis.

Portanto, todos os scripts externos que são iniciados de um cliente remoto devem especificar as informações de logon ou usuário como parte da cadeia de conexão.

<a name="launchpad"></a>

## <a name="services-used-in-external-processing-launchpad"></a>Serviços usados no processamento externo (Launchpad)

A estrutura de extensibilidade adiciona um novo serviço de NT para o [lista de serviços](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md#Service_Details) em uma instalação do SQL Server: [**SQL Server Launchpad (MSSSQLSERVER)** ](extensibility-framework.md#launchpad).

O mecanismo de banco de dados usa o serviço Launchpad do SQL Server para criar uma instância de uma sessão de R ou Python como um processo separado. O processo é executado sob uma conta de baixo privilégio; diferente do SQL Server, o Launchpad em si e a identidade do usuário na qual a consulta de host ou o procedimento armazenada foi executada. Executar o script em um processo separado, na conta de baixo privilégio, é a base do modelo de segurança e isolamento para R e Python no SQL Server.

Além de iniciar processos externos, o Launchpad também é responsável para controlar a identidade do usuário da chamada e essa identidade para a conta de trabalho de baixo privilégio usada para iniciar o processo de mapeamento. Em alguns cenários, no qual script ou código chama de volta para o SQL Server para dados e operações, a barra inicial é geralmente capaz de gerenciar a transferência de identidade perfeitamente. Script que contém as instruções SELECT ou chamar funções e outros objetos de programação normalmente terá êxito se o usuário chamador tem permissões suficientes.

> [!NOTE]
> Por padrão, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] está configurado para ser executado sob **NT Service\MSSQLLaunchpad**, que é provisionado com todas as permissões necessárias para executar scripts externos. Para obter mais informações sobre as opções configuráveis, consulte [configuração do serviço Launchpad do SQL Server](../security/sql-server-launchpad-service-account.md).

<a name="sqlrusergroup"></a>

## <a name="identities-used-in-processing-sqlrusergroup"></a>Identidades usadas no processamento (SQLRUserGroup)

**SQLRUserGroup** (grupo de usuários restritos do SQL) é criado pela instalação do SQL Server e contém um pool de contas de usuário do Windows locais com poucos privilégios. Quando for necessário um processo externo, Launchpad leva a uma conta de trabalho disponíveis e usa-o para executar um processo. Mais especificamente, o Launchpad ativa uma conta de trabalho disponível, mapeia-os para a identidade do usuário da chamada e executa o script sob a conta de trabalho.

+ **SQLRUserGroup** está vinculado a uma instância específica. Um pool separado de contas de trabalho é necessário para cada instância no qual o machine learning foi habilitado. Contas não podem ser compartilhadas entre instâncias.

+ O tamanho do pool de conta de usuário é estático e o valor padrão é 20, que oferece suporte a 20 sessões simultâneas. O número de sessões de tempo de execução externos que podem ser iniciadas simultaneamente é limitado pelo tamanho desse pool de conta de usuário. 

+ Nomes de conta de trabalho no pool estão no formato SQLInstanceName*nn*. Por exemplo, em uma instância padrão, **SQLRUserGroup** contém contas chamadas MSSQLSERVER01, MSSQLSERVER02 e assim por diante na até MSSQLSERVER20.

Tarefas em paralelo não consomem contas adicionais. Por exemplo, se um usuário executa uma tarefa de pontuação que usa processamento paralelo, a mesma conta de trabalho é reutilizada para todos os threads. Se você pretende fazem uso intenso de aprendizado de máquina, você pode aumentar o número de contas usadas para executar scripts externos. Para obter mais informações, consulte [modificar o pool de conta de usuário para o machine learning](../../advanced-analytics/administration/modify-user-account-pool.md).

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>Isolamento do AppContainer no SQL Server 2019

No SQL Server de 2019, a instalação não cria mais contas de trabalho para **SQLRUserGroup**. Em vez disso, o isolamento é obtido por meio [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). Em tempo de execução, quando um script externo é detectado em uma consulta ou procedimento armazenado, SQL Server chama o Launchpad com uma solicitação para um iniciador específicas da extensão. Launchpad invoca o ambiente de tempo de execução apropriado em um processo sob sua identidade e cria uma instância de um AppContainer para contê-lo. Essa alteração é benéfica porque o gerenciamento de conta e senha local não é mais necessário. Além disso, em instalações em que as contas de usuário local são proibidas, eliminação da dependência de conta de usuário local significa que agora você pode usar esse recurso.

Conforme implementado pelo SQL Server, AppContainers são um mecanismo interno. Embora você não ver evidências físicas de AppContainers no Monitor de processo, você pode encontrá-los nas regras de firewall de saída criadas pela instalação para impedir que processos façam chamadas de rede. Para obter mais informações, consulte [configuração do Firewall para serviços do SQL Server Machine Learning](../../advanced-analytics/security/firewall-configuration.md).

> [!Note]
> No SQL Server de 2019, **SQLRUserGroup** tem apenas um membro que agora é a única conta de serviço do Launchpad do SQL Server em vez de várias contas de trabalho.
::: moniker-end

### <a name="permissions-granted-to-sqlrusergroup"></a>Permissões concedidas ao SQLRUserGroup

Por padrão, os membros **SQLRUserGroup** leu e permissões de execução nos arquivos do SQL Server **Binn**, **R_SERVICES**, e **PYTHON_SERVICES** diretórios com acesso a arquivos executáveis, bibliotecas e conjuntos de dados internos nas distribuições de R e Python instalados com o SQL Server. 

Para proteger recursos confidenciais no SQL Server, opcionalmente, você pode definir uma lista de controle de acesso (ACL) que nega o acesso ao **SQLRUserGroup**. Por outro lado, você também pode conceder permissões para recursos de dados local que existem no computador host, além do próprio SQL Server. 

Por design, **SQLRUserGroup** não tem permissões para todos os dados ou um logon de banco de dados. Em determinadas circunstâncias, você talvez queira criar um logon para permitir conexões de voltar de loop, especialmente quando uma identidade confiável do Windows é o usuário que está chamando. Esse recurso é chamado [ *autenticação implícita*](#implied-authentication). Para obter mais informações, consulte [adicionar SQLRUserGroup como um usuário de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

## <a name="identity-mapping"></a>Mapeamento de identidade

Quando uma sessão é iniciada, o Launchpad mapeia a identidade do usuário da chamada para uma conta de trabalho. O mapeamento de um usuário externo do Windows ou logon SQL válido para uma conta de trabalho é válido somente para o procedimento armazenado de tempo de vida do SQL que executa o script externo. Consultas paralelas do mesmo logon são mapeadas para a mesma conta de trabalho do usuário.

Durante a execução, o Launchpad cria pastas temporárias para armazenar dados de sessão, excluí-los quando a sessão termina. Os diretórios têm o acesso restrito. Para R, RLauncher realiza essa tarefa. Para o Python, PythonLauncher realiza essa tarefa. Cada conta de trabalho individuais é restrito a sua própria pasta e não pode acessar arquivos em pastas acima de seu próprio nível. No entanto, a conta de trabalho pode ler, gravar ou excluir filhos sob a pasta de trabalho de sessão que foi criado. Se você for um administrador no computador, você poderá exibir os diretórios criados para cada processo. Cada diretório é identificado por seu GUID de sessão.

<a name="implied-authentication"></a>

## <a name="implied-authentication-loop-back-requests"></a>Autenticação implícita (solicitações de back-loop)

*Autenticação implícita* descreve o comportamento de solicitação de conexão sob a qual processos externos em execução como contas de trabalho de baixo privilégio são apresentadas como uma identidade de usuário confiável para o SQL Server no back-solicitações de dados ou operações de loop. Como um conceito, a autenticação implícita é exclusiva para autenticação do Windows, nas cadeias de caracteres de conexão do SQL Server especificando uma conexão confiável, em solicitações provenientes de processos externos, como o script de R ou Python. Ela é, às vezes, também conhecida como uma *loopback*.

Conexões confiáveis são viável do script R e Python, mas apenas com uma configuração adicional. Na arquitetura de extensibilidade, processos de R e Python são executados em contas de trabalho, herdar permissões do pai **SQLRUserGroup**. Quando uma cadeia de caracteres de conexão especifica `Trusted_Connection=True`, a identidade da conta de trabalho é apresentada na solicitação de conexão, que é desconhecida por padrão para o SQL Server.

Para fazer conexões confiáveis com êxito, você deve criar um logon de banco de dados para o **SQLRUserGroup**. Depois de fazer isso, qualquer confiável para conexão a partir de qualquer membro da **SQLRUserGroup** tem direitos de logon para o SQL Server. Para obter instruções passo a passo, consulte [SQLRUserGroup adicionar a um logon de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md).

Conexões confiáveis não são a mais amplamente usada formulação de uma solicitação de conexão. Quando o script de R ou Python Especifica uma conexão, é mais comum usar um logon do SQL, ou um nome de usuário totalmente especificado e uma senha se a conexão é a uma fonte de dados ODBC.

### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>Implícita como funciona a autenticação para sessões de R e Python

O diagrama a seguir mostra a interação de componentes do SQL Server com o tempo de execução de R e como ele faz a autenticação implícita para R.

![Autenticação implícita para R](../security/media/implied-auth-rsql.png)

O diagrama a seguir mostra a interação de componentes do SQL Server com o tempo de execução do Python e como ele faz a autenticação implícita para Python.

![Autenticação implícita para Python](../security/media/implied-auth-python2.png)

## <a name="no-support-for-transparent-data-encryption-at-rest"></a>Não há suporte para criptografia transparente de dados em repouso

[Criptografia de dados transparente (TDE)](../../relational-databases/security/encryption/transparent-data-encryption.md) não há suporte para dados enviados ou recebidos do tempo de execução do script externo. O motivo é que o processo externo (R ou Python) é executado fora do processo do SQL Server. Portanto, os dados usados pelo tempo de execução externo não serão protegidos pelos recursos de criptografia do mecanismo de banco de dados. Esse comportamento é não é diferente de qualquer outro cliente em execução no computador do SQL Server que lê dados do banco de dados e faz uma cópia.

Como consequência, a TDE **não é** aplicadas a todos os dados que você pode usar nos scripts de R ou Python, ou a todos os dados salvos em disco, ou em resultados intermediários persistentes. No entanto, outros tipos de criptografia, como criptografia de disco BitLocker do Windows ou a criptografia de terceiros são aplicadas no nível de arquivo ou pasta, ainda se aplicam.

No caso de [Always Encrypted](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md), tempos de execução externos não têm acesso às chaves de criptografia. Portanto, os dados não serão enviados para os scripts.

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você aprendeu os componentes e o modelo de interação da arquitetura de segurança incorporados a [estrutura de extensibilidade](../../advanced-analytics/concepts/extensibility-framework.md). Os principais pontos abordados neste artigo incluem a finalidade das contas de trabalho, SQLRUserGroup e barra inicial, o isolamento do processo do R e Python e como as identidades de usuário são mapeadas para contas de trabalho. 

Como uma próxima etapa, examine as instruções para [concedendo permissões](../../advanced-analytics/security/user-permission.md). Para servidores que usam a autenticação do Windows, você também deve revisar [SQLRUserGroup adicionar a um logon de banco de dados](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md) para saber quando a configuração adicional é necessária.