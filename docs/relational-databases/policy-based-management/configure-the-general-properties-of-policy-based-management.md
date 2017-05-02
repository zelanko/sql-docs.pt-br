---
title: "Configurar as propriedades gerais do gerenciamento baseado em políticas | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dmf.PolicyManagement.f1
helpviewer_keywords:
- Policy-Based Management, configure properties
ms.assetid: 6d1e0e37-29ea-408a-a055-384984d884be
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 7f7103ab22a01f6dcb60c31d7ad7fdcc503746db
ms.lasthandoff: 04/11/2017

---
# <a name="configure-the-general-properties-of-policy-based-management"></a>Configurar as propriedades gerais do gerenciamento baseado em políticas
  Este tópico descreve como configurar as propriedades para o Gerenciamento Baseado em Políticas no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para configurar o Gerenciamento Baseado em Políticas usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a associação à função de banco de dados fixa PolicyAdministratorRole.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-policy-based-management"></a>Para configurar o Gerenciamento Baseado em Políticas  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja configurar as propriedades do Gerenciamento Baseado em Políticas.  
  
2.  Clique no sinal de adição para expandir a pasta **Gerenciamento** .  
  
3.  Clique com o botão direito do mouse em **Gerenciamento de Política** e selecione **Propriedades**.  
  
     As opções a seguir estão disponíveis na caixa de diálogo **Propriedades de Gerenciamento de Política** .  
  
     **Habilitado**  
     Especifica se o Gerenciamento Baseado em Políticas está habilitado.  
  
     **HistoryRetentionInDays**  
     Especifica o número de dias que o histórico de avaliação de política deve ser mantido. Se esse valor for 0 (o padrão), o histórico não será removido automaticamente.  
  
     **LogOnSuccess**  
     Especifica se o Gerenciamento Baseado em Políticas registra em log avaliações de política com êxito.  
  
    -   Quando esse valor é false (o padrão), somente são registradas em log as avaliações de política com falha.  
  
    -   Quando esse valor é verdadeiro, as avaliações de política bem-sucedidas e com falha são registradas em log.  
  
4.  Quando terminar, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-configure-policy-based-management"></a>Para configurar o Gerenciamento Baseado em Políticas  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- enables Policy-Based Management   
    USE msdb;  
    GO  
    EXEC dbo.sp_syspolicy_configure   
         @name = N'Enabled',   
         @value = 1;  
    GO  
    ```  
  
 Para obter mais informações, veja [sp_syspolicy_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql.md).  
  
  
