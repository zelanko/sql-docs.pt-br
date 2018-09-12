---
title: Visão geral de segurança para o Python no SQL Server Machine Learning | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: a33701283635327fcaac4a9629cb02044b30dda8
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43890052"
---
# <a name="security-overview-for-python-in-sql-server-machine-learning"></a>Visão geral de segurança para o Python no Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tópico descreve a arquitetura de segurança que é usada para conectar o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] componentes de Python e o mecanismo de banco de dados. Exemplos do processo de segurança são fornecidos para dois cenários comuns: execução de Python no SQL Server usando um procedimento armazenado e execução de Python com o SQL Server como o contexto de computação remota.

## <a name="security-overview"></a>Visão geral de segurança

Um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] logon ou conta de usuário do Windows é necessária para executar o script de Python no SQL Server. Eles *as entidades de segurança* são gerenciados na instância e no nível de banco de dados e identificar os usuários que têm permissão para se conectar ao banco de dados, ler e gravar dados ou criar objetos de banco de dados como tabelas ou procedimentos armazenados. Além disso, os usuários que executarem o script Python devem ter permissão para executar o script externo no nível do banco de dados.

Até mesmo os usuários estão usando o Python em uma ferramenta externa devem ser mapeados para um logon ou conta no banco de dados se o usuário precisa para executar o Python código no banco de dados, ou acessar objetos de banco de dados e dados. As mesmas permissões são necessárias se o script Python é enviado de um cliente de ciência de dados remoto ou ao uso de um procedimento armazenado T-SQL.

Por exemplo, suponha que você criou um script Python que é executado em seu laptop e você deseja executar esse código em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Você deve certificar-se de que as seguintes condições sejam atendidas:

+ O banco de dados permite conexões remotas.
+ O logon SQL ou a conta do Windows que você usou para acesso ao banco de dados foi adicionada para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] no nível da instância.
+ O logon SQL ou o usuário do Windows deve receber permissão para executar scripts externos. Em geral, essa permissão só pode ser adicionada por um administrador de banco de dados.
+ O logon do SQL ou o usuário da janela deve ser adicionado como um usuário, com permissões apropriadas, em cada banco de dados em que o script de Python executa qualquer uma dessas operações:
    + Recuperação dados
    + Gravação ou atualização de dados
    + Criação de novos objetos, tais como tabelas ou procedimentos armazenados

Depois que o logon ou conta de usuário do Windows foi provisionada e recebeu as permissões necessárias, você pode executar código Python em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando os objetos de fonte de dados fornecidos pelo **revoscalepy** biblioteca, ou chamando um armazenado procedimento que contém o script Python.

Sempre que um script Python é iniciado no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], a segurança do mecanismo de banco de dados obtém o contexto de segurança do usuário que iniciou o trabalho e gerencia os mapeamentos do usuário ou logon para objetos protegíveis.

Portanto, todos os scripts de Python que são iniciados de um cliente remoto devem especificar as informações de logon ou usuário como parte da cadeia de conexão.

## <a name="interaction-of-includessnoversionmdincludesssnoversion-mdmd-security-and-launchpad-security"></a>Interação de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] segurança e segurança do Launchpad

Quando um script Python é executado no contexto do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] computador, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] serviço obtém uma conta de trabalho disponíveis (uma conta de usuário local) de um pool de contas de trabalho estabelecido para processos externos e usa a conta de trabalho para Execute as tarefas relacionadas.

Por exemplo, suponha que você inicia um script do Python com suas credenciais de domínio do Windows. SQL Server obtém suas credenciais e mapeia a tarefa a uma conta de trabalho do Launchpad disponível, como *SQLRUser01*.

> [!NOTE]
> O nome do grupo de contas de trabalho é o mesmo, independentemente se você estiver usando o R ou Python. No entanto, um grupo separado é criado para cada instância em que você pode habilitar qualquer linguagem externa.

Após o mapeamento para uma conta de trabalho, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] cria um token de usuário que é usado para iniciar processos. 

Quando todas as operações de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] forem concluídas, a conta de trabalho do usuário será marcada como livre e retornada ao pool.

Para obter mais informações sobre o serviço, consulte [Extensibility framework](../concepts/extensibility-framework.md).

### <a name="implied-authentication"></a>Autenticação implícita

**Autenticação implícita** é o termo usado para o processo sob a qual o SQL Server obtém o usuário as credenciais e, em seguida, executa todas as tarefas de script externo em nome dos usuários, supondo que o usuário tem as permissões corretas no banco de dados. Autenticação implícita é particularmente importante se o script de Python precisa fazer uma chamada ODBC fora do banco de dados do SQL Server. Por exemplo, o código pode recuperar uma lista menor de fatores de uma planilha ou outra fonte.

Para essas chamadas de loopback seja bem-sucedida, o grupo que contém as contas de trabalho, SQLRUserGroup, deve ter permissões de "Permitir logon localmente". Por padrão, esse direito é fornecido para todos os novos usuários locais, mas em algumas organizações políticas mais rígidas do grupo podem ser impostas.

![Autenticação implícita para R](media/implied-auth-python2.png)

## <a name="security-of-worker-accounts"></a>Segurança de contas de trabalho

O mapeamento de um usuário externo do Windows ou logon SQL válido para uma conta de trabalho é válido somente para o procedimento armazenado de tempo de vida do SQL que executa o script de Python.

Consultas paralelas do mesmo logon são mapeadas para a mesma conta de trabalho do usuário.

As pastas usadas para os processos são gerenciadas pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], e os diretórios têm o acesso restrito. Para o Python, PythonLauncher realiza essa tarefa. Cada conta de trabalho individuais é restrito a sua própria pasta e não pode acessar arquivos em pastas acima de seu próprio nível. No entanto, a conta de trabalho pode ler, gravar ou excluir filhos sob a pasta de trabalho de sessão que foi criado.

Para obter mais informações sobre como alterar o número de contas de trabalho, nomes de contas ou senhas de contas, consulte [modificar o pool de conta de usuário para o aprendizado de máquina do SQL Server](../../advanced-analytics/r/modify-the-user-account-pool-for-sql-server-r-services.md).


## <a name="security-isolation-for-multiple-external-scripts"></a>Isolamento de segurança para vários scripts externos

O mecanismo de isolamento se baseia em contas de usuário físico. Conforme os processos satélite são iniciados para o tempo de execução de uma linguagem específica, cada tarefa satélite usa a conta de trabalho especificada pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Se uma tarefa exigir vários satélites, tal como no caso de consultas paralelas, uma única conta de trabalho será usada para todas as tarefas relacionadas.

Nenhuma conta de trabalho pode ver ou manipular arquivos usados por outras contas de trabalho.

Se você for um administrador no computador, você poderá exibir os diretórios criados para cada processo. Cada diretório é identificado por seu GUID de sessão.

## <a name="see-also"></a>Consulte também

[Visão geral da arquitetura](../../advanced-analytics/python/architecture-overview-sql-server-python.md)
