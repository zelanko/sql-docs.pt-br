---
title: Excluir exibições | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- dropping views
- deleting views
- views [SQL Server], deleting
- removing views
ms.assetid: 6823c7f8-06ca-4bda-8482-7092f03d52a0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9e52ab35b0f75f80a6117995a353b66c320a5294
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48085578"
---
# <a name="delete-views"></a>Excluir exibições
  Você pode excluir (remover) exibições no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  

  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Quando você descarta uma exibição, a definição da exibição e outras informações sobre ela são excluídas do catálogo do sistema. Todas as permissões para a exibição também são excluídas.  
  
-   Qualquer exibição em uma tabela descartada pelo uso de `DROP TABLE` deve ser descartada explicitamente usando `DROP VIEW`.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na permissão SCHEMA ou CONTROL em OBJECT.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-view-from-a-database"></a>Para excluir uma exibição de um banco de dados  
  
1.  No **Pesquisador de Objetos**, expanda o banco de dados que contém a exibição que deseja excluir e expanda a pasta **Exibições** .  
  
2.  Clique com o botão direito do mouse na exibição que você deseja excluir e clique em **Excluir**.  
  
3.  Na caixa de diálogo **Excluir Objeto** , clique em **OK**.  
  
    > [!IMPORTANT]  
    >  Clique em **Mostrar Dependências** na caixa de diálogo **Excluir Objeto** para abrir a caixa de diálogo *nome_da_exibição***Dependências*. Isso mostrará todos os objetos que dependem da exibição e todos os objetos dos quais a exibição depende.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-delete-a-view-from-a-database"></a>Para excluir uma exibição de um banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo excluirá a exibição especificada somente se a exibição já existir.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    IF OBJECT_ID ('HumanResources.EmployeeHireDate', 'V') IS NOT NULL  
    DROP VIEW HumanResources.EmployeeHireDate;  
    GO  
    ```  
  
 Para obter mais informações, veja [DROP VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql).  
  
  
