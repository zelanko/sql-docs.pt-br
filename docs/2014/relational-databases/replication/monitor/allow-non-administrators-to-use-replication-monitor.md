---
title: Permitir que não administradores usem o Replication Monitor, | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e8f03d12d3ac1695d4f6d000c8eab89a42004fd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62667384"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>Permitir que não administradores usem o Replication Monitor
  Este tópico descreve como permitir que não administradores usem o Replication Monitor no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O Replication Monitor pode ser usado por usuários que são membros das seguintes funções:  
  
-   A função de servidor fixa **sysadmin** .  
  
     Esses usuários podem monitorar a replicação e possuem controle total sobre a modificação de propriedades de replicação como cronogramas de agentes, perfis de agentes, etc...  
  
-   A `replmonitor` função de banco de dados no banco de dados de distribuição.  
  
     Esses usuários podem monitorar a replicação, mas não podem modificar nenhuma propriedade de replicação.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para permitir que não administradores usem o Replication Monitor, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Para permitir que não administradores usem o Replication Monitor, um membro da função de servidor fixa **sysadmin** deve adicionar o usuário ao banco de dados de distribuição e atribuir esse usuário `replmonitor` à função.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>Para permitir que não administradores usem o Replication Monitor  
  
1.  No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conecte-se ao Distribuidor e, em seguida, expanda o nó do servidor.  
  
2.  Expanda **Bancos de Dados**, expanda **Bancos de Dados do Sistema**e, em seguida, expanda o banco de dados de distribuição (nomeado **distribuição** por padrão).  
  
3.  Expanda **Segurança**, clique com o botão direito do mouse em **Usuários**e, em seguida, clique em **Novo Usuário**.  
  
4.  Digite um nome de usuário e logon para o usuário.  
  
5.  Selecione um esquema padrão de `replmonitor`.  
  
6.  Marque a `replmonitor` caixa de seleção na grade **associação da função de banco de dados** .  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>Para adicionar um usuário à função de banco de dados fixo replmonitor  
  
1.  No Distribuidor no banco de dados de distribuição, execute [sp_helpuser &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpuser-transact-sql). Se o usuário não estiver listado no `UserName` conjunto de resultados, o usuário deverá receber acesso ao banco de dados de distribuição usando a instrução [Create User &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql) .  
  
2.  No distribuidor no banco de dados de distribuição, execute [sp_helprolemember &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql), especificando um valor `replmonitor` de para **@rolename** o parâmetro. Se o usuário estiver listado no `MemberName` conjunto de resultados, o usuário já pertence a essa função.  
  
3.  Se o usuário não pertencer à `replmonitor` função, execute [Sp_addrolemember &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) no distribuidor no banco de dados de distribuição. Especifique um valor de `replmonitor` para **@rolename** e o nome do usuário do banco de dados [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ou o logon do Windows **@membername**que está sendo adicionado para.  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>Para remover um usuário da função de banco de dados fixo replmonitor  
  
1.  Para verificar se o usuário `replmonitor` pertence à função, execute [Sp_helprolemember &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql) no distribuidor no banco de dados de distribuição e especifique um valor de `replmonitor` para. **@rolename** Se o usuário não estiver listado em `MemberName` no conjunto de resultados, o usuário não pertence atualmente à essa função.  
  
2.  Se o usuário pertencer à `replmonitor` função, execute [Sp_droprolemember &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql) no distribuidor no banco de dados de distribuição. Especifique um valor de `replmonitor` para **@rolename** e o nome do usuário do banco de dados ou o logon do Windows **@membername**que está sendo removido para o.  
  
  
