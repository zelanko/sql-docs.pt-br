---
title: "Vis&#227;o geral de seguran&#231;a (SQL Server R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8fc84754-7fbf-4c1b-9150-7d88680b3e68
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# Vis&#227;o geral de seguran&#231;a (SQL Server R Services)

Este tópico descreve a arquitetura geral de segurança que é usada para conectar o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] engine e os componentes relacionados ao tempo de execução R do banco de dados. Exemplos do processo de segurança são fornecidos para cenários comuns para usar o R em um ambiente corporativo:

+ Executando funções RevoScaleR em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] de um cliente de ciência de dados
+ Executar R diretamente do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando procedimentos armazenados

## Visão geral de segurança

Um [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] logon ou conta de usuário do Windows é necessária para executar todos os trabalhos de R que utilizam [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)]. A conta de logon ou usuário identifica o *entidade de segurança*, que deve ter permissão para acessar o banco de dados onde R é executado, bem como permissões para ler dados de objetos protegidos, como tabelas, ou para escrever novos dados ou adicionar novos objetos, se necessário, o trabalho de R.

Portanto, é um requisito obrigatório que cada pessoa que executa o código R em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] deve ser mapeado para um logon no banco de dados, independentemente de que o código é enviado de um cliente de ciência de dados remota usando as funções RevoScaleR ou iniciado usando um procedimento armazenado T-SQL. 

Por exemplo, suponha que você criou algum código R que é executado em seu laptop e você deseja executar esse código em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Certifique-se de que as seguintes condições forem atendidas:

+ O banco de dados permite conexões remotas.
+ Foi adicionado um logon do SQL com o nome e a senha que você usou no código R para o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] no nível de instância. Ou, se você estiver usando a autenticação integrada do Windows, o usuário do Windows especificado na cadeia de conexão deve ser adicionado como um usuário na instância.
+ O logon do SQL ou o usuário do Windows deve ter a permissão para executar scripts externos. Em geral, essa permissão só pode ser adicionada por um administrador de banco de dados.
+ O logon do SQL ou o usuário da janela deve ser adicionado como um usuário, com permissões apropriadas, em cada banco de dados em que o trabalho de R executa qualquer uma dessas operações:
    + Recuperando dados
    + Gravar ou atualizando dados 
    + Criando novos objetos, como tabelas ou procedimentos armazenados

Após o logon ou conta de usuário do Windows foi provisionada e recebeu as permissões necessárias, você pode executar código R em [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] usando um objeto de fonte de dados R ou chamar procedimentos armazenados. Sempre que R é iniciado no [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], a segurança do mecanismo de banco de dados obtém o contexto de segurança do usuário que iniciou o trabalho de R e gerencia os mapeamentos do usuário ou logon objetos protegíveis. 

Portanto, todos os trabalhos de R são iniciados de um cliente remoto devem especificar as informações de logon ou usuário como parte da cadeia de conexão.


## Interação de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] segurança e barra inicial

Quando um script R é executado no contexto do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] computador, o [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] serviço obtém uma conta de trabalho disponível (uma conta de usuário local) de um pool de contas de trabalho estabelecida para o processo externo e usa essa conta de trabalho para executar as tarefas relacionadas. 

Por exemplo, se você iniciar um trabalho de R com suas credenciais de domínio do Windows, sua conta pode ser mapeada para a conta de trabalho da barra inicial *SQLRUser01*.

Após o mapeamento para uma conta de trabalho, [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] cria um token de usuário que é usado para iniciar processos. 

Quando todos os [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] operações forem concluídas, a conta de trabalho do usuário é marcada como livre e retornada ao pool.

Para obter mais informações sobre [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)], consulte [novos componentes do SQL Server dão suporte à integração de R](../../advanced-analytics/r-services/new-components-in-sql-server-to-support-r-services.md).

## Segurança de contas de trabalho
Esse mapeamento de um usuário externo do Windows ou logon SQL válido para uma conta de trabalho é válido somente para o tempo de vida do tempo de vida da consulta SQL que executa o script R. 

Consultas paralelas do mesmo logon são mapeadas para a mesma conta de trabalho do usuário.

As pastas usadas para os processos gerenciadas pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] usando RLauncher, e diretórios são acesso restrito. A conta de trabalho não pode acessar todos os arquivos em pastas acima seu próprio, mas ele pode ler, gravar ou excluir filhos sob a pasta de trabalho de sessão que foi criado para a consulta SQL com o script R.

Para obter mais informações sobre como alterar o número de contas de trabalho, nomes de contas ou senhas de conta, consulte [modifique o Pool de conta de usuário para serviços do SQL Server R](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md).


## Isolamento de segurança para vários Scripts externos

O mecanismo de isolamento se baseia em contas de usuário físico. Conforme os processos de satélite são iniciados para um idioma específico de tempo de execução, cada tarefa de satélite usa a conta de trabalho especificada pelo [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)]. Se uma tarefa exigir vários satélites, por exemplo, no caso de consultas paralelas, uma único trabalhador conta é usada para todas as tarefas relacionadas.

Nenhuma conta de trabalho pode ver ou manipular arquivos usados por outras contas de trabalho.
 
Se você for um administrador no computador, você pode exibir os diretórios criados para cada processo. Cada diretório é identificado por seu GUID de sessão.

## Consulte também
[Visão geral sobre arquitetura](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)