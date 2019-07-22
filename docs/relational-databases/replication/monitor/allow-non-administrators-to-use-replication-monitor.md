---
title: Permitir que não administradores usem o Replication Monitor, | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cad7341143ec6392ef4163f477b1d15144d932a5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018573"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>Permitir que não administradores usem o Replication Monitor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
 Para permitir que não administradores usem o Replication Monitor, um membro da função de servidor fixa **sysadmin** deve adicionar o usuário ao banco de dados de distribuição e atribuir-lhe a função **replmonitor** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>Para permitir que não administradores usem o Replication Monitor  
  
1.  No [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conecte-se ao Distribuidor e, em seguida, expanda o nó do servidor.  
  
2.  Expanda **Bancos de Dados**, expanda **Bancos de Dados do Sistema**e, em seguida, expanda o banco de dados de distribuição (nomeado **distribuição** por padrão).  
  
3.  Expanda **Segurança**, clique com o botão direito do mouse em **Usuários**e, em seguida, clique em **Novo Usuário**.  
  
4.  Digite um nome de usuário e logon para o usuário.  
  
5.  Selecione um esquema padrão de **replmonitor**.  
  
6.  Marque a caixa de seleção **replmonitor** na grade **Associação à função de banco de dados** .  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

[!INCLUDE[freshInclude](../../../includes/paragraph-content/fresh-note-steps-feedback.md)]

##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>Para adicionar um usuário à função de banco de dados fixo replmonitor  
  
1.  No Distribuidor no banco de dados de distribuição, execute [sp_helpuser &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md). Se o usuário não estiver listado em **UserName** no conjunto de resultados, esse usuário deverá receber acesso ao banco de dados de distribuição usando a instrução [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md).  
  
2.  No Distribuidor no banco de dados de distribuição, execute [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md), especificando um valor de **replmonitor** para o parâmetro **@rolename** . Se o usuário estiver listado em **MemberName** no conjunto de resultados, o usuário já pertence a essa função.  
  
3.  Se o usuário não pertencer à função **replmonitor**, execute [sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) no distribuidor no banco de dados de distribuição. Especifique um valor de **replmonitor** para **@rolename** e o nome do banco de dados do usuário ou o logon do Windows [!INCLUDE[msCoName](../../../includes/msconame-md.md)] sendo adicionado para o **@membername** .  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>Para remover um usuário da função de banco de dados fixo replmonitor  
  
1.  Para verificar se o usuário pertence à função **replmonitor**, execute [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) no Distribuidor no banco de dados de distribuição e especifique um valor de **replmonitor** para **@rolename** . Se o usuário não estiver listado em **MemberName** no conjunto de resultados, o usuário não pertence atualmente à essa função.  
  
2.  Se o usuário pertencer à função **replmonitor**, execute [sp_droprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) no Distribuidor no banco de dados de distribuição. Especifique um valor de **replmonitor** para **@rolename** e o nome do banco de dados do usuário ou o logon do Windows sendo removido para o **@membername** .  
  
  
