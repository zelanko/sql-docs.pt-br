---
title: Segurança para SQL Server machine learning e R | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c04670464d23f0951a957df945a2e81b817ae134
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889182"
---
# <a name="security-for-sql-server-machine-learning-and-r"></a>Segurança para SQL Server machine learning e R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve a arquitetura geral de segurança que é usada para conectar o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] componentes relacionados ao tempo de execução R e mecanismo de banco de dados. Exemplos do processo de segurança são fornecidos para esses cenários comuns para usar o R em um ambiente corporativo:

+ Executando funções RevoScaleR em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] de um cliente de ciência de dados
+ Executar o R diretamente do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando procedimentos armazenados

## <a name="security-overview"></a>Visão geral de segurança

Um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] logon ou conta de usuário do Windows é necessária para executar scripts do R que usam dados do SQL Server ou que são executados com o SQL Server como o contexto de computação. Esse requisito se aplica a ambos [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] e o SQL Server 2017 [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)].

A conta de usuário ou logon identifica o *entidade de segurança*, que talvez seja necessário vários níveis de acesso, dependendo dos requisitos de script R:

+ Permissão para acessar o banco de dados em que o R está habilitado
+ Permissões para ler dados de objetos protegidos, como tabelas
+ A capacidade de gravar novos dados em uma tabela, como um modelo ou resultados de pontuação
+ A capacidade de criar novos objetos, como tabelas, procedimentos armazenados do que usam o script R ou personalizado funções de trabalho usar o R
+ O direito de instalar novos pacotes no computador do SQL Server, ou pacotes de usar o R fornecidos a um grupo de usuários. 

Portanto, cada pessoa que executa o código R usando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] como a execução do contexto deve ser mapeado para um logon no banco de dados. Na segurança do SQL Server, é geralmente mais fácil criar funções para gerenciar conjuntos de permissões e atribuir usuários a essas funções, em vez de individualmente, definir permissões de usuário. 

Por exemplo, suponha que você criou código R que é executado em seu laptop e você deseja executar esse código em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Você pode fazer isso apenas se essas condições forem atendidas:

+ O banco de dados permite conexões remotas.
+ Um logon SQL com o nome e a senha que você usou no código R foi adicionado ao [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] no nível de instância. Ou, se você estiver usando a autenticação integrada do Windows, o usuário do Windows especificado na cadeia de conexão deverá ser adicionado como um usuário na instância.
+ O logon do SQL ou o usuário do Windows deve ter a permissão para executar scripts externos. Em geral, essa permissão só pode ser adicionada por um administrador de banco de dados.
+ O logon SQL ou o usuário do Windows deverá ser adicionado como um usuário, com as permissões apropriadas, em cada banco de dados em que o trabalho do R executar qualquer uma destas operações:
    + Recuperação dados
    + Gravação ou atualização de dados 
    + Criação de novos objetos, tais como tabelas ou procedimentos armazenados

Depois que o logon ou conta de usuário do Windows foi provisionada e recebeu as permissões necessárias, você pode executar código R em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando um objeto de fonte de dados do R ou chamando um procedimento armazenado. Sempre que o R for iniciado no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], a segurança do mecanismo de banco de dados obtém o contexto de segurança do usuário que iniciou o trabalho de R ou executou o procedimento armazenado e gerencia os mapeamentos do usuário ou logon para objetos protegíveis. 

Portanto, todos os trabalhos de R que são iniciados de um cliente remoto devem especificar as informações de logon ou usuário como parte da cadeia de conexão.

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interação de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] segurança e segurança do Launchpad

Quando um script R é executado no contexto do computador do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], o serviço [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] obtém uma conta de trabalho disponível (uma conta de usuário local) de um pool de contas de trabalho estabelecido para o processo externo e usa essa conta de trabalho para executar as tarefas relacionadas. 

Por exemplo, se você iniciar um trabalho de R com suas credenciais de domínio do Windows, sua conta poderá ser mapeada para a conta de trabalho *SQLRUser01* do Launchpad.

Após o mapeamento para uma conta de trabalho, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] cria um token de usuário que é usado para iniciar processos. 

Quando todas as operações de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] forem concluídas, a conta de trabalho do usuário será marcada como livre e retornada ao pool.

Para obter mais informações sobre o serviço, consulte [Extensibility framework](../concepts/extensibility-framework.md). 

### <a name="implied-authentication"></a>Autenticação implícita

**Autenticação implícita** é o termo usado para o processo sob a qual o SQL Server obtém o usuário as credenciais e, em seguida, executa todas as tarefas de script externo em nome dos usuários, supondo que o usuário tem as permissões corretas no banco de dados. Autenticação implícita é particularmente importante se o script de R precisa fazer uma chamada ODBC fora do banco de dados do SQL Server. Por exemplo, o código pode recuperar uma lista menor de fatores de uma planilha ou outra fonte.

Para essas chamadas de loopback seja bem-sucedida, o grupo que contém as contas de trabalho, SQLRUserGroup, deve ter permissões de "Permitir logon localmente". Por padrão, esse direito é fornecido para todos os novos usuários locais, mas em algumas organizações políticas mais rígidas do grupo podem ser impostas.

![Autenticação implícita para R](media/implied-auth-rsql.png)

## <a name="security-of-worker-accounts"></a>Segurança de contas de trabalho

O mapeamento de um usuário externo do Windows ou logon SQL válido para uma conta de trabalho é válido somente para o tempo de vida da consulta SQL que executa o script de R.

Consultas paralelas do mesmo logon são mapeadas para a mesma conta de trabalho do usuário.

As pastas usadas para os processos são gerenciadas pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] usando o RLauncher e o acesso aos diretórios é restrito. A conta de trabalho não pode acessar todos os arquivos em pastas acima da pasta da própria conta, mas ela pode ler, gravar ou excluir filhos sob a pasta de trabalho de sessão que foi criada para a consulta SQL com o script R.

Para obter mais informações sobre como alterar o número de contas de trabalho, nomes de contas ou senhas de contas, consulte [modificar o pool de conta de usuário para o aprendizado de máquina do SQL Server](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).

## <a name="security-isolation-for-multiple-external-scripts"></a>Isolamento de segurança para vários scripts externos

O mecanismo de isolamento se baseia em contas de usuário físico. Conforme os processos satélite são iniciados para o tempo de execução de uma linguagem específica, cada tarefa satélite usa a conta de trabalho especificada pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Se uma tarefa exigir vários satélites, tal como no caso de consultas paralelas, uma única conta de trabalho será usada para todas as tarefas relacionadas.

Nenhuma conta de trabalho pode ver ou manipular arquivos usados por outras contas de trabalho.
 
Se você for um administrador no computador, você poderá exibir os diretórios criados para cada processo. Cada diretório é identificado por seu GUID de sessão.

## <a name="see-also"></a>Confira também

[Visão geral da arquitetura para o aprendizado de máquina do SQL Server](../../advanced-analytics/r/architecture-overview-sql-server-r.md)
