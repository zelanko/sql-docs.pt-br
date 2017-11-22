---
title: "Segurança de aprendizado de máquina do SQL Server e R | Microsoft Docs"
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: "9"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f694cca3286b5f1a9f738a08919f4fe8214fa770
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="security-for-sql-server-machine-learning-and-r"></a>Segurança de aprendizado de máquina do SQL Server e R

Este artigo descreve a arquitetura geral de segurança que é usada para conectar o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] componentes relacionados ao tempo de execução de R e mecanismo de banco de dados. Exemplos do processo de segurança são fornecidos para esses cenários comuns para usar o R em um ambiente corporativo:

+ Executando funções RevoScaleR em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] de um cliente de ciência de dados
+ Executar o R diretamente do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando procedimentos armazenados

## <a name="security-overview"></a>Visão geral de segurança

Um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] logon ou conta de usuário do Windows é necessário para executar scripts do R que usam dados do SQL Server ou que executam o com o SQL Server como o contexto de computação. Esse requisito se aplica a ambos [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] e SQL Server 2017 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)].

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

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interação de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] segurança e barra inicial

Quando um script R é executado no contexto do computador do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], o serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] obtém uma conta de trabalho disponível (uma conta de usuário local) de um pool de contas de trabalho estabelecido para o processo externo e usa essa conta de trabalho para executar as tarefas relacionadas. 

Por exemplo, se você iniciar um trabalho de R com suas credenciais de domínio do Windows, sua conta poderá ser mapeada para a conta de trabalho *SQLRUser01* do Launchpad.

Após o mapeamento para uma conta de trabalho, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] cria um token de usuário que é usado para iniciar processos. 

Quando todas as operações de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] forem concluídas, a conta de trabalho do usuário será marcada como livre e retornada ao pool.

Para obter mais informações sobre [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], consulte [componentes do SQL Server para dar suporte à integração de R](../../advanced-analytics/r/new-components-in-sql-server-to-support-r.md).

### <a name="implied-authentication"></a>Autenticação implícita

**Autenticação implícita** é o termo usado para o processo sob a qual o SQL Server obtém o usuário credenciais e, em seguida, executa todas as tarefas de script externo em nome dos usuários, supondo que o usuário tem as permissões corretas no banco de dados. Autenticação implícita é particularmente importante se o script R precisa fazer uma chamada ODBC fora do banco de dados do SQL Server. Por exemplo, o código pode recuperar uma lista menor de fatores de uma planilha ou outra fonte.

Para essas chamadas de loopback seja bem-sucedida, o grupo que contém as contas de trabalho, SQLRUserGroup, deve ter permissões de "Permitir logon localmente". Por padrão, esse direito é fornecido para todos os novos usuários locais, mas em algumas organizações mais rígidas políticas de grupo podem ser impostas.

![Autenticação implícita para R](media/implied-auth-rsql.png)

## <a name="security-of-worker-accounts"></a>Segurança de contas de trabalho

O mapeamento de um usuário externo do Windows ou logon SQL válido para uma conta de trabalho é válido somente para o tempo de vida do tempo de vida da consulta SQL que executa o script R.

Consultas paralelas do mesmo logon são mapeadas para a mesma conta de trabalho do usuário.

As pastas usadas para os processos são gerenciadas pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] usando o RLauncher e o acesso aos diretórios é restrito. A conta de trabalho não pode acessar todos os arquivos em pastas acima da pasta da própria conta, mas ela pode ler, gravar ou excluir filhos sob a pasta de trabalho de sessão que foi criada para a consulta SQL com o script R.

Para obter mais informações sobre como alterar o número de contas de trabalho, nomes de contas ou senhas de conta, consulte [modificar o pool de conta de usuário para o aprendizado de máquina do SQL Server](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

## <a name="security-isolation-for-multiple-external-scripts"></a>Isolamento de segurança para vários scripts externos

O mecanismo de isolamento se baseia em contas de usuário físico. Conforme os processos satélite são iniciados para o tempo de execução de uma linguagem específica, cada tarefa satélite usa a conta de trabalho especificada pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Se uma tarefa exigir vários satélites, tal como no caso de consultas paralelas, uma única conta de trabalho será usada para todas as tarefas relacionadas.

Nenhuma conta de trabalho pode ver ou manipular arquivos usados por outras contas de trabalho.
 
Se você for um administrador no computador, você poderá exibir os diretórios criados para cada processo. Cada diretório é identificado por seu GUID de sessão.

## <a name="see-also"></a>Consulte também

[Visão geral da arquitetura de aprendizado de máquina do SQL Server](../../advanced-analytics/r/architecture-overview-sql-server-r.md)
