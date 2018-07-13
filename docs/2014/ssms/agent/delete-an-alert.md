---
title: Excluir um alerta | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], deleting
- deleting alerts
- canceling alerts
- dropping alerts
- disabling alerts
- removing alerts
ms.assetid: c982b208-e2d1-4d34-8cee-940b9baf6586
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d9f8f3c8ff9a6c6cb12c99adce98c784cda148b0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230086"
---
# <a name="delete-an-alert"></a>Delete an Alert
  Este tópico descreve como excluir alertas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para excluir um alerta, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 A remoção de um alerta também remove qualquer notificação associada a ele.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Por padrão, somente membros da função de servidor fixa **sysadmin** podem excluir alertas.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-an-alert"></a>Para excluir um alerta  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor que contém o alerta do SQL Server Agent que você deseja excluir.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Alertas** .  
  
4.  Clique com o botão direito do mouse no alerta a ser excluído e selecione **Excluir**.  
  
5.  Na caixa de diálogo **Excluir Objeto** , confirme se o alerta correto está selecionado e clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-delete-an-alert"></a>Para excluir um alerta  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- deletes the SQL Server Agent alert called 'Test Alert.'  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_delete_alert  
       @name = N'Test Alert' ;  
    GO  
    ```  
  
 Para obter mais informações, consulte s[sp_delete_alert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-delete-alert-transact-sql).  
  
  
