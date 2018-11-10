---
title: Criar um procedimento armazenado | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: quickstart
helpviewer_keywords:
- new stored procedures
- stored procedures [SQL Server], creating
- creating stored procedures
ms.assetid: 76e8a6ba-1381-4620-b356-4311e1331ca7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2add7097a4cead6a03d2aa3f0b6e14b9cc0bdce5
ms.sourcegitcommit: b58d514879f182fac74d9819918188f1688889f3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50970368"
---
# <a name="create-a-stored-procedure"></a>Criar um procedimento armazenado
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

> [!div class="nextstepaction"]
> [Ajude a aprimorar os documentos do SQL Server!](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

Este tópico descreve como criar um procedimento armazenado [!INCLUDE[tsql](../../includes/tsql-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e a declaração [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE PROCEDURE.  
  
##  <a name="Top"></a>   
-   **Antes de começar:**  [Permissões](#Permissions)  
  
-   **To create a procedure, using:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="Permissions"></a> Permissões  
 Requer a permissão CREATE PROCEDURE no banco de dados e a permissão ALTER no esquema no qual o procedimento está sendo criado.  
  
##  <a name="Procedures"></a> Como criar um procedimento armazenado  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para criar um procedimento no Pesquisador de Objetos**  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados do [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e, em seguida, expanda **Programação**.  
  
3.  Clique com o botão direito do mouse em **Procedimentos Armazenados**e clique em **Novo Procedimento Armazenado**.  
  
4.  No menu **Consulta** , clique em **Especificar Valores para Parâmetros de Modelo**.  
  
5.  Na caixa de diálogo **Especificar Valores para Parâmetros de Modelo** , digite os seguintes valores para os parâmetros mostrados.  
  
    |Parâmetro|Valor|  
    |---------------|-----------|  
    |Autor|*Seu nome*|  
    |Data de criação|*A data de hoje*|  
    |Descrição|Retorna dados de funcionário.|  
    |Procedure_name|HumanResources.uspGetEmployeesTest|  
    |@Param1|@LastName|  
    |@Datatype_For_Param1|**nvarchar**(50)|  
    |Default_Value_For_Param1|NULL|  
    |@Param2|@FirstName|  
    |@Datatype_For_Param2|**nvarchar**(50)|  
    |Default_Value_For_Param2|NULL|  
  
6.  Clique em **OK**.  
  
7.  No **Editor de Consultas**, substitua a instrução SELECT pela seguinte instrução:  
  
    ```sql  
    SELECT FirstName, LastName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory  
    WHERE FirstName = @FirstName AND LastName = @LastName  
        AND EndDate IS NULL;  
    ```  
  
8.  Para testar a sintaxe, no menu **Consulta** , clique em **Analisar**. Se uma mensagem de erro for retornada, compare as instruções com as informações acima e corrija conforme necessário.  
  
9. Para criar o procedimento, no menu **Consulta** , clique em **Executar**. O procedimento é criado como um objeto no banco de dados.  
  
10. Para ver o procedimento listado no Pesquisador de Objetos, clique com o botão direito do mouse em **Procedimentos Armazenados** e selecione **Atualizar**.  
  
11. Para executar o procedimento, no Pesquisador de Objetos, clique com o botão direito do mouse no nome do procedimento armazenado **HumanResources.uspGetEmployeesTest** e selecione **Executar Procedimento Armazenado**.  
  
12. Na janela **Executar Procedimento**, insira Margheim como o valor para o parâmetro @LastName e insira o valor Diane como o valor para o parâmetro @FirstName.  
  
> [!WARNING]  
>  Valide todas as entradas de usuário. Não concatene a entrada de usuário antes de validá-la. Nunca execute um comando construído por uma entrada de usuário inválida.  
  
###  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para criar um procedimento no Editor de Consultas**  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  No menu **Arquivo** , clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo cria o mesmo procedimento armazenado descrito acima usando um nome de procedimento diferente.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE PROCEDURE HumanResources.uspGetEmployeesTest2   
        @LastName nvarchar(50),   
        @FirstName nvarchar(50)   
    AS   
  
        SET NOCOUNT ON;  
        SELECT FirstName, LastName, Department  
        FROM HumanResources.vEmployeeDepartmentHistory  
        WHERE FirstName = @FirstName AND LastName = @LastName  
        AND EndDate IS NULL;  
    GO  
  
    ```  
  
4.  Para executar o procedimento, copie e cole o exemplo a seguir em uma nova janela de consulta e clique em **Executar**. Observe que métodos diferentes de especificar os valores de parâmetros são mostrados.  
  
    ```  
    EXECUTE HumanResources.uspGetEmployeesTest2 N'Ackerman', N'Pilar';  
    -- Or  
    EXEC HumanResources.uspGetEmployeesTest2 @LastName = N'Ackerman', @FirstName = N'Pilar';  
    GO  
    -- Or  
    EXECUTE HumanResources.uspGetEmployeesTest2 @FirstName = N'Pilar', @LastName = N'Ackerman';  
    GO  
  
    ```  
  
##  <a name="PowerShellProcedure"></a>   
## <a name="see-also"></a>Consulte Também  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)  
  
  
