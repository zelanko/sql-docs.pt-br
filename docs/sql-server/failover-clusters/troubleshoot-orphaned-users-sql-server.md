---
title: Solução de problemas de usuários órfãos (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- orphaned users [SQL Server]
- logins [SQL Server], orphaned users
- troubleshooting [SQL Server], user accounts
- user accounts [SQL Server], orphaned users
- failover [SQL Server], managing metadata
- database mirroring [SQL Server], metadata
- users [SQL Server], orphaned
ms.assetid: 11eefa97-a31f-4359-ba5b-e92328224133
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d158cff3a2761ae27357088488075e50381145b5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825884"
---
# <a name="troubleshoot-orphaned-users-sql-server"></a>Solução de problemas de usuários órfãos (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Os usuários órfãos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ocorrem quando um usuário de banco de dados tem base em um logon no banco de dados **mestre** , mas o logon não existe mais no **mestre**. Isso pode ocorrer quando o logon é excluído, ou quando o banco de dados é movido para outro servidor onde o logon não existe. Este tópico descreve como localizar usuários órfãos e remapeá-los para logons.  
  
> [!NOTE]  
>  Reduza a possibilidade de usuários órfãos usando usuários de banco de dados independente para os bancos de dados que podem ser movidos. Para obter mais informações, consulte [Usuários de bancos de dados independentes – Tornando seu banco de dados portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
## <a name="background"></a>Plano de fundo  
 Para se conectar a um banco de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando uma entidade de segurança (identidade do usuário do banco de dados) com base em um logon, a entidade deve ter um logon válido no banco de dados **mestre** . Esse logon é usado no processo de autenticação que verifica a identidade da entidade e determina se ela tem permissão para conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma instância do servidor são visíveis na exibição do catálogo **sys.server_principals** e na exibição de compatibilidade **sys.sql_logins** .  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acessam bancos de dados individuais como um "usuário do banco de dados" mapeado para o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Há três exceções a essa regra:  
  
-   Usuários de banco de dados independente  
  
     Os usuários de banco de dados independente se autenticam no nível do banco de dados de usuário e não estão associados a logons. Isso é recomendado porque os bancos de dados são mais portáteis e os usuários de banco de dados independente não podem se tornar órfãos. No entanto, eles devem ser recriados para cada banco de dados. Isso pode ser impraticável em um ambiente com muitos bancos de dados.  
  
-   A conta de **convidado** .  
  
     Quando habilitada no banco de dados, essa conta permite que os logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não estejam mapeados para um usuário de banco de dados acessem o banco de dados como o usuário **convidado** . A conta de **convidado** está desabilitada por padrão.  
  
-   Associação de grupo do Microsoft Windows.  
  
     Um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criado a partir de um usuário do Windows poderá acessar um banco de dados se esse usuário for membro de um grupo do Windows que também seja um usuário no banco de dados.  
  
 Informações sobre o mapeamento de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um usuário do banco de dados são armazenadas no banco de dados. Isso inclui o nome do usuário do banco de dados e o SID do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondente. As permissões desse usuário de banco de dados são aplicadas para autorização no banco de dados.  
  
 Um usuário de banco de dados (com base em um logon) para o qual o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondente não esteja definido, ou que esteja definido incorretamente em uma instância do servidor, não pode fazer logon na instância. Esse usuário é um *usuário órfão* do banco de dados nessa instância do servidor. A condição de órfão pode ocorrer se o usuário do banco de dados for mapeado para um SID de logon que não esteja presente na instância do `master` . Um usuário de banco de dados pode se tornar órfão após um banco de dados ser restaurado ou anexado a uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , na qual o logon nunca foi criado. Um usuário do banco de dados também se tornará órfão se o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondente for descartado. Mesmo se o logon for recriado, ele terá um SID diferente, então o usuário do banco de dados ainda será órfão.  
  
## <a name="to-detect-orphaned-users"></a>Para detectar usuários órfãos  

**Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e PDW**

Para detectar usuários órfãos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com base em logons de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ausentes, execute a seguinte instrução no banco de dados do usuário:  
  
```  
SELECT dp.type_desc, dp.SID, dp.name AS user_name  
FROM sys.database_principals AS dp  
LEFT JOIN sys.server_principals AS sp  
    ON dp.SID = sp.SID  
WHERE sp.SID IS NULL  
    AND authentication_type_desc = 'INSTANCE';  
```  
  
 A saída lista os usuários de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e as SIDs (IDs de segurança) correspondentes no banco de dados atual que não estão vinculados a um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

**Para Banco de Dados SQL e SQL Data Warehouse**

A tabela `sys.server_principals` não está disponível no Banco de Dados SQL ou no SQL Data Warehouse. Identifique usuários órfãos nesses ambientes com as seguintes etapas:

1. Conecte-se ao banco de dados `master` e selecione as SIDs para os logons com a seguinte consulta:
    ```
    SELECT sid 
    FROM sys.sql_logins 
    WHERE type = 'S'; 
    ```

2. Conecte-se ao banco de dados de usuário e examine as SIDs dos usuários na tabela `sys.database_principals` usando a seguinte consulta:

    ```
    SELECT name, sid, principal_id
    FROM sys.database_principals 
    WHERE type = 'S' 
      AND name NOT IN ('guest', 'INFORMATION_SCHEMA', 'sys')
      AND authentication_type_desc = 'INSTANCE';
    ```

3. Compare as duas listas para determinar se há SIDs de usuário na tabela `sys.database_principals` do banco de dados do usuário que não correspondem às SIDs de logon na tabela `sql_logins` do banco de dados mestre. 
  
## <a name="to-resolve-an-orphaned-user"></a>Para resolver um usuário órfão  
No banco de dados mestre, use a instrução [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) com a opção de SID para recriar um logon ausente, fornecendo a `SID` do usuário do banco de dados obtida na seção anterior:  
  
```  
CREATE LOGIN <login_name>   
WITH PASSWORD = '<use_a_strong_password_here>',  
SID = <SID>;  
```  
  
 Para mapear um usuário órfão para um logon já existente no **mestre**, execute a instrução [ALTER USER](../../t-sql/statements/alter-user-transact-sql.md) no banco de dados do usuário, especificando o nome de logon.  
  
```  
ALTER USER <user_name> WITH Login = <login_name>;  
```  
  
 Ao recriar um logon ausente, o usuário pode acessar o banco de dados usando a senha fornecida. Em seguida, o usuário pode alterar a senha da conta de logon usando a instrução ALTER LOGIN.  
  
```  
ALTER LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
```  
  
> [!IMPORTANT]  
>  Qualquer logon pode alterar sua própria senha. Somente logons com a permissão `ALTER ANY LOGIN` podem alterar a senha de logon de outro usuário. Porém, somente membros da função **sysadmin** podem modificar senhas de membros da função **sysadmin** .  
  
 O procedimento preterido [sp_change_users_login](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md) também funciona com usuários órfãos. `sp_change_users_login` não pode ser usado com [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER USER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-user-transact-sql.md)   
 [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sp_change_users_login &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-change-users-login-transact-sql.md)   
 [sp_addlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_grantlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_password &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)   
 [sys.sysusers &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysusers-transact-sql.md)   
 [sys.sql_logins](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md) [sys.syslogins &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslogins-transact-sql.md)  
  
  
