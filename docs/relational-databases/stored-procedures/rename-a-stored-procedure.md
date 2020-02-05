---
title: Renomear um procedimento armazenado | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], renaming
- renaming stored procedures
ms.assetid: 5d2e4c68-7e0b-4405-8919-f5b203e46770
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 177886f6b43e90a094ae69945a1deee7adcab61d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68136688"
---
# <a name="rename-a-stored-procedure"></a>Renomear um procedimento armazenado
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
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
  
-   Os nomes de procedimento devem estar de acordo com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
-   Renomear um procedimento armazenado mantém o `object_id` e todas as permissões que forem especificamente atribuídas ao procedimento. Descartar e recriar o objeto cria um novo `object_id` e remove quaisquer permissões atribuídas especificamente ao procedimento.

-   Renomear um procedimento armazenado não altera o nome do objeto correspondente na coluna de definição da exibição de catálogo **sys.sql_modules** . Para fazer isso, remova-o e recrie o procedimento armazenado com seu nome novo.  

-   A alteração do nome ou definição de um procedimento pode causar falha em objetos dependentes que não são atualizados para refletir as alterações que tenham sido feitas no procedimento. Para obter mais informações, veja [Exibir as dependências de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 CREATE PROCEDURE  
 Exige a permissão CREATE PROCEDURE no banco de dados e a permissão ALTER no esquema em que o procedimento está sendo criado, ou exige a associação na função de banco de dados fixa **db_ddladmin** .  
  
 ALTER PROCEDURE  
 Exige a permissão ALTER no procedimento, ou exige a associação na função de banco de dados fixa **db_ddladmin** .  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-rename-a-stored-procedure"></a>Para renomear um procedimento armazenado  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
2.  Expanda **Bancos de Dados**, expanda o banco de dados ao qual pertence o procedimento e expanda **Programação**.  
3.  [Determinar as dependências do procedimento armazenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
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

CREATE PROCEDURE HumanResources.uspGetAllEmployeesTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
  
--Rename the stored procedure.  
EXEC sp_rename 'HumanResources.uspGetAllEmployeesTest', 'uspEveryEmployeeTest'; 
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [Criar um procedimento armazenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Modificar um procedimento armazenado](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [Excluir um procedimento armazenado](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)   
 [Exibir a definição de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [Exibir as dependências de um procedimento armazenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
  
