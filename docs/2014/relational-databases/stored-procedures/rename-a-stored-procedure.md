---
title: Renomear um procedimento armazenado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], renaming
- renaming stored procedures
ms.assetid: 5d2e4c68-7e0b-4405-8919-f5b203e46770
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b85a6a5e79c004eb3ed2c7c40c6e3b62d526e95a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721008"
---
# <a name="rename-a-stored-procedure"></a>Renomear um procedimento armazenado
  Este tópico descreve como renomear um procedimento armazenado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para renomear um procedimento armazenado, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Os nomes de procedimento devem estar de acordo com as regras para [identificadores](../databases/database-identifiers.md).  
  
-   Renomear uma procedimento armazenado não alterará o nome do objeto correspondente na coluna de definição da exibição de catálogo **sys.sql_modules** . Assim, é recomendável não renomear esse tipo de objeto. Em vez disso, remova-o e recrie o procedimento armazenado com seu nome novo.  
  
-   A alteração do nome ou definição de um procedimento pode causar falha em objetos dependentes que não são atualizados para refletir as alterações que tenham sido feitas no procedimento. Para obter mais informações, consulte [exibir as dependências de um procedimento armazenado](view-the-dependencies-of-a-stored-procedure.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 CREATE PROCEDURE  
 Exige a permissão CREATE PROCEDURE no banco de dados e a permissão ALTER no esquema em que o procedimento está sendo criado, ou exige a associação na função de banco de dados fixa **db_ddladmin** .  
  
 ALTER PROCEDURE  
 Requer a permissão ALTER no procedimento, ou requer a associação na função de banco de dados fixa **db_ddladmin**.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-rename-a-stored-procedure"></a>Para renomear um procedimento armazenado  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados ao qual pertence o procedimento e expanda **Programação**.  
  
3.  [Determine as dependências do procedimento armazenado](view-the-dependencies-of-a-stored-procedure.md).  
  
4.  Expanda **Procedimentos Armazenados**, clique com o botão direito do mouse no procedimento a ser renomeado e clique em **Renomear**.  
  
5.  Modifique o nome do procedimento.  
  
6.  Modifique o nome do procedimento referenciado em qualquer objeto dependente ou script.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-rename-a-stored-procedure"></a>Para renomear um procedimento armazenado  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como renomear um procedimento removendo-o e recriando-o com um novo nome. O primeiro exemplo cria o procedimento armazenado `'HumanResources.uspGetAllEmployeesTest`. O segundo exemplo renomeia o procedimento armazenado para `HumanResources.uspEveryEmployeeTest`.  
  
```sql  
--Create the stored procedure.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'HumanResources.uspGetAllEmployeesTest', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetAllEmployeesTest;  
GO  
CREATE PROCEDURE HumanResources.uspGetAllEmployeesTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
  
--Rename the stored procedure.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'HumanResources.uspGetAllEmployeesTest', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetAllEmployeesTest;  
GO  
CREATE PROCEDURE HumanResources.uspEveryEmployeeTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-procedure-transact-sql)   
 [CRIAR procedimento &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-procedure-transact-sql)   
 [Criar um procedimento armazenado](../stored-procedures/create-a-stored-procedure.md)   
 [Modificar um procedimento armazenado](../stored-procedures/modify-a-stored-procedure.md)   
 [Excluir um procedimento armazenado](../stored-procedures/delete-a-stored-procedure.md)   
 [Exibir a definição de um procedimento armazenado](view-the-definition-of-a-stored-procedure.md)   
 [Exibir as dependências de um procedimento armazenado](view-the-dependencies-of-a-stored-procedure.md)  
  
  
