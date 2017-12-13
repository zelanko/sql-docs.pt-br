---
title: "Tutorial: cadeias de propriedade e alternância de contexto | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
helpviewer_keywords:
- context switching [SQL Server], tutorials
- ownership chains [SQL Server]
ms.assetid: db5d4cc3-5fc5-4cf5-afc1-8d4edc1d512b
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a917fdde958f61b8cf6e218a39e8e2c463a726dd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="tutorial-ownership-chains-and-context-switching"></a>Tutorial: Ownership Chains and Context Switching
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tutorial usa um cenário para ilustrar os conceitos de segurança do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] envolvendo cadeias de propriedade e mudança de contexto de usuário.  
  
> [!NOTE]  
> Para executar o código nesse tutorial será necessário ter a segurança do Modo Misto configurada e o banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] instalado. Para obter mais informações sobre a segurança de Modo Misto, consulte [Escolher um modo de autenticação](../relational-databases/security/choose-an-authentication-mode.md).  
  
## <a name="scenario"></a>Cenário  
Neste cenário, dois usuários precisam de contas para acessar dados de ordem de compra armazenados no banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] . Os requisitos são os seguintes:  
  
-   A primeira conta (TestManagerUser) deve estar habilitada para que você veja todos os detalhes em cada ordem de compra.  
  
-   A segunda conta (TestEmployeeUser) deve estar habilitada para ver o número da ordem de compra, a data do pedido, a data de envio, os números de ID do produto e os itens solicitados e recebidos por ordem de compra, por número de ordem de compra, para itens cujos envios parciais foram recebidos.  
  
-   Todas as outras contas devem reter suas permissões atuais.  
  
Para atender aos requisitos deste cenário, o exemplo é dividido em quatro partes que demonstram os conceitos de cadeia de propriedade e alternância de contexto:  
  
1.  Configurando o ambiente.  
  
2.  Criando um procedimento armazenado para acessar dados por ordem de compra.  
  
3.  Acessando os dados pelo procedimento armazenado.  
  
4.  Redefinindo o ambiente.  
  
