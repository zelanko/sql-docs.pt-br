---
title: "Funções de usuário | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: be0ec384-e03b-4483-96ca-02b289804d6a
caps.latest.revision: "7"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f01d18033764d683871cbc8d5883e25c78b7d958
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="user-roles"></a>Funções de usuário
  Esta seção descreve as funções de usuário para o Serviço Change Data Capture para Oracle da Attunity. As funções descritas são funções de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , funções do Windows ou funções de banco de dados Oracle.  
  
## <a name="windows-user-roles"></a>Funções de usuário do Windows  
 Veja a seguir a descrição das funções de usuário do Windows usadas pelo Serviço Oracle CDC.  
  
### <a name="computer-administrator-oracle-cdc-service"></a>Administrador do computador: Serviço Oracle CDC  
 O administrador do computador é um usuário do Windows responsável por criar e manter o Serviço CDC no computador. Este usuário deve pertencer ao grupo de administradores do computador local.  
  
 As tarefas executadas pelo Administrador de Computador do Serviço Oracle CDC incluem:  
  
-   Instalar o software do Serviço CDC para Oracle  
  
-   Criar um serviço Windows Oracle CDC  
  
-   Configurar a conexão do Serviço CDC para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino (cadeia de conexão e credenciais)  
  
-   Garantir que a senha mestre do Serviço CDC com a qual as credenciais de mineração de logs da Oracle esteja protegida  
  
-   Excluir um serviço do Windows do Serviço CDC  
  
-   Desinstalar o software do Serviço CDC para Oracle  
  
-   Manter o software do Serviço CDC para Oracle (por exemplo, instalar as atualizações)  
  
-   Iniciar e parar o serviço do Windows do Serviço CDC  
  
 Ao trabalhar com configurações de alta disponibilidade, como clusters de failover da Microsoft, o administrador do computador deve ter responsabilidades e permissões adicionais como:  
  
-   Instalação e manutenção do software do Serviço CDC para Oracle em todos os nós de cluster.  
  
-   Definir recursos genéricos de serviço de cluster para o serviço do Windows do Serviço CDC em vários nós de cluster.  
  
-   Agir como o administrador autorizado no computador em que o Serviço CDC para Oracle está instalado. Esta pessoa instala o Serviço CDC para Oracle e usa o Console de Configuração de Serviço CDC para configurar um Serviço CDC para Oracle em um computador local.  
  
### <a name="service-account-oracle-cdc-service"></a>Conta de serviço: Serviço Oracle CDC  
 Essa Conta de Serviço Windows do Serviço Oracle CDC é uma conta do Windows usada para executar o Serviço Oracle CDC (a conta de serviço).  
  
 O único privilégio exigido necessário para a conta de serviço é poder usar o cliente Oracle e o provedor ODBC do cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta conta não precisa acessar arquivos a menos que isso seja exigido por provedores específicos (por exemplo, se a cadeia de conexão do cliente Oracle referenciar instâncias de banco de dados Oracle em um arquivo **tnsnames.ora** , isso significará que esse arquivo estará acessível à leitura para uma conta de serviço).  
  
 Ao criar um Serviço Oracle CDC no Windows Vista ou Windows Server 2008, a conta de serviço padrão é a conta NETWORK SERVICE.  
  
 No Windows 7, Windows Server 2008 R2 e posterior, a conta de serviço padrão é NT Service\\<service-name>.  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é executado em outra máquina ou é uma instância clusterizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o serviço precisa se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino usando autenticação do Windows, a conta de serviço deve ser uma conta de domínio.  
  
## <a name="sql-server-user-roles"></a>Funções de usuário do SQL Server  
 Veja a seguir a descrição das funções de usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usadas pelo Serviço Oracle CDC.  
  
### <a name="oracle-cdc-service-administrator"></a>Administrador do Serviço Oracle CDC  
 O Administrador do Serviço CDC é um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com controle total sobre os artefatos do Serviço Oracle CDC na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino. O Administrador do Serviço CDC usa o Console de Designer do Oracle CDC para criar Instâncias Oracle CDC.  
  
 O Administrador do Serviço CDC deve ter as funções de servidor fixas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] public **e** dbcreator **do**.  
  
 As tarefas executadas pelo Administrador do Serviço CDC incluem:  
  
-   Preparar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar Instâncias Oracle CDC (que são bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ). Nessa tarefa, um banco de dados especial chamado MSXDBCDC é criado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Criar um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da Instância Oracle CDC. A tarefa inclui habilitar o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recém-criado para o CDC que exige um administrador do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] system administrator**sysadmin**.  
  
-   Criar uma Instância Oracle CDC. Esta tarefa inclui fornecer informações sobre o banco de dados Oracle de origem e tabelas capturadas que exigem um administrador de banco de dados Oracle.  
  
-   Manter a Instância Oracle CDC com o passar do tempo, o que inclui adição/remoção de instâncias de captura e atualização de configuração.  
  
-   Habilitar ou desabilitar uma Instância Oracle CDC.  
  
-   Monitorar o estado de uma Instância Oracle CDC.  
  
-   Solucionar problemas que afetam a Instância Oracle CDC.  
  
 O Administrador do Serviços CDC está, pelo menos inicialmente, na função de banco de dados fixa **db_owner** para o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC associado com a Instância Oracle CDC. Isto dá ao Administrador do Serviço CDC acesso aos dados de alteração armazenados no banco de dados CDC. Uma vez criada, a função **db_owner** do banco de dados CDC pode ser atribuída a um usuário diferente que pode conduzir todas as tarefas listadas acima exceto preparar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e criar outra Instância Oracle CDC).  
  
 O Administrador do Serviço CDC não precisa saber a senha mestra especificada com a criação do serviço do Windows do Oracle CDC.  
  
