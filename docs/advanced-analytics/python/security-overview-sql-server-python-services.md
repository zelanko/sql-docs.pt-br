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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6ddfc3ccb67d017dc618cfbb7e7680c0164f3a21
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="security-overview"></a>Visão geral de segurança

Este tópico descreve a arquitetura de segurança que é usada para conectar o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] componentes de Python e mecanismo de banco de dados. Exemplos do processo de segurança são fornecidos para dois cenários comuns: executando Python no SQL Server usando um procedimento armazenado e executando o Python com o SQL Server como o contexto de computação remota.

## <a name="security-overview"></a>Visão geral de segurança

Um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] logon ou conta de usuário do Windows é necessário para executar script Python no SQL Server. A conta de logon ou usuário identifica o *entidade de segurança*, que deve ter permissão para acessar o banco de dados onde os dados são recuperados. Dependendo se o script de Python cria novos objetos ou grava novos dados, o usuário talvez precise de permissões para criar tabelas, gravar dados ou criar funções personalizadas ou procedimentos armazenados.

Portanto, é um requisito restrito que cada pessoa que executa o código Python em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] deve ser mapeado para um logon ou conta no banco de dados. Essa restrição se aplica independentemente se o script for enviado de um cliente de ciência de dados remotos ou usando um procedimento armazenado T-SQL foi iniciado.

Por exemplo, suponha que você criou um script de Python é executado em seu laptop, e você deseja executar esse código em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Você deve certificar-se de que as seguintes condições sejam atendidas:

+ O banco de dados permite conexões remotas.
+ O logon do SQL ou a conta do Windows que você usou para acesso ao banco de dados foi adicionada para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] no nível de instância.
+ O logon SQL ou o usuário do Windows deve receber permissão para executar scripts externos. Em geral, essa permissão só pode ser adicionada por um administrador de banco de dados.
+ O logon do SQL ou o usuário da janela deve ser adicionado como um usuário, com permissões apropriadas, em cada banco de dados em que o script de Python executa qualquer uma dessas operações:
    + Recuperação dados
    + Gravação ou atualização de dados
    + Criação de novos objetos, tais como tabelas ou procedimentos armazenados

Depois que o logon ou conta de usuário do Windows foi provisionada e recebeu as permissões necessárias, você pode executar o código Python em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando os objetos de fonte de dados fornecidos pelo **revoscalepy** biblioteca, ou chamando um armazenado procedimento que contém o script de Python.

Sempre que um script Python é iniciado de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], a segurança do mecanismo de banco de dados obtém o contexto de segurança do usuário que iniciou o trabalho e gerencia os mapeamentos do usuário ou logon em objetos protegíveis.

Portanto, todos os scripts de Python são iniciados de um cliente remoto devem especificar as informações de logon ou usuário como parte da cadeia de conexão.


## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interação entre Segurança do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e Segurança do LaunchPad

Quando um script Python é executado no contexto da [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] computador, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] serviço obtém uma conta de trabalho disponível (uma conta de usuário local) de um pool de contas de trabalho estabelecido para processos externos e usa a conta de trabalho para Execute as tarefas relacionadas.

Por exemplo, suponha que você iniciar um script Python com suas credenciais de domínio do Windows. SQL Server obterá suas credenciais e mapeá-la para uma conta de trabalho disponível barra inicial, como *SQLRUser01*.

> [!NOTE]
> O nome do grupo de contas de trabalho é o mesmo, independentemente de se você estiver usando o R ou Python. No entanto, um grupo separado é criado para cada instância em que você habilitar qualquer linguagem externa.

Após o mapeamento para uma conta de trabalho, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] cria um token de usuário que é usado para iniciar processos. 

Quando todas as operações de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] forem concluídas, a conta de trabalho do usuário será marcada como livre e retornada ao pool.

Para obter mais informações sobre [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], consulte [novos componentes do SQL Server dão suporte à integração do Python](../../advanced-analytics/python/new-components-in-sql-server-to-support-python-integration.md).

> [!NOTE]
> Para a barra inicial gerenciar as contas de trabalho e executar trabalhos de Python, o grupo que contém as contas de trabalho, *SQLRUserGroup*, deve ter permissões de "Permitir logon localmente"; caso contrário, o tempo de execução do Python não pode ser iniciado. Por padrão, esse direito é fornecido para todos os novos usuários locais, mas em algumas organizações mais rígidas políticas de grupo podem ser impostas, que impedirá que as contas de trabalho conectem-se ao SQL Server para trabalhos de Python.

## <a name="security-of-worker-accounts"></a>Segurança de contas de trabalho

O mapeamento de um usuário externo do Windows ou logon SQL válido para uma conta de trabalho é válido somente para o procedimento armazenado de tempo de vida do SQL que executa o script de Python.

Consultas paralelas do mesmo logon são mapeadas para a mesma conta de trabalho do usuário.

Diretórios usados para os processos gerenciados pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], e diretórios são acesso restrito. Para Python, PythonLauncher executa essa tarefa. Cada conta de trabalho individuais é restrito a sua própria pasta e não pode acessar arquivos em pastas acima do seu próprio nível. No entanto, a conta de trabalho pode ler, gravar ou excluir filhos sob a pasta de trabalho de sessão que foi criado.

Para obter mais informações sobre como alterar o número de contas de trabalho, nomes de conta ou senhas de conta, consulte [Modificar o pool de contas de usuário para o SQL Server R Services](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).


## <a name="security-isolation-for-multiple-external-scripts"></a>Isolamento de segurança para vários scripts externos

O mecanismo de isolamento se baseia em contas de usuário físico. Conforme os processos satélite são iniciados para o tempo de execução de uma linguagem específica, cada tarefa satélite usa a conta de trabalho especificada pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Se uma tarefa exigir vários satélites, tal como no caso de consultas paralelas, uma única conta de trabalho será usada para todas as tarefas relacionadas.

Nenhuma conta de trabalho pode ver ou manipular arquivos usados por outras contas de trabalho.

Se você for um administrador no computador, você poderá exibir os diretórios criados para cada processo. Cada diretório é identificado por seu GUID de sessão.

## <a name="see-also"></a>Consulte também

[Visão geral de arquitetura](../../advanced-analytics/python/architecture-overview-sql-server-python.md)

