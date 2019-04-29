---
title: Criar uma categoria de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
ms.assetid: e24a6d38-d231-4f64-ab89-2d1ef6f5792c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d904f82c793acf6135f600e1ed5392bda96e1bb8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856119"
---
# <a name="create-a-job-category"></a>Criar uma categoria de trabalho
  Este tópico descreve como criar uma categoria de trabalho no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)] ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent fornece categorias de trabalho internas às quais é possível atribuir trabalhos, mas você também pode criar uma categoria e atribuir-lhe trabalhos. As categorias de trabalho ajudam a organizar os trabalhos de modo a facilitar sua filtragem e agrupamento. Por exemplo, você pode organizar todos os seus trabalhos de backup de banco de dados na categoria Manutenção de Banco de Dados. Você também pode criar suas próprias categorias de trabalho.  
  
 
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 As categorias multisservidor só existem em um servidor mestre. Há apenas uma categoria de trabalho padrão disponível em um servidor mestre: [**Não Categorizado (Multisservidor)**]. Quando um trabalho multisservidor é baixado, sua categoria é alterada para **Trabalhos do MSX** no servidor de destino.  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  

  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-job-category"></a>Para criar uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja criar uma categoria de trabalho.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse na pasta **Trabalhos** e selecione **Gerenciar Categorias de Trabalho**.  
  
4.  Na caixa de diálogo **Gerenciar Categorias de Trabalho**_server_name_ , clique em **Adicionar**.  
  
5.  Na nova caixa de diálogo, na caixa **Nome** , insira um nome para a nova categoria de trabalho.  
  
6.  Marque a caixa de seleção **Mostrar todos os trabalhos** . Selecione um ou mais trabalhos para a nova categorias, marcando as caixas correspondentes a eles.  
  
7.  Clique em **OK**.  
  
8.  Na caixa de diálogo **Gerenciar Categorias de Trabalho**_server_name_ , clique em **Atualizar** para garantir que a nova categoria de trabalho esteja ativa. Se tudo estiver como esperado, feche a caixa de diálogo.  
  
 Para obter mais informações sobre essas caixas de diálogo, consulte [categorias de trabalho: Gerenciar categorias de trabalho](job-categories-manage-job-categories.md) e [propriedades de categorias e a nova categoria de trabalho do trabalho](job-categories-properties-new-job-category.md).  
  
 
  
##  <a name="TSQL"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-job-category"></a>Para criar uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- creates a local job category named AdminJobs   
    USE msdb ;  
    GO  
    EXEC dbo.sp_add_category  
        @class=N'JOB',  
        @type=N'LOCAL',  
        @name=N'AdminJobs' ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_add_category &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-category-transact-sql).  
  

  
##  <a name="SMO"></a> Usando o SQL Server Management Objects  
 **Para criar uma categoria de trabalho**  
  
 Chame a classe `JobCategory` usando uma linguagem de programação que você escolher, como Visual Basic, Visual C# ou PowerShell. Para obter um código de exemplo, consulte [Agendamento de tarefas administrativas automáticas no SQL Server Agent](sql-server-agent.md).  
  
 
  
  
