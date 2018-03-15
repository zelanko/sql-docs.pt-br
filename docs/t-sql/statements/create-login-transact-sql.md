---
title: CREATE LOGIN (Transact-SQL) | Microsoft Docs
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 2e94847ca10923bba05e228f36a25e5caa8c2027
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
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
 Especifica o nome do logon criado. Há quatro tipos de logon: logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], logons do Windows, logons mapeados por certificado e logons mapeados por chave assimétrica. Ao criar logons mapeados de uma conta de domínio do Windows, você deve usar o nome de logon de usuário de versões anteriores ao Windows 2000 no formato [\<domainName>\\<login_name>]. Você não pode usar um UPN no formato login_name@DomainName. Para obter um exemplo, consulte o exemplo D posteriormente neste tópico. Os logons de autenticação no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são do tipo **sysname** e devem estar em conformidade com as regras para [Identificadores](http://msdn.microsoft.com/library/ms175874.aspx) e não podem conter um '**\\**'. Os logons do Windows podem conter um '**\\**'. Logons baseados em usuários do Active Directory estão limitados a nomes de menos de 21 caracteres.  
  
 PASSWORD **='***password***'**  
 Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Especifica a senha do logon que está sendo criado. Use uma senha forte. Para obter mais informações, veja [Senhas fortes](../../relational-databases/security/strong-passwords.md) e [Política de senha](../../relational-databases/security/password-policy.md). Começando com [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]armazenadas, informações de senha armazenadas são calculadas usando SHA-512 da senha com valor de sal.  
  
 As senhas diferenciam maiúsculas de minúsculas. As senhas sempre devem ter pelo menos 8 caracteres e não podem exceder 128 caracteres.  Elas podem incluir caracteres de a-z, A-Z, 0-9, e a maioria dos caracteres não alfanuméricos. As senhas não podem conter aspas simples nem o *login_name*.  
  
 PASSWORD **=***hashed_password*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Só se aplica à palavra-chave HASHED. Especifica o valor com hash da senha para o logon que está sendo criado.  
  
 HASHED  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Especifica que a senha digitada depois do argumento PASSWORD já esteja com hash. Se esta opção não for selecionada, a cadeia de caracteres inserida como senha terá hash antes de ser armazenada no banco de dados. Essa opção deve ser usada somente para migrar bancos de dados de um servidor para outro. Não use a opção HASHED para criar novos logons. A opção HASHED não pode ser usada com os hashes criados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7 ou anterior.  
  
 MUST_CHANGE  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se esta opção estiver incluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicita ao usuário uma nova senha quando o novo logon for usado pela primeira vez.  
  
 CREDENTIAL **=***credential_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 O nome de uma credencial a ser mapeada para um novo logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A credencial já deve existir no servidor. Atualmente, esta opção vincula apenas a credencial a um logon. Uma credencial não pode ser mapeada para o logon de Administrador do Sistema (sa).  
  
 SID = *sid*  
 Usado para recriar um logon. Aplica-se apenas aos logons de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e não aos logons de autenticação do Windows. Especifica o SID do novo logon de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se esta opção não for usada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atribuirá um SID automaticamente. A estrutura do SID depende da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   SID de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: uma valor literal de 16 bytes (**binary(16)**) baseado em um GUID. Por exemplo, `SID = 0x14585E90117152449347750164BA00A7`.  
  
-   SID de logon no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]: uma estrutura de SID válida para o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Normalmente, trata-se de um literal de 32 bytes (**binary(32)**) que consiste em `0x01060000000000640000000000000000`, além de 16 bytes representando um GUID. Por exemplo, `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`.  
  
DEFAULT_DATABASE **=***database*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o banco de dados padrão a ser atribuído ao logon. Se esta opção não for incluída, o banco de dados padrão será definido como master.  
  
DEFAULT_LANGUAGE **=***language*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o idioma padrão a ser atribuído ao logon. Se esta opção não for incluída, o idioma padrão será definido como o idioma padrão atual do servidor. Se o idioma padrão do servidor for alterado posteriormente, o idioma padrão do logon permanecerá inalterado.  
  
CHECK_EXPIRATION **=** { ON | **OFF** }  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Especifica se a política de expiração de senha deve ser aplicada neste logon. O valor padrão é OFF.  
  
CHECK_POLICY **=** { **ON** | OFF }  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Especifica se as políticas de senha do Windows do computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução devem ser aplicadas neste logon. O valor padrão é ON.  
  
 Se a diretiva de Windows exigir senhas fortes, as senhas deverão conter pelo menos três das quatro características a seguir:  
  
-   Um caractere maiúsculo (A-Z).  
-   Um caractere minúsculo (a-z).  
-   Um dígito (0-9).  
-   Um dos caracteres não alfanuméricos, como um espaço, _, @, *, ^, %, !, $, # ou &.  
  
WINDOWS  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica que o logon seja mapeado para um logon do Windows.  
  
CERTIFICATE *certname*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o nome de um certificado a ser associado a este logon. Este certificado já deve ocorrer no banco de dados mestre.  
  
ASYMMETRIC KEY *asym_key_name*  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o nome de uma chave assimétrica a ser associada a este logon. Esta chave já deve ocorrer no banco de dados mestre.  
  
