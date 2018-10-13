---
title: Segurança do SQL Server para aprendizado de máquina | Microsoft Docs
description: Visão geral de segurança para a estrutura de extensibilidade em serviços do SQL Server Machine Learning. Segurança para contas de usuário e logon, o serviço Launchpad do SQL Server, contas de trabalho que executam vários scripts e permissões de arquivo.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: bee8e2162c56ac1b26273873943d848c2167dbda
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100397"
---
# <a name="security-overview-for-the-extensibility-framework-in-sql-server-machine-learning-services"></a>Visão geral de segurança para a estrutura de extensibilidade em serviços do SQL Server Machine Learning

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve a arquitetura geral de segurança que é usada para conectar o mecanismo de banco de dados do SQL Server e componentes relacionados para a estrutura de extensibilidade. Ele descreve as interações e partes do componente. 

<a name="launchpad"></a>

## <a name="sql-server-launchpad-service"></a>Serviço do Launchpad do SQL Server

Para criar uma instância de processos externos, o mecanismo de banco de dados fornece o serviço Launchpad do SQL Server para criar uma sessão de R ou Python. Um separado [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] serviço é criado para a instância do mecanismo de banco de dados ao qual você adicionou a integração de (R ou Python) de aprendizado de máquina do SQL Server, um serviço por instância.

Por padrão, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] está configurado para ser executado sob **NT Service\MSSQLLaunchpad**, que é provisionado com todas as permissões necessárias para executar scripts externos. Removendo permissões desta conta pode resultar em [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] Falha ao iniciar ou acessar a instância do SQL Server em que os scripts externos devem ser executados. Serviço Launchpad geralmente é usado como-está, mas para obter mais informações sobre as opções configuráveis, consulte [configuração do serviço Launchpad do SQL Server](../security/sql-server-launchpad-service-account.md).

<a name="sqlrusergroup"></a>

## <a name="sqlrusergroup-and-worker-accounts"></a>Contas de trabalho e SQLRUserGroup

Scripts externos executados em processos externos, sob a identidade das contas de local de trabalho com menos privilégios, sujeito à lista de controle de acesso (ACL) do pai **SQLRUserGroup** (grupo de usuários restritos do SQL). 

**SQLRUserGroup** é criado pela instalação do SQL Server e contém o pool de contas de usuário locais do Windows. Quando for necessário um processo externo, Launchpad leva a uma conta de trabalho disponíveis e usa-o para executar um processo. Mais especificamente, o Launchpad ativa uma conta de trabalho disponível, mapeia-os para a identidade do usuário da chamada e executa o script sob a conta de trabalho. 

+ **SQLRUserGroup** está vinculado a uma instância específica. Um pool separado de contas de trabalho é necessário para cada instância no qual o machine learning foi habilitado. Contas não podem ser compartilhadas entre instâncias.

+ O tamanho do pool de conta de usuário é estático e o valor padrão é 20, que oferece suporte a 20 sessões simultâneas. O número de sessões de tempo de execução externos que podem ser iniciadas simultaneamente é limitado pelo tamanho desse pool de conta de usuário. 

+ Nomes de conta de trabalho no pool estão no formato SQLInstanceName*nn*. Por exemplo, em uma instância padrão, **SQLRUserGroup** contém contas chamadas MSSQLSERVER01, MSSQLSERVER02 e assim por diante na até MSSQLSERVER20.

Tarefas em paralelo não consomem contas adicionais. Por exemplo, se um usuário executa uma tarefa de pontuação que usa processamento paralelo, a mesma conta de trabalho é reutilizada para todos os threads. Se você pretende fazem uso intenso de aprendizado de máquina, você pode aumentar o número de contas usadas para executar scripts externos. Para obter mais informações, consulte [modificar o pool de conta de usuário para o machine learning](../../advanced-analytics/administration/modify-user-account-pool.md).

### <a name="permissions-granted-to-sqlrusergroup"></a>Permissões concedidas ao SQLRUserGroup

Por padrão, os membros **SQLRUserGroup** leu e permissões de execução nos arquivos do SQL Server **Binn**, **R_SERVICES**, e **PYTHON_SERVICES** diretórios com acesso a arquivos executáveis, bibliotecas e conjuntos de dados internos nas distribuições de R e Python instalados com o SQL Server. 

Para proteger recursos confidenciais no SQL Server, opcionalmente, você pode definir uma lista de controle de acesso (ACL) que nega o acesso ao **SQLRUserGroup**. Por outro lado, você também pode conceder permissões para recursos de dados local que existem no computador host, além do próprio SQL Server. 