Cada bloco de código neste exemplo é explicado em linha. Para copiar o exemplo completo, consulte [Exemplo completo](#CompleteExample) no fim deste tutorial.  
  
## <a name="1-configure-the-environment"></a>1. Configure o ambiente  
Use o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e o código a seguir para abrir o banco de dados `AdventureWorks2012` e use a instrução [!INCLUDE[tsql](../includes/tsql-md.md)] `CURRENT_USER` para verificar se o usuário dbo é exibido como o contexto.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
```  
  
Para obter mais informações sobre a instrução CURRENT_USER, consulte [CURRENT_USER &#40;Transact-SQL&#41;](../t-sql/functions/current-user-transact-sql.md).  
  
Use esse código como o usuário dbo para criar dois usuários no servidor e no banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)].  
  
```  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
GO  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
```  
  
Para obter mais informações sobre a instrução CREATE USER, consulte [CREATE USER &#40;Transact-SQL&#41;](../t-sql/statements/create-user-transact-sql.md). Para obter mais informações sobre a instrução CREATE LOGIN, consulte [CREATE LOGIN &#40;Transact-SQL&#41;](../t-sql/statements/create-login-transact-sql.md).  
  
Use o código a seguir para alterar a propriedade do esquema `Purchasing` para a conta `TestManagerUser` . Isso permite que a conta use todos os acessos da instrução DML (Linguagem de Manipulação de Dados) (como as permissões `SELECT` e `INSERT` ) nos objetos que ela contém. `TestManagerUser` também tem a capacidade de criar procedimentos armazenados.  
  
```  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
```  
  
Para obter mais informações sobre a instrução GRANT, consulte [GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md). Para obter mais informações sobre procedimentos armazenados, consulte [Procedimentos armazenados &#40;Mecanismo de Banco de Dados&#41;](../relational-databases/stored-procedures/stored-procedures-database-engine.md). Para obter um cartaz de todas as permissões do [!INCLUDE[ssDE](../includes/ssde-md.md)], visite [http://go.microsoft.com/fwlink/?LinkId=229142](http://go.microsoft.com/fwlink/?LinkId=229142).  
  
## <a name="2-create-a-stored-procedure-to-access-data"></a>2. Crie um procedimento armazenado para acessar os dados  
Para alternar o contexto dentro de um banco de dados, use a instrução EXECUTE AS. EXECUTE AS exige permissões IMPERSONATE.  
  
Use a instrução `EXECUTE AS` no código a seguir para alterar o contexto para `TestManagerUser` e criar um procedimento armazenado exibindo somente os dados requeridos por `TestEmployeeUser`. Para atender a esses requisitos, o procedimento armazenado aceita uma variável como número da ordem de compra e não exibe informações financeiras, e a cláusula WHERE limita os resultados a envios parciais.  
  
```  
EXECUTE AS LOGIN = 'TestManagerUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader a  
      INNER JOIN Purchasing.PurchaseOrderDetail b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END  
GO  
```  
  
Atualmente `TestEmployeeUser` não tem acesso a qualquer objeto de banco de dados. O código a seguir (ainda no contexto `TestManagerUser` ) concede ao usuário da conta a capacidade de consultar informações na tabela base, pelo procedimento armazenado).  
  
```  
GRANT EXECUTE  
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO  
```  
  
O procedimento armazenado faz parte do esquema `Purchasing` , embora nenhum esquema tenha sido explicitamente especificado devido ao `TestManagerUser` ser atribuído por padrão ao esquema `Purchasing` . Você pode usar informações de catálogo de sistema para localizar objetos, como mostrado no código a seguir.  
  
```  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas a  
   INNER JOIN sys.objects b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
```  
  
Com essa seção de exemplo concluída, o código muda o contexto de volta ao dbo usando a instrução `REVERT`.  
  
```  
REVERT;  
GO  
```  
  
Para obter mais informações sobre a instrução REVERT, consulte [REVERT &#40;Transact-SQL&#41;](../t-sql/statements/revert-transact-sql.md).  
  
## <a name="3-access-data-through-the-stored-procedure"></a>3. Acesse dados pelo procedimento armazenado  
`TestEmployeeUser` não tem permissões nos objetos de banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] , a não ser um logon e os direitos atribuídos à função de banco de dados pública. O código a seguir retorna um erro quando `TestEmployeeUser` tentar acessar tabelas base.  
  
```  
EXECUTE AS LOGIN = 'TestEmployeeUser'  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* This won't work */  
SELECT *  
FROM Purchasing.PurchaseOrderHeader;  
GO  
SELECT *  
FROM Purchasing.PurchaseOrderDetail;  
GO  
```  
  
Como os objetos referenciados pelos procedimentos armazenados criados na última seção são de propriedade do `TestManagerUser` em virtude da propriedade de esquema `Purchasing` , `TestEmployeeUser` pode acessar as tabelas base pelo procedimento armazenado. O código a seguir, ainda usando o contexto `TestEmployeeUser` , passa a ordem de compra 952 como um parâmetro.  
  
```  
EXEC Purchasing.usp_ShowWaitingItems 952  
GO  
```  
  
## <a name="4-reset-the-environment"></a>4. Redefina o ambiente  
O código a seguir usa o comando `REVERT` para retornar o contexto da conta atual ao `dbo`e, em seguida, redefine o ambiente.  
  
```  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="CompleteExample"></a>Exemplo completo  
Esta seção exibe o código de exemplo completo.  
  
> [!NOTE]  
> Este código não inclui os dois erros previstos que demonstram a incapacidade de o `TestEmployeeUser` fazer a seleção a partir de tabelas base.  
  
```  
/*   
Script:       UserContextTutorial.sql  
Author:       Microsoft  
Last Updated: Books Online  
Conditions:   Execute as DBO or sysadmin in the AdventureWorks database  
Section 1:    Configure the Environment   
*/  
USE AdventureWorks2012;  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
/* Create server and database users */  
CREATE LOGIN TestManagerUser   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khx';  
  
GO  
  
CREATE USER TestManagerUser   
   FOR LOGIN TestManagerUser  
   WITH DEFAULT_SCHEMA = Purchasing;  
GO   
  
CREATE LOGIN TestEmployeeUser  
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
GO  
CREATE USER TestEmployeeUser   
   FOR LOGIN TestEmployeeUser;  
GO   
  
/* Change owner of the Purchasing Schema to TestManagerUser */  
ALTER AUTHORIZATION   
   ON SCHEMA::Purchasing   
   TO TestManagerUser;  
GO  
  
GRANT CREATE PROCEDURE   
   TO TestManagerUser   
   WITH GRANT OPTION;  
GO  
  
/*   
Section 2: Switch Context and Create Objects  
*/  
EXECUTE AS LOGIN = 'TestManagerUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
  
/* Note: The user that calls the EXECUTE AS statement must have IMPERSONATE permissions on the target principal */  
CREATE PROCEDURE usp_ShowWaitingItems @ProductID int  
AS  
BEGIN   
   SELECT a.PurchaseOrderID, a.OrderDate, a.ShipDate  
      , b.ProductID, b.OrderQty, b.ReceivedQty  
   FROM Purchasing.PurchaseOrderHeader AS a  
      INNER JOIN Purchasing.PurchaseOrderDetail AS b  
         ON a.PurchaseOrderID = b.PurchaseOrderID  
   WHERE b.OrderQty > b.ReceivedQty  
      AND @ProductID = b.ProductID  
   ORDER BY b.ProductID ASC  
END;  
GO  
  
/* Give the employee the ability to run the procedure */  
GRANT EXECUTE   
   ON OBJECT::Purchasing.usp_ShowWaitingItems  
   TO TestEmployeeUser;  
GO   
  
/* Notice that the stored procedure is located in the Purchasing   
schema. This also demonstrates system catalogs */  
SELECT a.name AS 'Schema'  
   , b.name AS 'Object Name'  
   , b.type AS 'Object Type'  
FROM sys.schemas AS a  
   INNER JOIN sys.objects AS b  
      ON a.schema_id = b.schema_id   
WHERE b.name = 'usp_ShowWaitingItems';  
GO  
  
/* Go back to being the dbo user */  
REVERT;  
GO  
  
/*  
Section 3: Switch Context and Observe Security   
*/  
EXECUTE AS LOGIN = 'TestEmployeeUser';  
GO  
SELECT CURRENT_USER AS 'Current User Name';  
GO  
EXEC Purchasing.usp_ShowWaitingItems 952;  
GO  
  
/*   
Section 4: Clean Up Example  
*/  
REVERT;  
GO  
ALTER AUTHORIZATION   
ON SCHEMA::Purchasing TO dbo;  
GO  
DROP PROCEDURE Purchasing.usp_ShowWaitingItems;  
GO  
DROP USER TestEmployeeUser;  
GO  
DROP USER TestManagerUser;  
GO  
DROP LOGIN TestEmployeeUser;  
GO  
DROP LOGIN TestManagerUser;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
[Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
  
