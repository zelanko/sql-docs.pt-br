---
title: Excluir exibições | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a0b11b2d6fa897b99276f75fb74e2c41e25db904
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68123469"
---
# <a name="delete-views"></a>Excluir exibições
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-all-md.md)]
  Você pode excluir (remover) exibições no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para excluir uma exibição de um banco de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Quando você descarta uma exibição, a definição da exibição e outras informações sobre ela são excluídas do catálogo do sistema. Todas as permissões para a exibição também são excluídas.  
  
-   Qualquer exibição em uma tabela descartada pelo uso de `DROP TABLE` deve ser descartada explicitamente usando `DROP VIEW`.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na permissão SCHEMA ou CONTROL em OBJECT.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-view-from-a-database"></a>Para excluir uma exibição de um banco de dados  
  
1.  No **Pesquisador de Objetos**, expanda o banco de dados que contém a exibição que deseja excluir e expanda a pasta **Exibições** .  
  
2.  Clique com o botão direito do mouse na exibição que você deseja excluir e clique em **Excluir**.  
  
3.  Na caixa de diálogo **Excluir Objeto** , clique em **OK**.  
  
    > [!IMPORTANT]  
    >  Clique em **Mostrar Dependências** na caixa de diálogo **Excluir Objeto** para abrir a caixa de diálogo _view\_name_**Dependências**. Isso mostrará todos os objetos que dependem da exibição e todos os objetos dos quais a exibição depende.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
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
  
 Para obter mais informações, veja [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md).  
  
  
