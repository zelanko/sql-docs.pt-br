---
title: Criar logon (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_LOGIN_TSQL
- CREATE LOGIN
- LOGIN_TSQL
- LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], logins
- mapping logins [SQL Server]
- logins [SQL Server], creating
- CREATE LOGIN statement
- permissions [SQL Server], logins
- Windows domain accounts [SQL Server]
- re-hashing passwords
- certificates [SQL Server], logins
ms.assetid: eb737149-7c92-4552-946b-91085d8b1b01
caps.latest.revision: 101
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: e0b84743a9c3c578954560613c69f2863af8aa01
ms.contentlocale: pt-br
ms.lasthandoff: 10/24/2017

---
# <a name="create-login-transact-sql"></a>CREATE LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cria um logon do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
-- Syntax for SQL Server  
  
CREATE LOGIN login_name { WITH <option_list1> | FROM <sources> }  
  
<option_list1> ::=   
    PASSWORD = { 'password' | hashed_password HASHED } [ MUST_CHANGE ]  
    [ , <option_list2> [ ,... ] ]  
  
<option_list2> ::=    
    SID = sid  
    | DEFAULT_DATABASE = database      
    | DEFAULT_LANGUAGE = language  
    | CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
    | CREDENTIAL = credential_name   
  
<sources> ::=  
    WINDOWS [ WITH <windows_options>[ ,... ] ]  
    | CERTIFICATE certname  
    | ASYMMETRIC KEY asym_key_name  
  
<windows_options> ::=        
    DEFAULT_DATABASE = database  
    | DEFAULT_LANGUAGE = language  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse  
  
CREATE LOGIN login_name  
 { WITH <option_list3> }  
  
