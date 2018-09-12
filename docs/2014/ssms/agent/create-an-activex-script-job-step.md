---
title: Criar uma etapa de trabalho de script do ActiveX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ActiveX scripting jobs [SQL Server]
- job steps [Analysis Services]
ms.assetid: e6c46c6b-2d61-4571-bc8e-a831cd6e6302
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d502d81e5edddb8c47ffc3a9bcdf742aa84a59da
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43820832"
---
# <a name="create-an-activex-script-job-step"></a>Create an ActiveX Script Job Step
  Este tópico descreve como criar e definir uma etapa de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que execute um script ActiveX usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o SQL Server Management Objects.  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar uma etapa de trabalho Transact-SQL usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
## <a name="before-you-begin"></a>Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-an-activex-script-job-step"></a>Para criar uma etapa de trabalho de Script ActiveX  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e a expanda.  
  
2.  Expanda **SQL Server Agent**, crie um novo trabalho ou clique com o botão direito do mouse em um trabalho existente e clique em **Propriedades**. Para obter mais informações sobre como criar um trabalho, consulte [Criando trabalhos](create-jobs.md).  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , clique na página **Etapas** e, em seguida, em **Nova**.  
  
4.  Na caixa de diálogo **Nova Etapa de Trabalho** , digite o **Nome da etapa**de trabalho.  
  
5.  Na lista **Tipo** , clique em **Script ActiveX**.  
  
6.  Na lista **Executar como** , selecione a conta proxy com as credenciais que o trabalho usará.  
  
7.  Selecione o **Idioma** no qual o script foi escrito. Como alternativa, clique em **Outro** e insira o nome da linguagem de script [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX em que o script foi escrito.  
  
8.  Na caixa **Comando** , insira a sintaxe de script que será executada para a etapa de trabalho. Como alternativa, clique em **Abrir** e selecione um arquivo que contenha a sintaxe de script.  
  
9. Clique na página **Avançado** para definir as seguintes opções de etapa de trabalho: a ação a tomar em caso de êxito ou falha da etapa, quantas vezes o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve tentar executar a etapa e com que frequência.  
  
##  <a name="TSQL"></a> Usando o Transact-SQL  
  
#### <a name="to-create-an-activex-script-job-step"></a>Para criar uma etapa de trabalho de Script ActiveX  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
  
              -- create an ActiveX Script job step written in VBScript that creates a restore point  
    USE msdb;  
    GO  
    EXEC sp_add_jobstep  
        @job_name = N'Weekly Sales Data Backup',  
        @step_name = N'Create a restore point',  
        @subsystem = N'ACTIVESCRIPTING',  
        @command = N'Const RESTORE_POINT = 20  
  
    strComputer = "."  
    Set objWMIService = GetObject("winmgmts:" _  
        & "{impersonationLevel=impersonate}!\\" & strComputer & "\root\default")  
  
    Set objItem = objWMIService.Get("SystemRestore")  
    errResults = objItem.Restore(RESTORE_POINT)',   
        @retry_attempts = 5,  
        @retry_interval = 5 ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_add_jobstep &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql).  
  
##  <a name="SMO"></a> Usando o SQL Server Management Objects  
 **Para criar uma etapa de trabalho de Script ActiveX**  
  
 Use o `JobStep` classe usando uma linguagem de programação que você escolher, como Visual Basic, Visual c# ou PowerShell.  
  
  
