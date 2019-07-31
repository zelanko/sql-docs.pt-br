---
title: 'Tutorial: Assinando procedimentos armazenados com um certificado | Microsoft Docs'
ms.custom: ''
ms.date: 08/23/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: quickstart
helpviewer_keywords:
- signing stored procedures tutorial [SQL Server]
ms.assetid: a4b0f23b-bdc8-425f-b0b9-e0621894f47e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 225f827de70f4946cabca3e06e7a7be364094479
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138378"
---
# <a name="tutorial-signing-stored-procedures-with-a-certificate"></a>Tutorial: Assinando procedimentos armazenados com um certificado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Este tutorial ilustra como assinar procedimentos armazenados usando um certificado gerado pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
> Para executar o código nesse tutorial será necessário ter a segurança do Modo Misto configurada e o banco de dados AdventureWorks2017 instalado.   
  
A assinatura de procedimentos armazenados usando um certificado é útil quando você quer solicitar permissões sobre procedimentos armazenados, mas não quer conceder esses direitos explicitamente a um usuário. Embora essas tarefas possam ser realizadas de outras formas como, por exemplo, usando a instrução EXECUTE AS, o uso de um certificado permite que você utilize um rastreamento para localizar o chamador original do procedimento armazenado. Isso fornece um alto nível de auditoria, principalmente durante operações de segurança ou DDL (Linguagem de Definição de Dados).  
  
Você pode criar um certificado no banco de dados mestre para conceder permissões em nível de servidor ou criar um certificado em banco de dados de usuário para conceder permissões em nível de banco de dados. Nesse cenário, um usuário sem direitos a tabelas base deve acessar um procedimento armazenado no banco de dados AdventureWorks2017 e você deverá auditar a trilha de acesso ao objeto. Em vez de usar outros métodos de cadeia de propriedade, você criará uma conta de usuário de servidor e de banco de dados sem direitos aos objetos base e uma conta de usuário de banco de dados com direitos a uma tabela e a procedimentos armazenados. O procedimento armazenado e a segunda conta de usuário de banco de dados serão protegidos com um certificado. A segunda conta de banco de dados terá acesso a todos os objetos e concederá acesso aos procedimentos armazenados à primeira conta de usuário do banco de dados.  
  
Nesse cenário, primeiramente você criará um certificado de banco de dados, um procedimento armazenado e um usuário e, depois, testará o processo seguindo estas etapas:  
  
