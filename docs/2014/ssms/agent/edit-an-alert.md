---
title: Editar um alerta | Microsoft Docs
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
- alerts [SQL Server], modifying
- modifying alerts
ms.assetid: f518e528-cc8f-446a-b37d-98505b86e430
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cfa24e0c8b806e35363767f5da012dfa87cd12ea
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37159747"
---
# <a name="edit-an-alert"></a>Edit an Alert
  Este tópico descreve como editar um alerta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para editar um alerta usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem editar as informações em um alerta. Deve ser concedida a outros usuários a função de banco de dados fixa **SQLAgentOperatorRole** no banco de dados **msdb** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-edit-an-alert"></a>Para editar um alerta  
  
1.  No **Pesquisador de Objetos** , clique no sinal de mais para expandir o servidor que contém o alerta que você deseja editar.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Alertas** .  
  
4.  Clique com o botão direito do mouse no alerta que deseja editar e selecione **Propriedades**.  
  
5.  Atualize as propriedades do alerta nas páginas **Geral**, **Resposta**e **Opções** .  
  
6.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-edit-an-alert"></a>Para editar um alerta  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- changes the enabled setting of Test Alert to 0  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_alert  
        @name = N'Test Alert',  
        @enabled = 0 ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_update_alert &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql).  
  
  