## <a name="remarks"></a>Remarks  
 As senhas diferenciam maiúsculas de minúsculas.  
  
 O hash prévio de senhas tem suporte somente durante a criação de logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se MUST_CHANGE for especificado, CHECK_EXPIRATION e CHECK_POLICY deverão ser definidos como ON. Caso contrário, a instrução falhará.  
  
 Não há suporte para uma combinação de CHECK_POLICY = OFF e CHECK_EXPIRATION = ON.  
  
 Quando CHECK_POLICY é definida como OFF, *lockout_time* é redefinido e CHECK_EXPIRATION é definido como OFF.  
  
> [!IMPORTANT]  
>  CHECK_EXPIRATION e CHECK_POLICY serão aplicados apenas no [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] e posteriores. Para obter mais informações, consulte [Password Policy](../../relational-databases/security/password-policy.md).  
  
 Os logons criados a partir de certificados ou chaves assimétricas só são usados para assinatura de código. Eles não podem ser usados para a conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode criar um logon a partir de um certificado ou chave assimétrica somente quando o certificado ou a chave já existirem em master.  
  
 Para um script transferir logons, consulte [Como transferir os logons e senhas entre instâncias do SQL Server 2005 e SQL Server 2008](http://support.microsoft.com/kb/918992).  
  
 Criar um logon automaticamente habilita o novo logon e concede a ele a permissão **CONNECT SQL** de nível de servidor.  
 
 O [modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md) do servidor deve corresponder ao tipo de logon para permitir o acesso.
  
 Para obter informações sobre como criar um sistema de permissões, veja [Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-and-includesssdwincludessssdw-mdmd-logins"></a>Logins no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], a instrução **CREATE LOGIN** deve ser a única instrução em um lote.  
  
 Em alguns métodos de se conectar ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)], como **sqlcmd**, você deve acrescentar o nome do servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ao nome do logon na cadeia de conexão usando a notação *\<login>*@*\<server>*. Por exemplo, se o seu logon for `login1` e o nome totalmente qualificado do servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] for `servername.database.windows.net`, o parâmetro *username* da cadeia de conexão deverá ser `login1@servername`. Como o comprimento total do parâmetro *username* é 128 caracteres, *login_name* é limitado a 127 caracteres menos o comprimento do nome de servidor. No exemplo, `login_name` pode ter apenas 117 caracteres porque `servername` tem 10 caracteres.  
  
 No [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], você deve estar conectado ao banco de dados mestre para criar um logon.  
  
 As regras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permitem criar um logon de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no formato \<loginname>@\<servername>. Se seu servidor do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] for **myazureserver** e o logon for **myemail@live.com**, você deverá fornecer seu logon como **myemail@live.com@myazureserver**.  
  
 Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessários para autenticar uma conexão e as regras de firewall no nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
 Para obter mais informações sobre logons do [!INCLUDE[ssSDS](../../includes/sssds-md.md)], veja [Gerenciando bancos de dados e logons no Banco de Dados SQL do Microsoft Azure](http://msdn.microsoft.com/library/ee336235.aspx).  
  
## <a name="permissions"></a>Permissões  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], exige a permissão **ALTER ANY LOGIN** no servidor ou associação na função de servidor fixa**securityadmin**.  
  
 no [!INCLUDE[ssSDS](../../includes/sssds-md.md)], somente o logon principal do nível de servidor (criado pelo processo de provisionamento) ou membros da função de banco de dados `loginmanager` no banco de dados mestre podem criar novos logons.  
  
 Se a opção **CREDENTIAL** for usada, também será necessária a permissão **ALTER ANY CREDENTIAL** no servidor.  
  
## <a name="next-steps"></a>Next Steps  
 Depois de criar um logon, o logon pode se conectar ao aplicativo [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou [!INCLUDE[ssSDS](../../includes/sssds-md.md)], mas tem as permissões concedidas apenas à função **pública** . Execute algumas das atividades a seguir.  
  
-   Para conectar-se a um banco de dados, crie um usuário de banco de dados para o logon. Para obter mais informações, consulte [CREATE USER &#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md).  
  
-   Crie uma função de servidor definida pelo usuário usando [CREATE SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-role-transact-sql.md). Use **ALTER SERVER ROLE** … **ADD MEMBER** para adicionar o novo logon á função de servidor definida pelo usuário. Para obter mais informações, veja [CREATE SERVER ROLE &#40;Transact-SQL&#41; ](../../t-sql/statements/create-server-role-transact-sql.md) e [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
-   Use **sp_addsrvrolemember** para adicionar o logon a uma função de servidor fixa. Para obter mais informações, veja [Funções em nível de servidor](../../relational-databases/security/authentication-access/server-level-roles.md) e [sp_addsrvrolemember &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md).  
  
-   Use a instrução **GRANT** para conceder permissões do nível de servidor para o novo logon ou para uma função que contém o logon. Para obter mais informações, veja [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md).  
  
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
 O exemplo a seguir cria um logon para um usuário específico de um certificado em mestre.  
  
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
 O exemplo a seguir cria primeiro um logon de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e determina o SID do logon.  
  
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
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="g-creating-a-sql-server-authentication-login-with-a-password"></a>G. Criando um logon de autenticação do SQL Server com uma senha  
 O exemplo a seguir cria o logon `Mary7` com senha `A2c3456`.  
  
```sql  
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
 O exemplo a seguir cria um logon usando uma conta de domínio do Windows chamada `Mary` no domínio `Contoso`.  
  
```  
CREATE LOGIN [Contoso\Mary] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Guia de Introdução às permissões do mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [Política de senha](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [Criar um logon](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  
