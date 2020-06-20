---
title: Excluir um ou mais trabalhos | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, deleting
- dropping jobs
- jobs [SQL Server Agent], deleting
- deleting jobs
- removing jobs
ms.assetid: 67dcdad0-57b2-431c-b77f-4ffc926af93d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 436625f9ad629a6b0e574aa046059f4e7e9c2bf2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84995481"
---
# <a name="delete-one-or-more-jobs"></a>Excluir um ou mais trabalhos
  Este tópico descreve como excluir [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalhos do Agent no usando o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , o ou o [!INCLUDE[tsql](../../includes/tsql-md.md)] SQL Server Management Objects.  
  
 
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 A menos que seja membro da função de servidor fixa **sysadmin** , você só poderá excluir trabalhos de sua propriedade.  
  
 
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-job"></a>Para excluir um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja excluir e então clique em **Excluir**.  
  
3.  Na caixa de diálogo **Excluir Objeto** , verifique se o trabalho que você pretende excluir está selecionado.  
  
4.  Clique em **OK**.  
  
#### <a name="to-delete-multiple-jobs"></a>Para excluir vários trabalhos  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e a expanda.  
  
2.  Expanda o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse em **Monitor de Atividade do Trabalho**e clique em **Exibir Atividade do Trabalho**.  
  
4.  No Monitor de Atividade do Trabalho, selecione os trabalhos que deseja excluir, clique com o botão direito do mouse em sua seleção e escolha **Excluir trabalhos**.  
  

  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Usando o Transact-SQL  
  
#### <a name="to-delete-a-job"></a>Para excluir um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    USE msdb ;  
    GO  
  
    EXEC sp_delete_job  
        @job_name = N'NightlyBackups' ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_delete_job &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-delete-job-transact-sql).  

##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usando SQL Server Management Objects  

### <a name="to-delete-multiple-jobs"></a>Para excluir vários trabalhos
  
 Use a classe `JobCollection` usando uma linguagem de programação da sua escolha, como o Visual Basic, o Visual C# ou o PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](https://msdn.microsoft.com/library/ms162169.aspx).  