<option_list3> ::=   
    PASSWORD = { 'password' }  
    [ SID = sid ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
CREATE LOGIN loginName { WITH <option_list1> | FROM WINDOWS }  
  
<option_list1> ::=   
    PASSWORD = { 'password' } [ MUST_CHANGE ]  
    [ , <option_list2> [ ,... ] ]  
  
<option_list2> ::=    
      CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
```  
  
## <a name="arguments"></a>Argumentos  
 *login_name*  
 Especifica o nome do logon criado. Há quatro tipos de logon: logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], logons do Windows, logons mapeados por certificado e logons mapeados por chave assimétrica. Quando você está criando logons mapeados de uma conta de domínio do Windows, você deve usar o nome de logon anterior ao Windows 2000 no formato [\<domainName >\\< login_name >]. Você não pode usar um UPN no formato login_name@DomainName. Para obter um exemplo, consulte o exemplo D posteriormente neste tópico. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]logons de autenticação são do tipo **sysname** e deve obedecer às regras para [identificadores](http://msdn.microsoft.com/library/ms175874.aspx) e não pode conter um '**\\**'. Os logons do Windows podem conter um '**\\**'. Logons com base em usuários do Active Directory, são limitados aos nomes de menos de 21 caracteres.  
  
 SENHA **='***senha***'**  
 Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] somente de logons. Especifica a senha do logon que está sendo criado. Use uma senha forte. Para obter mais informações, consulte [senhas fortes](../../relational-databases/security/strong-passwords.md) e [política de senha](../../relational-databases/security/password-policy.md). Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]armazenadas, informações de senha são calculadas usando SHA-512 da senha com valor de sal.  
  
 As senhas diferenciam maiúsculas de minúsculas. As senhas sempre devem ter pelo menos 8 caracteres e não podem exceder 128 caracteres.  Elas podem incluir caracteres de a-z, A-Z, 0-9, e a maioria dos caracteres não alfanuméricos. Senhas não podem conter aspas simples, ou o *login_name*.  
  
 SENHA  **=**  *hashed_password*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Só se aplica à palavra-chave HASHED. Especifica o valor com hash da senha para o logon que está sendo criado.  
  
 HASHED  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] somente de logons. Especifica que a senha digitada depois do argumento PASSWORD já esteja com hash. Se esta opção não for selecionada, a cadeia de caracteres inserida como senha terá hash antes de ser armazenada no banco de dados. Essa opção deve ser usada somente para migrar bancos de dados de um servidor para outro. Não use a opção HASHED para criar novos logons. A opção HASHED não pode ser usada com os hashes criados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7 ou anterior.  
  
 MUST_CHANGE  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] somente de logons. Se esta opção estiver incluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicita ao usuário uma nova senha quando o novo logon for usado pela primeira vez.  
  
 CREDENCIAL  **=**  *credential_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 O nome de uma credencial a ser mapeada para um novo logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A credencial já deve existir no servidor. Atualmente, esta opção vincula apenas a credencial a um logon. Uma credencial não pode ser mapeada para o logon de administrador do sistema (sa).  
  
 SID = *sid*  
 Usado para recriar um logon. Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] somente os logons de autenticação, os logons de autenticação do Windows. Especifica o SID do novo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de autenticação. Se essa opção não for usada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribui automaticamente um SID. A estrutura do SID depende de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versão.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SID de logon: uma 16 bytes (**binário (16)**) valor literal com base em um GUID. Por exemplo, `SID = 0x14585E90117152449347750164BA00A7`.  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)]SID de logon: uma estrutura de SID válida para [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Normalmente, isso é uma 32 bytes (**binary(32)**) literal consiste em `0x01060000000000640000000000000000` além de 16 bytes representando um GUID. Por exemplo, `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`.  
  
DEFAULT_DATABASE  **=**  *banco de dados*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o banco de dados padrão a ser atribuído ao logon. Se esta opção não for incluída, o banco de dados padrão será definido como master.  
  
DEFAULT_LANGUAGE  **=**  *idioma*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o idioma padrão a ser atribuído ao logon. Se esta opção não for incluída, o idioma padrão será definido como o idioma padrão atual do servidor. Se o idioma padrão do servidor for alterado posteriormente, o idioma padrão do logon permanecerá inalterado.  
  
CHECK_EXPIRATION  **=**  {ON | **OFF** }  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] somente de logons. Especifica se a política de expiração de senha deve ser aplicada neste logon. O valor padrão é OFF.  
  
CHECK_POLICY  **=**  { **ON** | OFF}  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] somente de logons. Especifica se as políticas de senha do Windows do computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução devem ser aplicadas neste logon. O valor padrão é ON.  
  
 Se a diretiva de Windows exigir senhas fortes, as senhas deverão conter pelo menos três das quatro características a seguir:  
  
-   Um caractere maiúsculo (A-Z).  
-   Um caractere minúsculo (a-z).  
-   Um dígito (0-9).  
-   Um dos caracteres não alfanuméricos, como um espaço, _, @, *, ^, %, !, $, # ou &.  
  
WINDOWS  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica que o logon seja mapeado para um logon do Windows.  
  
CERTIFICADO *certname*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o nome de um certificado a ser associado a este logon. Este certificado já deve ocorrer no banco de dados mestre.  
  
CHAVE ASSIMÉTRICA *asym_key_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o nome de uma chave assimétrica a ser associada a este logon. Esta chave já deve ocorrer no banco de dados mestre.  
  
## <a name="remarks"></a>Comentários  
 As senhas diferenciam maiúsculas de minúsculas.  
  
 O hash prévio de senhas tem suporte somente durante a criação de logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se MUST_CHANGE for especificado, CHECK_EXPIRATION e CHECK_POLICY deverão ser definidos como ON. Caso contrário, a instrução falhará.  
  
 Não há suporte para uma combinação de CHECK_POLICY = OFF e CHECK_EXPIRATION = ON.  
  
 Quando CHECK_POLICY é definido como OFF, *lockout_time* é redefinido e CHECK_EXPIRATION é definido como OFF.  
  
> [!IMPORTANT]  
>  CHECK_EXPIRATION e CHECK_POLICY serão aplicados apenas no [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] e posteriores. Para obter mais informações, consulte [Password Policy](../../relational-databases/security/password-policy.md).  
  
 Os logons criados a partir de certificados ou chaves assimétricas só são usados para assinatura de código. Eles não podem ser usados para a conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode criar um logon a partir de um certificado ou chave assimétrica somente quando o certificado ou a chave já existirem em master.  
  
 Para um script transferir logons, consulte [Como transferir os logons e senhas entre instâncias do SQL Server 2005 e SQL Server 2008](http://support.microsoft.com/kb/918992).  
  
 Criar um logon automaticamente habilita o novo logon e concede a ele a permissão **CONNECT SQL** de nível de servidor.  
  
 Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-and-includesssdwincludessssdw-mdmd-logins"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] logons  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], o **CREATE LOGIN** instrução deve ser a única instrução em um lote.  
  
 Em alguns métodos de se conectar a [!INCLUDE[ssSDS](../../includes/sssds-md.md)], como **sqlcmd**, você deve acrescentar o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] nome do servidor para o nome de logon na cadeia de conexão usando o  *\<logon >* @  *\<server >* notação. Por exemplo, se seu logon for `login1` e o nome totalmente qualificado do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] servidor é `servername.database.windows.net`, o *username* parâmetro da cadeia de caracteres de conexão deve ser `login1@servername`. Porque o comprimento total do *username* parâmetro é de 128 caracteres, *login_name* é limitada a 127 caracteres menos o comprimento do nome do servidor. No exemplo, `login_name` pode ter apenas 117 caracteres porque `servername` tem 10 caracteres.  
  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] você deve estar conectado ao banco de dados mestre para criar um logon.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]as regras permitem que você crie um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de autenticação no formato \<loginname > @\<servername >. Se seu [!INCLUDE[ssSDS](../../includes/sssds-md.md)] servidor é **myazureserver** e seu logon for  **myemail@live.com** , você deverá fornecer seu logon como  **myemail@live.com @myazureserver**  .  
  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessárias para autenticar uma conexão e as regras de firewall de nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e certifique-se de que um banco de dados tem a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE &#40; Transact-SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
 Para obter mais informações sobre [!INCLUDE[ssSDS](../../includes/sssds-md.md)] logons, consulte [Gerenciando bancos de dados e logons no banco de dados SQL do Windows Azure](http://msdn.microsoft.com/library/ee336235.aspx).  
  
## <a name="permissions"></a>Permissões  
 Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], requer **ALTER ANY LOGIN** permissão no servidor ou associação de **securityadmin** função de servidor fixa.  
  
 no [!INCLUDE[ssSDS](../../includes/sssds-md.md)], somente o logon principal do nível de servidor (criado pelo processo de provisionamento) ou membros da função de banco de dados `loginmanager` no banco de dados mestre podem criar novos logons.  
  
 Se a opção **CREDENTIAL** for usada, também será necessária a permissão **ALTER ANY CREDENTIAL** no servidor.  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de criar um logon, o logon pode se conectar ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou [!INCLUDE[ssSDS](../../includes/sssds-md.md)] mas só tem as permissões concedidas para o **pública** função. Execute algumas das atividades a seguir.  
  
-   Para conectar-se a um banco de dados, crie um usuário de banco de dados para o logon. Para obter mais informações, consulte [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md).  
  
-   Criar uma função de servidor definida pelo usuário usando [CREATE SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-server-role-transact-sql.md). Use **ALTER SERVER ROLE** … **Adicionar membro** para adicionar o novo logon à função de servidor definida pelo usuário. Para obter mais informações, consulte [CREATE SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/create-server-role-transact-sql.md) e [ALTER SERVER ROLE &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
-   Use **sp_addsrvrolemember** para adicionar o logon a uma função de servidor fixa. Para obter mais informações, consulte [funções de nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md) e [sp_addsrvrolemember &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md).  
  
-   Use o **GRANT** instrução para conceder permissões de nível de servidor para o novo logon ou uma função que contém o logon. Para obter mais informações, veja [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-login-with-a-password"></a>A. Criando um logon com uma senha  
 O exemplo a seguir cria um logon para um usuário específico e atribui uma senha.  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-with-a-password"></a>B. Criando um logon com uma senha  
 O exemplo a seguir cria um logon para um usuário específico e atribui uma senha. A opção `MUST_CHANGE` requer que os usuários alterem essa senha na primeira vez em que eles conectam ao servidor.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>' MUST_CHANGE;  
GO  
```  
  
### <a name="c-creating-a-login-mapped-to-a-credential"></a>C. Criando um logon mapeado para uma credencial  
 O exemplo a seguir cria o logon para um usuário específico usando o usuário. Esse logon é mapeado para a credencial.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>',   
    CREDENTIAL = <credentialName>;  
GO  
```  
  
### <a name="d-creating-a-login-from-a-certificate"></a>D. Criando um logon a partir de um certificado  
 O exemplo a seguir cria um logon para um usuário específico de um certificado em master.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
USE MASTER;  
CREATE CERTIFICATE <certificateName>  
    WITH SUBJECT = '<login_name> certificate in master database',  
    EXPIRY_DATE = '12/05/2025';  
GO  
CREATE LOGIN <login_name> FROM CERTIFICATE <certificateName>;  
GO  
```  
  
### <a name="e-creating-a-login-from-a-windows-domain-account"></a>E. Criando um logon a partir de uma conta de domínio do Windows  
 O exemplo a seguir cria um logon a partir de uma conta de domínio do Windows.  
  
**Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
CREATE LOGIN [<domainName>\<login_name>] FROM WINDOWS;  
GO  
```  
  
### <a name="f-creating-a-login-from-a-sid"></a>F. Criando um logon por meio de um SID  
 O exemplo a seguir cria primeiro um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon de autenticação e determina o SID do logon.  
  
```  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 Minha consulta retorna 0x241C11948AEEB749B0D22646DB1A19F2 como o SID. Sua consulta retornará um valor diferente. As instruções a seguir excluem o logon e depois o recriam. Use o SID da consulta anterior.  
  
```  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos:[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="g-creating-a-sql-server-authentication-login-with-a-password"></a>G. Criando um logon de autenticação do SQL Server com uma senha  
 O exemplo a seguir cria o logon `Mary7` com senha `A2c3456`.  
  
```tsql  
CREATE LOGIN Mary7 WITH PASSWORD = 'A2c3456$#' ;  
```  
  
### <a name="h-using-options"></a>H. Usando opções  
 O exemplo a seguir cria o logon `Mary8` com senha e alguns argumentos opcionais.  
  
```  
CREATE LOGIN Mary8 WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
```  
  
### <a name="i-creating-a-login-from-a-windows-domain-account"></a>I. Criando um logon a partir de uma conta de domínio do Windows  
 O exemplo a seguir cria um logon de uma conta de domínio do Windows chamada `Mary` no `Contoso` domínio.  
  
```  
CREATE LOGIN [Contoso\Mary] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Política de senha](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [Remover logon &#40; Transact-SQL &#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Crie um logon](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  