Cada bloco de código neste exemplo é explicado em linha. Para copiar o exemplo completo, consulte [Exemplo completo](#CompleteExample) no fim deste tutorial.  

## <a name="prerequisites"></a>Prerequisites
Para concluir este tutorial, você precisará do SQL Server Management Studio, bem como acesso a um servidor que executa o SQL Server e um banco de dados do AdventureWorks.

- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Baixe o [Bancos de dados de exemplo do AdventureWorks2017](https://docs.microsoft.com/sql/samples/adventureworks-install-configure).

Para obter instruções sobre como restaurar um banco de dados no SQL Server Management Studio, veja [Restaurar um banco de dados](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).   
  
## <a name="1-configure-the-environment"></a>1. Configure o ambiente  
Para configurar o contexto inicial do exemplo, no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] abra uma nova consulta e execute o código a seguir para abrir o banco de dados AdventureWorks2017. Esse código altera o contexto do banco de dados para `AdventureWorks2012` e cria um novo logon de servidor e conta de usuário de banco de dados (`TestCreditRatingUser`), usando uma senha.  
  
```sql  
USE AdventureWorks2017;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
```  
  
Para obter mais informações sobre a instrução CREATE USER, consulte [CREATE USER &#40;Transact-SQL&#41;](../t-sql/statements/create-user-transact-sql.md). Para obter mais informações sobre a instrução CREATE LOGIN, consulte [CREATE LOGIN &#40;Transact-SQL&#41;](../t-sql/statements/create-login-transact-sql.md).  
  
## <a name="2-create-a-certificate"></a>2. Criar um certificado  
Você pode criar certificados no servidor usando o banco de dados mestre como contexto, usando um banco de dados de usuário ou ambos. Há várias opções para proteger o certificado. Para obter mais informações sobre certificados, consulte [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../t-sql/statements/create-certificate-transact-sql.md).  
  
Execute este código para criar um certificado de banco de dados e protegê-lo usando uma senha.  
  
```sql  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2020';  -- Error 3701 will occur if this date is not in the future
GO  
```  
  
## <a name="3-create-and-sign-a-stored-procedure-using-the-certificate"></a>3. Criar e assinar um procedimento armazenado usando o certificado  
Use o código a seguir para criar um procedimento armazenado que seleciona dados da tabela `Vendor` no esquema do banco de dados `Purchasing`, restringindo o acesso apenas a empresas que tenham 1 como classificação de crédito. Observe que a primeira seção do procedimento armazenado exibe o contexto da conta do usuário que executa o procedimento armazenado apenas para demonstração dos conceitos. Não é exigido atender os requisitos.  
  
```sql  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Show who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1  
END  
GO  
```  
  
Execute este código para assinar o procedimento armazenado com o certificado de banco de dados usando uma senha.  
  
```sql  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
```  
  
Para obter mais informações sobre procedimentos armazenados, consulte [Procedimentos armazenados &#40;Mecanismo de Banco de Dados&#41;](../relational-databases/stored-procedures/stored-procedures-database-engine.md).  
  
Para obter mais informações sobre como assinar procedimentos armazenados, consulte [ADD SIGNATURE &#40;Transact-SQL&#41;](../t-sql/statements/add-signature-transact-sql.md).  
  
## <a name="4-create-a-certificate-account-using-the-certificate"></a>4. Criar uma conta de certificado usando o certificado  
Execute este código para criar um usuário de banco de dados (`TestCreditRatingcertificateAccount`) do certificado. Essa conta não tem logon de servidor e, em última instância, controlará o acesso às tabelas subjacentes.  
  
```sql  
USE AdventureWorks2017;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="5-grant-the-certificate-account-database-rights"></a>5. Conceder direitos de banco de dados à conta do certificado  
Execute este código para conceder direitos `TestCreditRatingcertificateAccount` à tabela base e ao procedimento armazenado.  
  
```sql  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
```  
  
Para obter mais informações sobre como conceder permissões a objetos, consulte [GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md).  
  
## <a name="6-display-the-access-context"></a>6. Exibir o contexto de acesso  
Para exibir os direitos associados ao acesso de procedimento armazenado, execute o código a seguir para conceder os direitos de execução do procedimento armazenado ao usuário `TestCreditRatingUser`.  
  
```sql  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
```  
  
Em seguida, execute o código a seguir para executar o procedimento armazenado como o logon dbo usado no servidor. Observe a saída das informações de contexto de usuário. Ela mostrará a conta dbo como o contexto com seus próprios direitos e não por meio de uma associação a um grupo.  
  
```sql  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
Execute o código a seguir para usar a instrução `EXECUTE AS` como a conta `TestCreditRatingUser` e executar o procedimento armazenado. Dessa vez você verá que o contexto de usuário está definido como o contexto de USER MAPPED TO CERTIFICATE.  
  
```sql  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
Como você assinou o procedimento, a auditoria disponível será exibida.  
  
> [!NOTE]  
> Use EXECUTE as para alternar contextos dentro de um banco de dados.  
  
## <a name="7-reset-the-environment"></a>7. Redefina o ambiente  
O código a seguir usa a instrução `REVERT` para retornar o contexto da conta atual para dbo e redefine o ambiente.  
  
```sql  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
Para obter mais informações sobre a instrução REVERT, consulte [REVERT &#40;Transact-SQL&#41;](../t-sql/statements/revert-transact-sql.md).  
  
## <a name="CompleteExample"></a>Exemplo completo  
Esta seção exibe o código de exemplo completo.  
  
```sql  
/* Step 1 - Open the AdventureWorks2017 database */  
USE AdventureWorks2017;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
  
/* Step 2 - Create a certificate in the AdventureWorks2012 database */  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2020';   -- Error 3701 will occur if this date is not in the future
GO  
  
/* Step 3 - Create a stored procedure and  
sign it using the certificate */  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Shows who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token;     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1;  
END  
GO  
  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
  
/* Step 4 - Create a database user for the certificate.   
This user has the ownership chain associated with it. */  
USE AdventureWorks2012;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
  
/* Step 5 - Grant the user database rights */  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE  
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
  
/* Step 6 - Test, using the EXECUTE AS statement */  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
  
-- Run the procedure as the dbo user, notice the output for the type  
EXEC TestCreditRatingSP;  
GO  
  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXEC TestCreditRatingSP;  
GO  
  
/* Step 7 - Clean up the example */  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
  
