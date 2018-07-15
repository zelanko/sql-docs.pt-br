---
title: Alterar etapas de um trabalho mestre do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8f1a0ee6-49ff-4080-94ca-d661daeff2a6
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 243f5f15535a785e544c6b4e081d3404fb7ad26c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187613"
---
# <a name="change-steps-of-a-sql-server-agent-master-job"></a>Change Steps of a SQL Server Agent Master Job
  Este tópico descreve como realizar alterações às etapas de um trabalho mestre do SQL Server Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para realizar alterações às etapas de um trabalho mestre do SQL Server Agent, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 Um trabalho mestre do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não pode ser destino em ambos os servidores, local e remoto.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 A menos que seja membro da função de servidor fixa **sysadmin** , você poderá modificar somente trabalhos de sua propriedade. Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-make-changes-to-the-steps-of-a-sql-server-agent-master-job"></a>Para realizar alterações às etapas de um trabalho mestre do SQL Server Agent  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor que contém o trabalho onde você deseja modificar etapas.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Trabalhos** .  
  
4.  Clique com o botão direito do mouse no trabalho no qual você deseja modificar etapas e selecione **Propriedades**.  
  
5.  Na caixa de diálogo **Propriedades do Trabalho –***job_name*, em **Selecione uma página**, selecione **Etapas**.  
  
6.  Clique em **Editar** para abrir a caixa de diálogo **Propriedades da Etapa de Trabalho –***job_step_name*. Para obter mais informações sobre as opções disponíveis nessa caixa de diálogo, consulte [propriedades da etapa de trabalho: nova etapa de trabalho &#40;página geral&#41; ](../../integration-services/general-page-of-integration-services-designers-options.md) e [propriedades da etapa de trabalho: nova etapa de trabalho &#40;página avançada&#41; ](job-step-properties-new-job-step-advanced-page.md).  
  
7.  Quando terminar, clique em **OK**.  
  
8.  Na caixa de diálogo **Propriedades do Trabalho –***job_name*, clique em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-make-changes-to-the-steps-of-a-sql-server-agent-master-job"></a>Para realizar alterações às etapas de um trabalho mestre do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- changes the number of retry attempts for the first step of the Weekly Sales Data Backup job.   
    -- After running this example, the number of retry attempts is 10   
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_id = 1,  
        @retry_attempts = 10 ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_update_jobstep &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql).  
  
  
