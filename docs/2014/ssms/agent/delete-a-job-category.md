---
title: Excluir uma categoria de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- deleting job category
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- removing job category
ms.assetid: 47a7640b-20b3-4639-ab37-b6fc73575e6c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bb392991afbb3707fafdb18a28cc3de53f97c78
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783197"
---
# <a name="delete-a-job-category"></a>Excluir uma categoria de trabalho
  Este tópico descreve como excluir uma categoria de trabalho do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o SQL Server Management Objects.  
  
 As categorias de trabalho ajudam a organizar os trabalhos de modo a facilitar sua filtragem e agrupamento. Por exemplo, você pode organizar todos os seus trabalhos de backup de banco de dados na categoria Manutenção de Banco de Dados.  

##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
 Quando se exclui uma categoria de trabalho definida pelo usuário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent solicita que os trabalhos a ela atribuídos sejam reatribuídos a outra categoria. Você só pode excluir categorias de trabalho definidas pelo usuário.  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  

##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
  
### <a name="to-delete-a-job-category"></a>Para excluir uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja excluir uma categoria de trabalho.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse na pasta **Trabalhos** e selecione **Gerenciar Categorias de Trabalho**.  
  
4.  Na caixa de diálogo **Gerenciar Categorias de Trabalho**_server_name_ , selecione a categoria de trabalho a excluir.  
  
5.  Clique em **Excluir**.  
  
6.  Na caixa de diálogo **Categorias de Trabalho** , clique em **Sim**.  
  
7.  Feche a caixa de diálogo **Gerenciar Categorias de Trabalho**_server_name_ .  
  
##  <a name="TSQL"></a> Usando Transact-SQL  
  
### <a name="to-delete-a-job-category"></a>Para excluir uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    -- deletes the job category named AdminJobs.  
    USE msdb ;  
    GO   
    EXEC dbo.sp_delete_category  
        @name = N'AdminJobs',  
        @class = N'JOB' ;  
    GO  
    ```  
  
 Para obter mais informações, [consulte &#40;Transact-SQL&#41;sp_delete_category](/sql/relational-databases/system-stored-procedures/sp-delete-category-transact-sql).  

  
##  <a name="SMO"></a>Usando SQL Server Management Objects  

### <a name="to-delete-a-job-category"></a>Para excluir uma categoria de trabalho
  
 Chame a classe `JobCategory` usando uma linguagem de programação que você escolher, como Visual Basic, Visual C# ou PowerShell.  
