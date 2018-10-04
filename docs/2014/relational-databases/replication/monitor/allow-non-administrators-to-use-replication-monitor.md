---
title: Permitir que não administradores usem o Replication Monitor, | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e0c880bbb7c21ec7d0a766f8bdf0876d4962d10b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219846"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>Permitir que não administradores usem o Replication Monitor
  Este tópico descreve como permitir que não administradores usem o Replication Monitor no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O Replication Monitor pode ser usado por usuários que são membros das seguintes funções:  
  
-   A função de servidor fixa **sysadmin** .  
  
     Esses usuários podem monitorar a replicação e possuem controle total sobre a modificação de propriedades de replicação como cronogramas de agentes, perfis de agentes, etc...  
  
-   O `replmonitor` função de banco de dados no banco de dados de distribuição.  
  
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
 Para permitir que usuários não administradores usem o Replication Monitor, um membro do **sysadmin** função de servidor fixa deve adicionar o usuário no banco de dados de distribuição e atribuir ao usuário para o `replmonitor` função.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>Para permitir que não administradores usem o Replication Monitor  
  
1.  No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conecte-se ao Distribuidor e, em seguida, expanda o nó do servidor.  
  
2.  Expanda **Bancos de Dados**, expanda **Bancos de Dados do Sistema**e, em seguida, expanda o banco de dados de distribuição (nomeado **distribuição** por padrão).  
  
3.  Expanda **Segurança**, clique com o botão direito do mouse em **Usuários**e, em seguida, clique em **Novo Usuário**.  
  
4.  Digite um nome de usuário e logon para o usuário.  
  
5.  Selecione um esquema padrão de `replmonitor`.  
  
6.  Selecione o `replmonitor` caixa de seleção de **associação à função de banco de dados** grade.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>Para adicionar um usuário à função de banco de dados fixo replmonitor  
  
1.  No Distribuidor no banco de dados de distribuição, execute [sp_helpuser &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpuser-transact-sql). Se o usuário não estiver listado em `UserName` no conjunto de resultados, o usuário deve ter acesso ao banco de dados de distribuição usando o [CREATE USER &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-user-transact-sql) instrução.  
  
2.  No distribuidor no banco de dados de distribuição, execute [sp_helprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql), especificando um valor de `replmonitor` para o **@rolename** parâmetro. Se o usuário estiver listado em `MemberName` no conjunto de resultados, o usuário já pertence a essa função.  
  
3.  Se o usuário não pertencer à `replmonitor` função, execute [sp_addrolemember &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) no distribuidor no banco de dados de distribuição. Especifique um valor de `replmonitor` para **@rolename** e o nome do usuário de banco de dados ou o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] logon do Windows que está sendo adicionado para **@membername**.  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>Para remover um usuário da função de banco de dados fixo replmonitor  
  
1.  Para verificar se o usuário pertence a `replmonitor` função, execute [sp_helprolemember &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql) no distribuidor no banco de dados de distribuição e especifique um valor de `replmonitor` para **@rolename**. Se o usuário não estiver listado em `MemberName` no conjunto de resultados, o usuário não pertence atualmente à essa função.  
  
2.  Se o usuário pertencer à `replmonitor` função, execute [sp_droprolemember &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql) no distribuidor no banco de dados de distribuição. Especifique um valor de `replmonitor` para **@rolename** e o nome do banco de dados do usuário ou o logon do Windows que está sendo removido para **@membername**.  
  
  
