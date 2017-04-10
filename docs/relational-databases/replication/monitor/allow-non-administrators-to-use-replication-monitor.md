---
title: "Permitir que n&#227;o administradores usem o Replication Monitor | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Replication Monitor, acesso de não administradores"
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Permitir que n&#227;o administradores usem o Replication Monitor
  Este tópico descreve como permitir que não administradores usem o Replication Monitor no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O Replication Monitor pode ser usado por usuários que são membros das seguintes funções:  
  
-   A função de servidor fixa **sysadmin** .  
  
     Esses usuários podem monitorar a replicação e possuem controle total sobre a modificação de propriedades de replicação como cronogramas de agentes, perfis de agentes, etc...  
  
-   A função de banco de dados **replmonitor** no banco de dados de distribuição.  
  
     Esses usuários podem monitorar a replicação, mas não podem modificar nenhuma propriedade de replicação.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para permitir que não administradores usem o Replication Monitor, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para permitir que usuários não administradores usem o Replication Monitor, um membro do **sysadmin** função de servidor fixa deve adicionar o usuário no banco de dados de distribuição e atribuir a esse usuário o **replmonitor** função.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### Para permitir que não administradores usem o Replication Monitor  
  
1.  No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conecte-se ao Distribuidor e, em seguida, expanda o nó do servidor.  
  
2.  Expanda **bancos de dados**, expanda **bancos de dados do sistema**, e, em seguida, expanda o banco de dados de distribuição (chamado **distribuição** por padrão).  
  
3.  Expanda **segurança**, clique com botão direito **usuários**, e, em seguida, clique em **novo usuário**.  
  
4.  Digite um nome de usuário e logon para o usuário.  
  
5.  Selecione um esquema padrão de **replmonitor**.  
  
6.  Marque a caixa de seleção **replmonitor** na grade **Associação à função de banco de dados** .  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para adicionar um usuário à função de banco de dados fixo replmonitor  
  
1.  No distribuidor no banco de dados de distribuição, execute [sp_helpuser & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md). Se o usuário não estiver listado em **UserName** no conjunto de resultados, o usuário deve ter acesso ao banco de dados de distribuição usando o [Criar usuário & #40. O Transact-SQL e 41;](../../../t-sql/statements/create-user-transact-sql.md) instrução.  
  
2.  No distribuidor no banco de dados de distribuição, execute [sp_helprolemember & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md), especificando um valor de **replmonitor** para o **@rolename** parâmetro. Se o usuário estiver listado em **MemberName** no conjunto de resultados, o usuário já pertence a essa função.  
  
3.  Se o usuário não pertence ao **replmonitor** função, execute [sp_addrolemember & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) no distribuidor no banco de dados de distribuição. Especifique um valor de **replmonitor** para **@rolename** e o nome do banco de dados do usuário ou o logon do Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que está sendo adicionado para **@membername**.  
  
#### Para remover um usuário da função de banco de dados fixo replmonitor  
  
1.  Para verificar se o usuário pertence a **replmonitor** função, execute [sp_helprolemember & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) no distribuidor no banco de dados de distribuição e especifique um valor de **replmonitor** para **@rolename**. Se o usuário não estiver listado em **MemberName** no conjunto de resultados, ele não pertence atualmente a essa função.  
  
2.  Se o usuário pertencer ao **replmonitor** função, execute [sp_droprolemember & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) no distribuidor no banco de dados de distribuição. Especifique um valor de **replmonitor** para **@rolename** e o nome do banco de dados do usuário ou o logon do Windows que está sendo removido para **@membername**.  
  
  