Por design, **SQLRUserGroup** não tem permissões para todos os dados ou um logon de banco de dados. Em determinadas circunstâncias, você talvez queira criar um logon para permitir conexões de voltar de loop, especialmente quando uma identidade confiável do Windows é o usuário que está chamando. Esse recurso é chamado [ *autenticação implícita*](#implied-authentication). Para obter mais informações, consulte [adicionar SQLRUserGroup como um usuário de banco de dados](../../advanced-analytics/security/add-sqlrusergroup-to-database.md).

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
### <a name="appcontainer-isolation-in-sql-server-2019"></a>Isolamento do AppContainer no SQL Server 2019

No SQL Server de 2019, a instalação não cria mais contas de trabalho para **SQLRUserGroup**. Em vez disso, o isolamento é obtido por meio [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). Em tempo de execução quando o script inserido ou o código é detectado em uma consulta ou procedimento armazenado, SQL Server chama o Launchpad com uma solicitação para um iniciador específicas da extensão. Launchpad invoca o ambiente de tempo de execução apropriado em um processo sob sua identidade e cria uma instância de um AppContainer para contê-lo. Essa alteração é benéfica porque o gerenciamento de conta e senha local não é mais necessário. Além disso, em instalações em que as contas de usuário local são proibidas, eliminação da dependência de conta de usuário local significa que agora você pode usar esse recurso.

Conforme implementado pelo SQL Server, AppContainers são um mecanismo interno. Embora você não ver evidências físicas de AppContainers no Monitor de processo, você pode encontrá-los nas regras de firewall de saída criadas pela instalação para impedir que processos façam chamadas de rede.

> [!Note]
> No SQL Server de 2019, **SQLRUserGroup** tem apenas um membro que agora é a única conta de serviço do Launchpad do SQL Server em vez de várias contas de trabalho.
::: moniker-end

## <a name="user-security"></a>Segurança do usuário

Estender o modelo de segurança de dados do SQL Server de logons de banco de dados e funções para o script de R e Python. Logons de banco de dados podem ser baseados em identidades do Windows ou um usuário de banco de dados do SQL Server. 

Como um usuário de banco de dados, se você tiver permissões para executar uma consulta específica, qualquer script de R ou Python que são executados no SQL Server também tem permissão para recuperar os mesmos dados. A capacidade de consumir, criar e salvar o banco de dados de objetos depende das permissões de banco de dados. Para obter mais informações, consulte [aos usuários permissão para serviços do SQL Server Machine Learning](../../advanced-analytics/security/user-permission.md).

### <a name="mapping-user-identities-to-worker-accounts"></a>Mapeando as identidades de usuário para contas de trabalho

Quando uma sessão é iniciada, o Launchpad mapeia a identidade do usuário da chamada para uma conta de trabalho. O mapeamento de um usuário externo do Windows ou logon SQL válido para uma conta de trabalho é válido somente para o procedimento armazenado de tempo de vida do SQL que executa o script externo. Consultas paralelas do mesmo logon são mapeadas para a mesma conta de trabalho do usuário.

Durante a execução, o Launchpad cria pastas temporárias para armazenar dados de sessão, excluí-los quando a sessão termina. Os diretórios têm o acesso restrito. Para R, RLauncher realiza essa tarefa. Para o Python, PythonLauncher realiza essa tarefa. Cada conta de trabalho individuais é restrito a sua própria pasta e não pode acessar arquivos em pastas acima de seu próprio nível. No entanto, a conta de trabalho pode ler, gravar ou excluir filhos sob a pasta de trabalho de sessão que foi criado. Se você for um administrador no computador, você poderá exibir os diretórios criados para cada processo. Cada diretório é identificado por seu GUID de sessão.

<a name="implied-authentication"></a>

### <a name="implied-authentication"></a>Autenticação implícita

*Autenticação implícita* descreve o comportamento de solicitação de conexão sob a qual processos externos em execução como contas de trabalho de baixo privilégio são apresentadas como uma identidade de usuário confiável para o SQL Server no back-solicitações de dados ou operações de loop. Como um conceito, a autenticação implícita é exclusiva para autenticação do Windows, nas cadeias de caracteres de conexão do SQL Server especificando uma conexão confiável, em solicitações provenientes de processos externos, como o script de R ou Python. Ela é, às vezes, também conhecida como uma *loopback*.

Conexões confiáveis são viável do script R e Python, mas apenas com uma configuração adicional. Na arquitetura de extensibilidade, processos de R e Python são executados em contas de trabalho, herdar permissões do pai **SQLRUserGroup**. Quando uma cadeia de caracteres de conexão Especifica "Trusted_Connection = True", a identidade da conta de trabalho é apresentada na solicitação de conexão, que é desconhecida por padrão para o SQL Server. 

Para fazer conexões confiáveis com êxito, você deve criar um logon de banco de dados para o **SQLRUserGroup**. Depois de fazer isso, qualquer confiável para conexão a partir de qualquer membro da **SQLRUserGroup** tem direitos de logon para o SQL Server. Para obter instruções passo a passo, consulte [SQLRUserGroup adicionar a um logon de banco de dados](../../advanced-analytics/security/add-sqlrusergroup-to-database.md).

Conexões confiáveis não são a mais amplamente usada formulação de uma solicitação de conexão. Quando o script de R ou Python Especifica uma conexão, é mais comum usar um logon do SQL, ou um nome de usuário totalmente especificado e uma senha se a conexão é a uma fonte de dados ODBC.

#### <a name="how-implied-authentication-works-for-r-and-python-sessions"></a>Implícita como funciona a autenticação para sessões de R e Python

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

Como uma próxima etapa, examine as instruções para [concedendo permissões](../../advanced-analytics/security/user-permission.md). Para servidores que usam a autenticação do Windows, você também deve revisar [SQLRUserGroup adicionar a um logon de banco de dados](../../advanced-analytics/security/add-sqlrusergroup-to-database.md) para saber quando a configuração adicional é necessária.