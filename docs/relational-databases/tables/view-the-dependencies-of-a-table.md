---
title: "Exibir as dependências de uma tabela | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- table dependencies [SQL Server]
- dependencies [SQL Server], tables
- displaying dependences
- viewing dependencies
ms.assetid: c4351ef5-e7d0-46e7-8367-88695e9974f8
caps.latest.revision: 24
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8359eccee9aeda470c962793d13c85819ef9fe49
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="view-the-dependencies-of-a-table"></a>Exibir as dependências de uma tabela
[!INCLUDE[tsql-appliesto-ss2016-all_md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Você pode exibir as dependências de uma tabela no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir as dependências de uma tabela usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Requer permissão VIEW DEFINITION no banco de dados e permissão SELECT em sys.sql_expression_dependencies para o banco de dados. Por padrão, a permissão SELECT é concedida somente a membros da função de banco de dados fixa db_owner. Quando são concedidas permissões SELECT e VIEW DEFINITION a outro usuário, o usuário autorizado pode exibir todas as dependências no banco de dados.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-dependencies-of-a-table"></a>Para visualizar as dependências de uma tabela  
  
1.  No **Pesquisador de Objetos**, expanda **Bancos de Dados**, expanda um banco de dados e, em seguida, expanda **Tabelas**.  
  
2.  Clique com o botão direito do mouse em uma tabela e clique em **Exibir Dependências**.  
  
3.  Na caixa de diálogo **Dependências do Objeto***\<object name>*, selecione **Objetos que dependem do**  *\<<nome do objeto>* ou **Objetos dos quais o** *\<object name>***depende**.  
  
4.  Selecione um objeto na grade **Dependências** . O tipo de objeto (como “Gatilho” ou “Procedimento Armazenado”) aparece na caixa **Tipo** .  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-view-the-objects-that-depend-on-a-table"></a>Para exibir os objetos que dependem de uma tabela  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT * FROM sys.sql_expression_dependencies  
    WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');   
    GO  
  
    ```  
  
#### <a name="to-view-the-objects-on-which-a-table-depends"></a>Para exibir os objetos dos quais uma tabela depende  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  O exemplo a seguir retorna os objetos que dependem da tabela `Production.Product`. Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT * FROM sys.sql_expression_dependencies  
    WHERE referenced_id = OBJECT_ID(N'Production.Product');   
    GO  
  
    ```  
  
 Para obter mais informações, veja [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)  
  
  

