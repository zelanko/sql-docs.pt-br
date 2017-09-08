---
title: "Visão geral de segurança (SQL Server R Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8388d7c9d22a49a49a1a45a6fa6b479107f9ccae
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview-sql-server-r-services"></a>Visão geral de segurança (SQL Server R Services)

Este tópico descreve a arquitetura geral de segurança que é usada para conectar o mecanismo de banco de dados [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e os componentes relacionados ao tempo de execução do R. Exemplos do processo de segurança são fornecidos para dois cenários comuns de uso do R em um ambiente corporativo:

+ Executando funções RevoScaleR em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] de um cliente de ciência de dados
+ Executar o R diretamente do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando procedimentos armazenados

## <a name="security-overview"></a>Visão geral de segurança

Um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] logon ou conta de usuário do Windows é necessário para executar scripts do R que usam dados do SQL Server ou que executam o com o SQL Server como o contexto de computação. Esse requisito se aplica a ambos [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] e serviços de aprendizado de máquina do SQL Server de 2017. 

A conta de logon ou usuário identifica o *entidade de segurança*, que talvez seja necessário vários níveis de acesso, dependendo dos requisitos de script R:
+ Permissão para acessar o banco de dados onde R é habilitado
+ Permissões para ler dados de objetos protegidos, como tabelas
+ A capacidade de gravar novos dados em uma tabela, como um modelo ou resultados de pontuação
+ A capacidade de criar novos objetos, como tabelas, procedimentos armazenados do que usam o script R ou personalizado funções de trabalho use R
+ O direito de instalar novos pacotes no computador do SQL Server, ou use R pacotes fornecidos a um grupo de usuários. 

Portanto, cada pessoa que executa o código R usando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] como a execução de contexto deve ser mapeado para um logon no banco de dados. Na segurança do SQL Server, é geralmente mais fácil criar funções para gerenciar conjuntos de permissões e atribuir usuários a essas funções, em vez de definir individualmente as permissões de usuário. 

Por exemplo, suponha que você criou um código de R que é executado em seu laptop, e você deseja executar esse código em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Você pode fazer isso apenas se essas condições forem atendidas:

+ O banco de dados permite conexões remotas.
+ Um logon SQL com o nome e a senha que você usou no código R foi adicionado ao [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] no nível de instância. Ou, se você estiver usando a autenticação integrada do Windows, o usuário do Windows especificado na cadeia de conexão deverá ser adicionado como um usuário na instância.
+ O logon do SQL ou o usuário do Windows deve ter a permissão para executar scripts externos. Em geral, essa permissão só pode ser adicionada por um administrador de banco de dados.
+ O logon SQL ou o usuário do Windows deverá ser adicionado como um usuário, com as permissões apropriadas, em cada banco de dados em que o trabalho do R executar qualquer uma destas operações:
    + Recuperação dados
    + Gravação ou atualização de dados 
    + Criação de novos objetos, tais como tabelas ou procedimentos armazenados

Depois que o logon ou conta de usuário do Windows foi provisionada e recebeu as permissões necessárias, você pode executar código R em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando um objeto de fonte de dados R ou chamando um procedimento armazenado. Sempre que R é iniciado do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], a segurança do mecanismo de banco de dados obtém o contexto de segurança do usuário que iniciou o trabalho de R ou executar o procedimento armazenado e gerencia os mapeamentos do usuário ou logon em objetos protegíveis. 

Portanto, todos os trabalhos de R que são iniciados de um cliente remoto devem especificar as informações de logon ou usuário como parte da cadeia de conexão.

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interação entre Segurança do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e Segurança do LaunchPad

Quando um script R é executado no contexto do computador do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], o serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] obtém uma conta de trabalho disponível (uma conta de usuário local) de um pool de contas de trabalho estabelecido para o processo externo e usa essa conta de trabalho para executar as tarefas relacionadas. 

Por exemplo, se você iniciar um trabalho de R com suas credenciais de domínio do Windows, sua conta poderá ser mapeada para a conta de trabalho *SQLRUser01* do Launchpad.

Após o mapeamento para uma conta de trabalho, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] cria um token de usuário que é usado para iniciar processos. 

Quando todas as operações de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] forem concluídas, a conta de trabalho do usuário será marcada como livre e retornada ao pool.

Para obter mais informações sobre o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], consulte [Novos componentes do SQL Server para suporte à integração de R](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r.md).

> [!NOTE]
Para que o Launchpad gerencie as contas de trabalho e execute trabalhos em R, o grupo que contém as contas de trabalho, SQLRUserGroup, deverá ter permissões para "Permitir logon local"; caso contrário, o R Services poderá não funcionar. Esse direito é fornecido por padrão a todos os novos usuários locais, mas em algumas organizações, é possível que políticas de grupo mais rígidas sejam impostas, impedindo que as contas de trabalho se conectem ao SQL Server para executar trabalhos em R.  

## <a name="security-of-worker-accounts"></a>Segurança de contas de trabalho

O mapeamento de um usuário externo do Windows ou logon SQL válido para uma conta de trabalho é válido somente para o tempo de vida do tempo de vida da consulta SQL que executa o script R. 

Consultas paralelas do mesmo logon são mapeadas para a mesma conta de trabalho do usuário.

As pastas usadas para os processos são gerenciadas pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] usando o RLauncher e o acesso aos diretórios é restrito. A conta de trabalho não pode acessar todos os arquivos em pastas acima da pasta da própria conta, mas ela pode ler, gravar ou excluir filhos sob a pasta de trabalho de sessão que foi criada para a consulta SQL com o script R.

Para obter mais informações sobre como alterar o número de contas de trabalho, nomes de conta ou senhas de conta, consulte [Modificar o pool de contas de usuário para o SQL Server R Services](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).


## <a name="security-isolation-for-multiple-external-scripts"></a>Isolamento de segurança para vários scripts externos

O mecanismo de isolamento se baseia em contas de usuário físico. Conforme os processos satélite são iniciados para o tempo de execução de uma linguagem específica, cada tarefa satélite usa a conta de trabalho especificada pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Se uma tarefa exigir vários satélites, tal como no caso de consultas paralelas, uma única conta de trabalho será usada para todas as tarefas relacionadas.

Nenhuma conta de trabalho pode ver ou manipular arquivos usados por outras contas de trabalho.
 
Se você for um administrador no computador, você poderá exibir os diretórios criados para cada processo. Cada diretório é identificado por seu GUID de sessão.

## <a name="see-also"></a>Consulte também
[Visão geral de arquitetura](../../advanced-analytics/r-services/architecture-overview-sql-server-r.md)