### <a name="system-administrator"></a>Administrador do Sistema  
 O administrador do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve ter a função de servidor fixa **sysadmin** na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associada com o Serviço Oracle CDC.  
  
 Há somente uma tarefa específica do Oracle CDC conduzida com o Administrador de Sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que é habilitar o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma Instância Oracle CDC para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC. Esta tarefa é realizada usando o console de Designer do Oracle CDC ao criar uma nova Instância Oracle CDC.  
  
### <a name="oracle-cdc-service-user"></a>Usuário do Serviço Oracle CDC  
 O usuário do Serviço Oracle CDC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que é usado pelo Serviço Oracle CDC para executar seu trabalho no MSXDBCDC e todas as Instâncias Oracle CDC (bancos de dados CDC) tratados por este serviço.  
  
 O usuário do Serviço Oracle CDC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser concedido o seguinte:  
  
-   Membro das funções de banco de dados fixas **db_dlladmin**, **db_datareader**e **db_datawriter** para todos os bancos de dados CDC tratados pelo servidor.  
  
-   Membro das funções de banco de dados fixas **db_datareader** e **db_datawriter** para o banco de dados MSXDBCDC.  
  
 Como o Serviço Oracle CDC usa um logon único do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para funcionar com todos os bancos de dados CDC e o banco de dados MSXDBCDC, este logon deve ser mapeado em todos estes bancos de dados.  
  
### <a name="oracle-cdc-change-consumer"></a>Consumidor de Alteração Oracle CDC  
 O Consumidor de Alteração Oracle CDC é um usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que consome alterações armazenadas nas tabelas CDC no banco de dados da Instância Oracle CDC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Este usuário determina a função de usuário que é necessária para acessar cada tabela CDC por meio das funções CDC geradas pela infraestrutura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC. Se nenhuma função de usuário for especificada quando uma instância de captura é especificada, o acesso às alterações será limitado ao membro da função de banco de dados fixa **db_owner** do banco de dados CDC.  
  
## <a name="oracle-user-roles"></a>Funções de usuário Oracle  
 Veja a seguir a descrição das funções de usuário do Oracle usadas pelo Serviço Oracle CDC.  
  
### <a name="database-administrator-dba"></a>Administrador de banco de dados (DBA)  
 O administrador de banco de dados Oracle (DBA) é um usuário de banco de dados Oracle. As tarefas executadas pelo DBA da Oracle incluem:  
  
-   Definir o banco de dados Oracle de origem para funcionar em modo ARCHIVELOG.  
  
-   Configurar um usuário de mineração de logs com as permissões necessárias.  
  
-   Definir o log suplementar para tabelas capturadas.  
  
-   Ajudar a restaurar arquivos de log de transação arquivados que não estão mais disponíveis para que possam ser processados.  
  
 O administrador de banco de dados Oracle pode obter scripts SQL de Oracle que precisam ser executados, para que possam ser avaliados antes de serem executados. O administrador de banco de dados Oracle também pode executar scripts SQL de Oracle diretamente do Console de Designer do Oracle CDC.  
  
 Se o administrador de banco de dados Oracle escolher usar o console de Designer do Oracle CDC, as credenciais de administrador não serão mantidas com exceção do contexto (caixa de diálogo) no qual eles foram usados.  
  
 O administrador de banco de dados Oracle funciona em coordenação com o administrador do Serviço Oracle CDC na configuração de Instâncias Oracle CDC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="log-mining-user"></a>Usuário de mineração de logs  
 O usuário do Minerador de Logs Oracle é um usuário de banco de dados Oracle especial que tem os privilégios necessários para acessar e processar os logs de transação Oracle.  
  
 As credenciais para este usuário são armazenadas no banco de dados da Instância Oracle CDC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando criptografia de chave assimétrica. Eles só estão acessíveis ao Serviço Oracle CDC, mas não para o proprietário do banco de dados da Instância Oracle CDC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 A lista a seguir descreve os privilégios necessários que devem ser concedidos ao usuário de mineração de logs:  
  
-   SELECT em \<qualquer-tabela-capturada>  
  
-   SELECT ANY TRANSACTION  
  
-   EXECUTE em DBMS_LOGMNR  
  
-   SELECT em V$LOGMNR_CONTENTS  
  
-   SELECT em V$ARCHIVED_LOG  
  
-   SELECT em V$LOG  
  
-   SELECT em V$LOGFILE  
  
-   SELECT em V$DATABASE  
  
-   SELECT em V$THREAD  
  
-   SELECT em ALL_INDEXES  
  
-   SELECT em ALL_OBJECTS  
  
-   SELECT em DBA_OBJECTS  
  
-   SELECT em ALL_TABLES  
  
 Se algum destes privilégios não puder ser concedido a um V$xxx, ele deverá ser concedido ao V $xxx.  
  
### <a name="schema-user"></a>Usuário do esquema  
 O Usuário do Esquema Oracle é um usuário do Oracle com acesso de leitura para o esquema das tabelas do Oracle a ser capturado. Este usuário é necessário ao trabalhar com o console de Designer do Oracle CDC para recuperar a lista de esquema do Oracle, tabelas a serem capturadas e suas colunas, índices e chaves.  
  
 As credenciais para este usuário nunca são armazenadas. Elas são solicitadas pelo console de Designer CDC toda vez em que são necessárias e são mantidas para o restante das sessões da interface do usuário.  
  
  
