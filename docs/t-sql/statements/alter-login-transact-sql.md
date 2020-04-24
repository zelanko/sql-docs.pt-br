---
title: ALTER LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/10/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_LOGIN_TSQL
- ALTER LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER LOGIN statement
- change password
- mapping logins [SQL Server]
- logins [SQL Server], modifying
- passwords [SQL Server], modifying
- names [SQL Server], logins
- modifying login accounts
ms.assetid: e247b84e-c99e-4af8-8b50-57586e1cb1c5
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4efecdda3375430a380e10ddb1845f08050ce4a3
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81627646"
---
# <a name="alter-login-transact-sql"></a>ALTER LOGIN (Transact-SQL)

Altera as propriedades de uma conta de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## <a name="click-a-product"></a>Clique em um produto!

Na linha a seguir, clique em qualquer nome de produto de seu interesse. O clique exibe conteúdo diferente aqui nesta página da Web, apropriado para qualquer produto no qual você clicar.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions"

||||||
|-|-|-|-|-|
|**_\* SQL Server \*_** &nbsp;|[Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-login-transact-sql.md?view=azuresqldb-current)|[Instância gerenciada<br />do Banco de Dados SQL](alter-login-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](alter-login-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System (PDW)](alter-login-transact-sql.md?view=aps-pdw-2016)
||||||

&nbsp;

## <a name="sql-server"></a>SQL Server

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for SQL Server

ALTER LOGIN login_name
    {
    <status_option>
    | WITH <set_option> [ ,... ]
    | <cryptographic_credential_option>
    }
[;]

<status_option> ::=
        ENABLE | DISABLE

<set_option> ::=
    PASSWORD = 'password' | hashed_password HASHED
    [
      OLD_PASSWORD = 'oldpassword'
      | <password_option> [<password_option> ]
    ]
    | DEFAULT_DATABASE = database
    | DEFAULT_LANGUAGE = language
    | NAME = login_name
    | CHECK_POLICY = { ON | OFF }
    | CHECK_EXPIRATION = { ON | OFF }
    | CREDENTIAL = credential_name
    | NO CREDENTIAL

<password_option> ::=
    MUST_CHANGE | UNLOCK
  
<cryptographic_credentials_option> ::=
    ADD CREDENTIAL credential_name
  | DROP CREDENTIAL credential_name
```

## <a name="arguments"></a>Argumentos

*login_name* Especifica o nome do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo alterado. Logons no domínio devem ser colocados entre colchetes no formato [domínio\usuário].

ENABLE | DISABLE Habilita ou desabilita este logon. Desabilitar um logon não afeta o comportamento de logons que já estão conectados. (Use a instrução `KILL` para encerrar as conexões existentes.) Os logons desabilitados retêm suas permissões e ainda podem ser representados.

PASSWORD **='** _password_ **'** Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica a senha do logon que está sendo alterado. As senhas diferenciam maiúsculas de minúsculas.

PASSWORD **=** _hashed\_password_ Aplica-se somente à palavra-chave HASHED. Especifica o valor com hash da senha para o logon que está sendo criado.

> [!IMPORTANT]
> Quando um logon (ou um usuário de banco de dados independente) se conecta e é autenticado, a conexão armazena em cache as informações de identidade sobre o logon. Para um logon de Autenticação do Windows, isso inclui informações sobre a associação em grupos do Windows. A identidade do logon permanece autenticada desde que a conexão seja mantida. Para forçar alterações na identidade, como uma redefinição de senha ou alteração na associação de grupo do Windows, o logon deve fazer logoff da autoridade de autenticação (Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) e fazer logon novamente. Um membro da função de servidor fixa ou **sysadmin** ou qualquer logon com a permissão **ALTER ANY CONNECTION** pode usar o comando **KILL** para terminar uma conexão e forçar um logon para reconectar. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] pode reutilizar informações de conexão ao abrir várias conexões para as janelas do Pesquisador de Objetos e do Editor de Consultas. Feche todas as conexões para forçar a reconexão.

HASHED Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica que a senha digitada depois do argumento PASSWORD já esteja com hash. Se esta opção não for selecionada, a senha terá hash antes de ser armazenada no banco de dados. Essa opção deve ser usada somente para sincronização de logon entre dois servidores. Não use a opção HASHED para alterar senhas rotineiramente.

OLD_PASSWORD **='** _oldpassword_ **'** Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A senha atual do logon a que uma senha nova será atribuída. As senhas diferenciam maiúsculas de minúsculas.

MUST_CHANGE Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esta opção estiver incluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicitará uma senha atualizada quando o logon alterado for usado pela primeira vez.

DEFAULT_DATABASE **=** _database_ Especifica um banco de dados padrão a ser atribuído ao logon.

DEFAULT_LANGUAGE **=** _language_ Especifica um idioma padrão a ser atribuído ao logon. O idioma padrão para todos os logons de Banco de Dados SQL é o inglês e não pode ser alterado. O idioma padrão do logon `sa` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em Linux, é o inglês, mas pode ser alterado.

NAME = *login_name* O nome novo do logon que está sendo renomeado. Se este for um logon do Windows, o SID do administrador do Windows correspondente ao novo nome deverá corresponder ao SID associado ao logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O nome novo de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode conter um caractere de barra invertida (\\).

CHECK_EXPIRATION = { ON | **OFF** } Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica se a política de expiração de senha deve ser aplicada neste logon. O valor padrão é OFF.

CHECK_POLICY **=** { **ON** | OFF } somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica se as políticas de senha do Windows do computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução devem ser aplicadas neste logon. O valor padrão é ON.

CREDENTIAL = *credential_name* O nome de uma credencial a ser mapeada para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A credencial já deve existir no servidor. Para obter mais informações, consulte [Credenciais](../../relational-databases/security/authentication-access/credentials-database-engine.md). Não é possível mapear uma credencial para logon do sa.

NO CREDENTIAL Remove qualquer mapeamento existente do logon para uma credencial de servidor. Para obter mais informações, consulte [Credenciais](../../relational-databases/security/authentication-access/credentials-database-engine.md).

UNLOCK Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica que um logon bloqueado deve ser desbloqueado.

ADD CREDENTIAL Adiciona uma credencial do provedor EKM (Gerenciamento de chave extensível) ao logon. Para obter mais informações, consulte [EKM (Gerenciamento extensível de chaves)](../../relational-databases/security/encryption/extensible-key-management-ekm.md).

DROP CREDENTIAL Remove uma credencial do provedor de EKM (Gerenciamento de chave extensível) do logon. Para obter mais informações, consulte [EKM (Gerenciamento de chave extensível)] (../.. /relational-databases/security/encryption/extensible-key-management-ekm.md).

## <a name="remarks"></a>Comentários

Quando CHECK_POLICY estiver definido como ON, o argumento HASHED não poderá ser usado.

Quando CHECK_POLICY for alterado para ON, o seguinte comportamento ocorrerá:

- O histórico de senhas é inicializado com o valor do hash da senha atual.

  Quando CHECK_POLICY for alterado para OFF, o seguinte comportamento ocorrerá:

- CHECK_EXPIRATION também será definido como OFF.
- O histórico de senhas será apagado.
- O valor de *lockout_time* é redefinido.

Se MUST_CHANGE for especificado, CHECK_EXPIRATION e CHECK_POLICY deverão ser definidos como ON. Caso contrário, a instrução falhará.

Se CHECK_POLICY for definido como OFF, CHECK_EXPIRATION não poderá ser definido como ON. Uma instrução ALTER LOGON com essa combinação de opções falhará.

Você não pode usar ALTER_LOGIN com o argumento DISABLE para negar acesso a um grupo do Windows. Por exemplo, ALTER_LOGIN [*domain\group*] DISABLE retornará a seguinte mensagem de erro:

    `"Msg 15151, Level 16, State 1, Line 1
    "Cannot alter the login '*Domain\Group*', because it does not exist or you do not have permission."`

    This is by design.
  
Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessários para autenticar uma conexão e as regras de firewall no nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).

## <a name="permissions"></a>Permissões

Requer a permissão ALTER ANY LOGIN.

Se a opção CREDENTIAL for usada, também será necessária a permissão ALTER ANY CREDENTIAL.

Se o logon sendo alterado for membro da função de servidor fixa **sysadmin** ou tiver a permissão CONTROL SERVER, a permissão CONTROL SERVER também será exigida quando as seguintes alterações forem efetuadas:

- Redefinição de senha sem fornecimento da senha antiga.
- Ativação de MUST_CHANGE, CHECK_POLICY ou CHECK_EXPIRATION.
- Alteração do nome de logon.
- Habilitação ou desabilitação do logon.
- Mapeamento do logon para uma credencial diferente.

Um administrador pode alterar a senha, o idioma padrão e o banco de dados padrão do seu próprio logon.

## <a name="examples"></a>Exemplos

### <a name="a-enabling-a-disabled-login"></a>a. Habilitando um logon desabilitado

O exemplo seguinte ativa o logon `Mary5`.

```sql
ALTER LOGIN Mary5 ENABLE;
```

### <a name="b-changing-the-password-of-a-login"></a>B. Alterando a senha de um logon

O exemplo seguinte altera a senha de logon `Mary5` para uma senha forte.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';
```

### <a name="c-changing-the-password-of-a-login-when-logged-in-as-the-login"></a>C. Alterar a senha de um logon quando conectado como o logon

Se você estiver tentando alterar a senha do logon ao qual está conectado no momento e não tiver a permissão `ALTER ANY LOGIN`, especifique a opção `OLD_PASSWORD`.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>' OLD_PASSWORD = '<oldWeakPasswordHere>';
```

### <a name="d-changing-the-name-of-a-login"></a>D. Alterando o nome de um logon

O exemplo seguinte altera o nome de logon `Mary5` para `John2`.

```sql
ALTER LOGIN Mary5 WITH NAME = John2;
```

### <a name="e-mapping-a-login-to-a-credential"></a>E. Mapeando um logon para uma credencial

O exemplo seguinte mapeia o logon `John2` para a credencial `Custodian04`.

```sql
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;
```

### <a name="f-mapping-a-login-to-an-extensible-key-management-credential"></a>F. Mapeando um logon para uma credencial de Gerenciamento Extensível de Chaves

O exemplo seguinte mapeia o logon `Mary5` para a credencial de EKM `EKMProvider1`.

```sql
ALTER LOGIN Mary5
ADD CREDENTIAL EKMProvider1;
GO
```

### <a name="f-unlocking-a-login"></a>F. Desbloqueando um logon

Para desbloquear um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute a seguinte instrução, substituindo \*\*\*\* pela senha da conta desejada.

```sql
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;

GO
```

Para desbloquear um logon sem alterar a senha, desative a política de verificação e ative-a novamente.

```sql
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;
GO
```

### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. Alterando a senha de um logon usando HASHED

O exemplo seguinte altera a senha do logon `TestUser` para um valor em que o hash já foi aplicado.

```sql
ALTER LOGIN TestUser WITH
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;
GO
```

## <a name="see-also"></a>Consulte Também

- [Credenciais](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [CREATE CREDENTIAL](../../t-sql/statements/create-credential-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [EKM (Gerenciamento extensível de chaves)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)

::: moniker-end
::: moniker range="=azuresqldb-current||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-login-transact-sql.md?view=sql-server-2017)|**_\* Banco de dados individual/pool elástico<br />do Banco de Dados SQL \*_**|[Instância gerenciada<br />do Banco de Dados SQL](alter-login-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](alter-login-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System (PDW)](alter-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-single-databaseelastic-pool"></a>Banco de dados individual/pool elástico do Banco de Dados SQL do Azure

## <a name="sql-server"></a>SQL Server

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for Azure SQL Database

ALTER LOGIN login_name
  {
      <status_option>
    | WITH <set_option> [ ,.. .n ]
  }
[;]

<status_option> ::=
    ENABLE | DISABLE

<set_option> ::=
    PASSWORD ='password'
    [
      OLD_PASSWORD ='oldpassword'
    ]
    | NAME = login_name
```

## <a name="arguments"></a>Argumentos

*login_name* Especifica o nome do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo alterado. Logons no domínio devem ser colocados entre colchetes no formato [domínio\usuário].

ENABLE | DISABLE Habilita ou desabilita este logon. Desabilitar um logon não afeta o comportamento de logons que já estão conectados. (Use a instrução `KILL` para encerrar as conexões existentes.) Os logons desabilitados retêm suas permissões e ainda podem ser representados.

PASSWORD **='** _password_ **'** Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica a senha do logon que está sendo alterado. As senhas diferenciam maiúsculas de minúsculas.

Conexões continuamente ativas para banco de dados SQL exigem nova autorização (executada pelo mecanismo de banco de dados) pelo menos a cada 10 horas. O Mecanismo de Banco de Dados tenta a nova autorização usando a senha enviada originalmente e não é necessária nenhuma entrada do usuário. Por motivos de desempenho, quando uma senha for redefinida no Banco de Dados SQL, a conexão não será autenticada novamente, mesmo que ela seja redefinida devido ao pool de conexões. Isso é diferente do comportamento do SQL Server local. Se a senha for alterada depois que a conexão for autorizada inicialmente, a conexão precisará ser terminada e uma nova conexão deverá ser feita usando a nova senha. Um usuário com a permissão KILL DATABASE CONNECTION pode terminar explicitamente uma conexão com o Banco de Dados SQL usando o comando KILL. Para obter mais informações, consulte [KILL](../../t-sql/language-elements/kill-transact-sql.md).

> [!IMPORTANT]
> Quando um logon (ou um usuário de banco de dados independente) se conecta e é autenticado, a conexão armazena em cache as informações de identidade sobre o logon. Para um logon de Autenticação do Windows, isso inclui informações sobre a associação em grupos do Windows. A identidade do logon permanece autenticada desde que a conexão seja mantida. Para forçar alterações na identidade, como uma redefinição de senha ou alteração na associação de grupo do Windows, o logon deve fazer logoff da autoridade de autenticação (Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) e fazer logon novamente. Um membro da função de servidor fixa ou **sysadmin** ou qualquer logon com a permissão **ALTER ANY CONNECTION** pode usar o comando **KILL** para terminar uma conexão e forçar um logon para reconectar. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] pode reutilizar informações de conexão ao abrir várias conexões para as janelas do Pesquisador de Objetos e do Editor de Consultas. Feche todas as conexões para forçar a reconexão.

OLD_PASSWORD **='** _oldpassword_ **'** Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A senha atual do logon a que uma senha nova será atribuída. As senhas diferenciam maiúsculas de minúsculas.

NAME = *login_name* O nome novo do logon que está sendo renomeado. Se este for um logon do Windows, o SID do administrador do Windows correspondente ao novo nome deverá corresponder ao SID associado ao logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O nome novo de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode conter um caractere de barra invertida (\\).

## <a name="remarks"></a>Comentários

Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessários para autenticar uma conexão e as regras de firewall no nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).

## <a name="permissions"></a>Permissões

Requer a permissão ALTER ANY LOGIN.

Se o logon sendo alterado for membro da função de servidor fixa **sysadmin** ou tiver a permissão CONTROL SERVER, a permissão CONTROL SERVER também será exigida quando as seguintes alterações forem efetuadas:

- Redefinição de senha sem fornecimento da senha antiga.
- Alteração do nome de logon.
- Habilitação ou desabilitação do logon.
- Mapeamento do logon para uma credencial diferente.

Uma entidade de segurança pode alterar a senha do seu próprio logon.

## <a name="examples"></a>Exemplos

Esses exemplos também incluem exemplos de uso de outros produtos SQL. Confira quais argumentos são compatíveis acima.

### <a name="a-enabling-a-disabled-login"></a>a. Habilitando um logon desabilitado

O exemplo seguinte ativa o logon `Mary5`.

```sql
ALTER LOGIN Mary5 ENABLE;
```

### <a name="b-changing-the-password-of-a-login"></a>B. Alterando a senha de um logon

O exemplo seguinte altera a senha de logon `Mary5` para uma senha forte.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';
```

### <a name="c-changing-the-name-of-a-login"></a>C. Alterando o nome de um logon

O exemplo seguinte altera o nome de logon `Mary5` para `John2`.

```sql
ALTER LOGIN Mary5 WITH NAME = John2;
```

### <a name="d-mapping-a-login-to-a-credential"></a>D. Mapeando um logon para uma credencial

O exemplo seguinte mapeia o logon `John2` para a credencial `Custodian04`.

```sql
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;
```

### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. Mapeando um logon para uma credencial de Gerenciamento Extensível de Chaves

O exemplo seguinte mapeia o logon `Mary5` para a credencial de EKM `EKMProvider1`.


**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
ALTER LOGIN Mary5
ADD CREDENTIAL EKMProvider1;
GO
```

### <a name="f-unlocking-a-login"></a>F. Desbloqueando um logon

Para desbloquear um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute a seguinte instrução, substituindo \*\*\*\* pela senha da conta desejada.

```sql
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;

GO
```

Para desbloquear um logon sem alterar a senha, desative a política de verificação e ative-a novamente.

```sql
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;
GO
```

### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. Alterando a senha de um logon usando HASHED

O exemplo seguinte altera a senha do logon `TestUser` para um valor em que o hash já foi aplicado.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
ALTER LOGIN TestUser WITH
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;
GO
```

## <a name="see-also"></a>Consulte Também

- [Credenciais](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [CREATE CREDENTIAL](../../t-sql/statements/create-credential-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [EKM (Gerenciamento extensível de chaves)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)

::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-login-transact-sql.md?view=sql-server-2017)|[Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-login-transact-sql.md?view=azuresqldb-current)|**_\* Instância gerenciada<br />do Banco de Dados SQL \*_**|[Azure Synapse<br />Analytics](alter-login-transact-sql.md?view=azure-sqldw-latest)|[Analytics Platform<br />System (PDW)](alter-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-sql-database-managed-instance"></a>Instância gerenciada do Banco de Dados SQL do Azure

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for SQL Server and Azure SQL Database managed instance

ALTER LOGIN login_name
    {
    <status_option>
    | WITH <set_option> [ ,... ]
    | <cryptographic_credential_option>
    }
[;]

<status_option> ::=
        ENABLE | DISABLE
  
<set_option> ::=
    PASSWORD = 'password' | hashed_password HASHED
    [
      OLD_PASSWORD = 'oldpassword'
      | <password_option> [<password_option> ]
    ]
    | DEFAULT_DATABASE = database
    | DEFAULT_LANGUAGE = language
    | NAME = login_name
    | CHECK_POLICY = { ON | OFF }
    | CHECK_EXPIRATION = { ON | OFF }
    | CREDENTIAL = credential_name
    | NO CREDENTIAL

<password_option> ::=
    MUST_CHANGE | UNLOCK

<cryptographic_credentials_option> ::=
    ADD CREDENTIAL credential_name
  | DROP CREDENTIAL credential_name
```

> [!NOTE]
> A funcionalidade de administrador do Azure AD para a instância gerenciada depois que a criação foi alterada. Para obter mais informações, confira [Nova funcionalidade de administrador do Azure AD para MI](/azure/sql-database/sql-database-aad-authentication-configure#new-azure-ad-admin-functionality-for-mi).

```syntaxsql
-- Syntax for Azure SQL Database managed instance using Azure AD logins

ALTER LOGIN login_name
  {
      <status_option>
    | WITH <set_option> [ ,.. .n ]
  }
[;]

<status_option> ::=
    ENABLE | DISABLE

<set_option> ::=
     DEFAULT_DATABASE = database
   | DEFAULT_LANGUAGE = language
```

## <a name="arguments"></a>Argumentos

### <a name="arguments-applicable-to-sql-and-azure-ad-logins"></a>Argumentos aplicáveis aos logons do SQL e do Azure AD

*login_name* Especifica o nome do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo alterado. Os logons do Azure AD precisam ser especificados como user@domain. Por exemplo, john.smith@contoso.com ou como o nome do grupo ou do aplicativo do Azure AD. Para logons do Azure AD, o *login_name* precisa corresponder a um logon existente do Azure AD criado no banco de dados mestre.

ENABLE | DISABLE Habilita ou desabilita este logon. Desabilitar um logon não afeta o comportamento de logons que já estão conectados. (Use a instrução `KILL` para encerrar uma conexão existente.) Os logons desabilitados retêm suas permissões e ainda podem ser representados.

DEFAULT_DATABASE **=** _database_ Especifica um banco de dados padrão a ser atribuído ao logon.

DEFAULT_LANGUAGE **=** _language_ Especifica um idioma padrão a ser atribuído ao logon. O idioma padrão para todos os logons de Banco de Dados SQL é o inglês e não pode ser alterado. O idioma padrão do logon `sa` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em Linux, é o inglês, mas pode ser alterado.

### <a name="arguments-applicable-only-to-sql-logins"></a>Argumentos aplicáveis somente a logons do SQL Server

PASSWORD **='** _password_ **'** Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica a senha do logon que está sendo alterado. As senhas diferenciam maiúsculas de minúsculas. As senhas também não se aplicam quando usado com logons externos, como logons do Azure AD.

Conexões continuamente ativas para banco de dados SQL exigem nova autorização (executada pelo mecanismo de banco de dados) pelo menos a cada 10 horas. O Mecanismo de Banco de Dados tenta a nova autorização usando a senha enviada originalmente e não é necessária nenhuma entrada do usuário. Por motivos de desempenho, quando uma senha for redefinida no Banco de Dados SQL, a conexão não será autenticada novamente, mesmo que ela seja redefinida devido ao pool de conexões. Isso é diferente do comportamento do SQL Server local. Se a senha for alterada depois que a conexão for autorizada inicialmente, a conexão precisará ser terminada e uma nova conexão deverá ser feita usando a nova senha. Um usuário com a permissão KILL DATABASE CONNECTION pode terminar explicitamente uma conexão com o Banco de Dados SQL usando o comando KILL. Para obter mais informações, consulte [KILL](../../t-sql/language-elements/kill-transact-sql.md).

PASSWORD **=** _hashed\_password_ Aplica-se somente à palavra-chave HASHED. Especifica o valor com hash da senha para o logon que está sendo criado.

HASHED Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica que a senha digitada depois do argumento PASSWORD já esteja com hash. Se esta opção não for selecionada, a senha terá hash antes de ser armazenada no banco de dados. Essa opção deve ser usada somente para sincronização de logon entre dois servidores. Não use a opção HASHED para alterar senhas rotineiramente.

OLD_PASSWORD **='** _oldpassword_ **'** Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A senha atual do logon a que uma senha nova será atribuída. As senhas diferenciam maiúsculas de minúsculas.

MUST_CHANGE<br>
Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esta opção estiver incluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicitará uma senha atualizada quando o logon alterado for usado pela primeira vez.

NAME = *login_name* O nome novo do logon que está sendo renomeado. No caso de logon do Windows, o SID da entidade de segurança do Windows correspondente ao novo nome precisará corresponder ao SID associado ao logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O nome novo de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode conter um caractere de barra invertida (\\).

CHECK_EXPIRATION = { ON | **OFF** } Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica se a política de expiração de senha deve ser aplicada neste logon. O valor padrão é OFF.

CHECK_POLICY **=** { **ON** | OFF } somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica se as políticas de senha do Windows do computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução devem ser aplicadas neste logon. O valor padrão é ON.

CREDENTIAL = *credential_name* O nome de uma credencial a ser mapeada para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A credencial já deve existir no servidor. Para obter mais informações, consulte [Credenciais](../../relational-databases/security/authentication-access/credentials-database-engine.md). Não é possível mapear uma credencial para logon do sa.

NO CREDENTIAL Remove qualquer mapeamento existente do logon para uma credencial de servidor. Para obter mais informações, consulte [Credenciais](../../relational-databases/security/authentication-access/credentials-database-engine.md).

UNLOCK Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica que um logon bloqueado deve ser desbloqueado.

ADD CREDENTIAL Adiciona uma credencial do provedor EKM (Gerenciamento de chave extensível) ao logon. Para obter mais informações, consulte [EKM (Gerenciamento extensível de chaves)](../../relational-databases/security/encryption/extensible-key-management-ekm.md).

DROP CREDENTIAL Remove uma credencial do provedor de EKM (Gerenciamento de chave extensível) do logon. Para obter mais informações, consulte [EKM (Gerenciamento extensível de chaves)](../../relational-databases/security/encryption/extensible-key-management-ekm.md).

## <a name="remarks"></a>Comentários

Quando CHECK_POLICY estiver definido como ON, o argumento HASHED não poderá ser usado.

Quando CHECK_POLICY for alterado para ON, o seguinte comportamento ocorrerá:

- O histórico de senhas é inicializado com o valor do hash da senha atual.

  Quando CHECK_POLICY for alterado para OFF, o seguinte comportamento ocorrerá:

- CHECK_EXPIRATION também será definido como OFF.
- O histórico de senhas será apagado.
- O valor de *lockout_time* é redefinido.

Se MUST_CHANGE for especificado, CHECK_EXPIRATION e CHECK_POLICY deverão ser definidos como ON. Caso contrário, a instrução falhará.

Se CHECK_POLICY for definido como OFF, CHECK_EXPIRATION não poderá ser definido como ON. Uma instrução ALTER LOGON com essa combinação de opções falhará.

Você não pode usar ALTER_LOGIN com o argumento DISABLE para negar acesso a um grupo do Windows. Isso ocorre por design. Por exemplo, ALTER_LOGIN [*domain\group*] DISABLE retornará a seguinte mensagem de erro:

    `"Msg 15151, Level 16, State 1, Line 1
    "Cannot alter the login '*Domain\Group*', because it does not exist or you do not have permission."`

Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessários para autenticar uma conexão e as regras de firewall no nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).

## <a name="permissions"></a>Permissões

Requer a permissão ALTER ANY LOGIN.

Se a opção CREDENTIAL for usada, também será necessária a permissão ALTER ANY CREDENTIAL.

Se o logon sendo alterado for membro da função de servidor fixa **sysadmin** ou tiver a permissão CONTROL SERVER, a permissão CONTROL SERVER também será exigida quando as seguintes alterações forem efetuadas:

- Redefinição de senha sem fornecimento da senha antiga.
- Ativação de MUST_CHANGE, CHECK_POLICY ou CHECK_EXPIRATION.
- Alteração do nome de logon.
- Habilitação ou desabilitação do logon.
- Mapeamento do logon para uma credencial diferente.

Um administrador pode alterar a senha, o idioma padrão e o banco de dados padrão do seu próprio logon.

Apenas uma entidade de segurança do SQL com privilégios `sysadmin` pode executar um comando ALTER LOGIN em um logon do Azure AD.

## <a name="examples"></a>Exemplos

Esses exemplos também incluem exemplos de uso de outros produtos SQL. Confira quais argumentos são compatíveis acima.

### <a name="a-enabling-a-disabled-login"></a>a. Habilitando um logon desabilitado

O exemplo seguinte ativa o logon `Mary5`.

```sql
ALTER LOGIN Mary5 ENABLE;
```

### <a name="b-changing-the-password-of-a-login"></a>B. Alterando a senha de um logon

O exemplo seguinte altera a senha de logon `Mary5` para uma senha forte.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';
```

### <a name="c-changing-the-name-of-a-login"></a>C. Alterando o nome de um logon

O exemplo seguinte altera o nome de logon `Mary5` para `John2`.

```sql
ALTER LOGIN Mary5 WITH NAME = John2;
```

### <a name="d-mapping-a-login-to-a-credential"></a>D. Mapeando um logon para uma credencial

O exemplo seguinte mapeia o logon `John2` para a credencial `Custodian04`.

```sql
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;
```

### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. Mapeando um logon para uma credencial de Gerenciamento Extensível de Chaves

O exemplo seguinte mapeia o logon `Mary5` para a credencial de EKM `EKMProvider1`.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior e à Instância Gerenciada do Banco de Dados SQL do Azure.

```sql
ALTER LOGIN Mary5
ADD CREDENTIAL EKMProvider1;
GO
```

### <a name="f-unlocking-a-login"></a>F. Desbloqueando um logon

Para desbloquear um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute a seguinte instrução, substituindo \*\*\*\* pela senha da conta desejada.

```sql
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;

GO
```

Para desbloquear um logon sem alterar a senha, desative a política de verificação e ative-a novamente.

```sql
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;
GO
```

### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. Alterando a senha de um logon usando HASHED

O exemplo seguinte altera a senha do logon `TestUser` para um valor em que o hash já foi aplicado.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior e à Instância Gerenciada do Banco de Dados SQL do Azure.

```sql
ALTER LOGIN TestUser WITH
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;
GO
```

### <a name="h-disabling-the-login-of-an-azure-ad-user"></a>H. Desabilitando o logon de um usuário do Azure AD

O exemplo a seguir desabilita o logon de um usuário do Azure AD, joe@contoso.com.

```sql
ALTER LOGIN [joe@contoso.com] DISABLE
```

## <a name="see-also"></a>Consulte Também

- [Credenciais](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [CREATE CREDENTIAL](../../t-sql/statements/create-credential-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [EKM (Gerenciamento extensível de chaves)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)

::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-login-transact-sql.md?view=sql-server-2017)|[Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-login-transact-sql.md?view=azuresqldb-current)|[Instância gerenciada<br />do Banco de Dados SQL](alter-login-transact-sql.md?view=azuresqldb-mi-current)|**_\* Azure Synapse<br />Analytics \*_**|[Analytics Platform<br />System (PDW)](alter-login-transact-sql.md?view=aps-pdw-2016)

&nbsp;

## <a name="azure-synapse-analytics"></a>Azure Synapse Analytics

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for Azure Synapse

ALTER LOGIN login_name
  {
      <status_option>
    | WITH <set_option> [ ,.. .n ]
  }
[;]

<status_option> ::=
    ENABLE | DISABLE
  
<set_option> ::=
    PASSWORD ='password'
    [
      OLD_PASSWORD ='oldpassword'
    ]
    | NAME = login_name
```

## <a name="arguments"></a>Argumentos

*login_name* Especifica o nome do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo alterado. Logons no domínio devem ser colocados entre colchetes no formato [domínio\usuário].

ENABLE | DISABLE Habilita ou desabilita este logon. Desabilitar um logon não afeta o comportamento de logons que já estão conectados. (Use a instrução `KILL` para encerrar as conexões existentes.) Os logons desabilitados retêm suas permissões e ainda podem ser representados.

PASSWORD **='** _password_ **'** Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica a senha do logon que está sendo alterado. As senhas diferenciam maiúsculas de minúsculas.

Conexões continuamente ativas para banco de dados SQL exigem nova autorização (executada pelo mecanismo de banco de dados) pelo menos a cada 10 horas. O Mecanismo de Banco de Dados tenta a nova autorização usando a senha enviada originalmente e não é necessária nenhuma entrada do usuário. Por motivos de desempenho, quando uma senha for redefinida no Banco de Dados SQL, a conexão não será autenticada novamente, mesmo que ela seja redefinida devido ao pool de conexões. Isso é diferente do comportamento do SQL Server local. Se a senha for alterada depois que a conexão for autorizada inicialmente, a conexão precisará ser terminada e uma nova conexão deverá ser feita usando a nova senha. Um usuário com a permissão KILL DATABASE CONNECTION pode terminar explicitamente uma conexão com o Banco de Dados SQL usando o comando KILL. Para obter mais informações, consulte [KILL](../../t-sql/language-elements/kill-transact-sql.md).

> [!IMPORTANT]
> Quando um logon (ou um usuário de banco de dados independente) se conecta e é autenticado, a conexão armazena em cache as informações de identidade sobre o logon. Para um logon de Autenticação do Windows, isso inclui informações sobre a associação em grupos do Windows. A identidade do logon permanece autenticada desde que a conexão seja mantida. Para forçar alterações na identidade, como uma redefinição de senha ou alteração na associação de grupo do Windows, o logon deve fazer logoff da autoridade de autenticação (Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) e fazer logon novamente. Um membro da função de servidor fixa ou **sysadmin** ou qualquer logon com a permissão **ALTER ANY CONNECTION** pode usar o comando **KILL** para terminar uma conexão e forçar um logon para reconectar. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] pode reutilizar informações de conexão ao abrir várias conexões para as janelas do Pesquisador de Objetos e do Editor de Consultas. Feche todas as conexões para forçar a reconexão.

OLD_PASSWORD **='** _oldpassword_ **'** Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A senha atual do logon a que uma senha nova será atribuída. As senhas diferenciam maiúsculas de minúsculas.

NAME = *login_name* O nome novo do logon que está sendo renomeado. Se este for um logon do Windows, o SID do administrador do Windows correspondente ao novo nome deverá corresponder ao SID associado ao logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O nome novo de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode conter um caractere de barra invertida (\\).

## <a name="remarks"></a>Comentários

Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessários para autenticar uma conexão e as regras de firewall no nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).

## <a name="permissions"></a>Permissões

Requer a permissão ALTER ANY LOGIN.

Se o logon sendo alterado for membro da função de servidor fixa **sysadmin** ou tiver a permissão CONTROL SERVER, a permissão CONTROL SERVER também será exigida quando as seguintes alterações forem efetuadas:

- Redefinição de senha sem fornecimento da senha antiga.
- Alteração do nome de logon.
- Habilitação ou desabilitação do logon.
- Mapeamento do logon para uma credencial diferente.

Uma entidade de segurança pode alterar a senha do seu próprio logon.

## <a name="examples"></a>Exemplos

Esses exemplos também incluem exemplos de uso de outros produtos SQL. Confira quais argumentos são compatíveis acima.

### <a name="a-enabling-a-disabled-login"></a>a. Habilitando um logon desabilitado

O exemplo seguinte ativa o logon `Mary5`.

```sql
ALTER LOGIN Mary5 ENABLE;
```

### <a name="b-changing-the-password-of-a-login"></a>B. Alterando a senha de um logon

O exemplo seguinte altera a senha de logon `Mary5` para uma senha forte.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';
```

### <a name="c-changing-the-name-of-a-login"></a>C. Alterando o nome de um logon

O exemplo seguinte altera o nome de logon `Mary5` para `John2`.

```sql
ALTER LOGIN Mary5 WITH NAME = John2;
```

### <a name="d-mapping-a-login-to-a-credential"></a>D. Mapeando um logon para uma credencial

O exemplo seguinte mapeia o logon `John2` para a credencial `Custodian04`.

```sql
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;
```

### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. Mapeando um logon para uma credencial de Gerenciamento Extensível de Chaves

O exemplo seguinte mapeia o logon `Mary5` para a credencial de EKM `EKMProvider1`.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
ALTER LOGIN Mary5
ADD CREDENTIAL EKMProvider1;
GO
```

### <a name="f-unlocking-a-login"></a>F. Desbloqueando um logon

Para desbloquear um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute a seguinte instrução, substituindo \*\*\*\* pela senha da conta desejada.

```sql
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;

GO
```

Para desbloquear um logon sem alterar a senha, desative a política de verificação e ative-a novamente.

```sql
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;
GO
```

### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. Alterando a senha de um logon usando HASHED

O exemplo seguinte altera a senha do logon `TestUser` para um valor em que o hash já foi aplicado.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
ALTER LOGIN TestUser WITH
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;
GO
```

## <a name="see-also"></a>Consulte Também

- [Credenciais](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [CREATE CREDENTIAL](../../t-sql/statements/create-credential-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [EKM (Gerenciamento extensível de chaves)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)

::: moniker-end
::: moniker range=">=aps-pdw-2016||=sqlallproducts-allversions"

> ||||||
> |-|-|-|-|-|
> |[SQL Server](alter-login-transact-sql.md?view=sql-server-2017)|[Banco de dados individual/pool elástico<br />do Banco de Dados SQL](alter-login-transact-sql.md?view=azuresqldb-current)|[Instância gerenciada<br />do Banco de Dados SQL](alter-login-transact-sql.md?view=azuresqldb-mi-current)|[Azure Synapse<br />Analytics](alter-login-transact-sql.md?view=azure-sqldw-latest)|**_\* Analytics<br />Platform System (PDW) \*_**

&nbsp;

## <a name="analytics-platform-system"></a>Sistema de plataforma de análise

## <a name="syntax"></a>Sintaxe

```syntaxsql
-- Syntax for Analytics Platform System

ALTER LOGIN login_name
    {
    <status_option>
    | WITH <set_option> [ ,... ]
    }

<status_option> ::=ENABLE | DISABLE

<set_option> ::=
    PASSWORD ='password'
    [
      OLD_PASSWORD ='oldpassword'
      | <password_option> [<password_option> ]
    ]
    | NAME = login_name
    | CHECK_POLICY = { ON | OFF }
    | CHECK_EXPIRATION = { ON | OFF }

<password_option> ::=
    MUST_CHANGE | UNLOCK
```

## <a name="arguments"></a>Argumentos

*login_name* Especifica o nome do logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo alterado. Logons no domínio devem ser colocados entre colchetes no formato [domínio\usuário].

ENABLE | DISABLE Habilita ou desabilita este logon. Desabilitar um logon não afeta o comportamento de logons que já estão conectados. (Use a instrução `KILL` para encerrar uma conexão existente.) Os logons desabilitados retêm suas permissões e ainda podem ser representados.

PASSWORD **='** _password_ **'** Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica a senha do logon que está sendo alterado. As senhas diferenciam maiúsculas de minúsculas.

> [!IMPORTANT]
> Quando um logon (ou um usuário de banco de dados independente) se conecta e é autenticado, a conexão armazena em cache as informações de identidade sobre o logon. Para um logon de Autenticação do Windows, isso inclui informações sobre a associação em grupos do Windows. A identidade do logon permanece autenticada desde que a conexão seja mantida. Para forçar alterações na identidade, como uma redefinição de senha ou alteração na associação de grupo do Windows, o logon deve fazer logoff da autoridade de autenticação (Windows ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) e fazer logon novamente. Um membro da função de servidor fixa ou **sysadmin** ou qualquer logon com a permissão **ALTER ANY CONNECTION** pode usar o comando **KILL** para terminar uma conexão e forçar um logon para reconectar. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] pode reutilizar informações de conexão ao abrir várias conexões para as janelas do Pesquisador de Objetos e do Editor de Consultas. Feche todas as conexões para forçar a reconexão.

OLD_PASSWORD **='** _oldpassword_ **'** Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A senha atual do logon a que uma senha nova será atribuída. As senhas diferenciam maiúsculas de minúsculas.

MUST_CHANGE Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se esta opção estiver incluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solicitará uma senha atualizada quando o logon alterado for usado pela primeira vez.

NAME = *login_name* O nome novo do logon que está sendo renomeado. No caso de logon do Windows, o SID da entidade de segurança do Windows correspondente ao novo nome precisará corresponder ao SID associado ao logon no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O nome novo de um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode conter um caractere de barra invertida (\\).

CHECK_EXPIRATION = { ON | **OFF** } Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica se a política de expiração de senha deve ser aplicada neste logon. O valor padrão é OFF.

CHECK_POLICY **=** { **ON** | OFF } somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica se as políticas de senha do Windows do computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução devem ser aplicadas neste logon. O valor padrão é ON.

UNLOCK Aplica-se somente a logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Especifica que um logon bloqueado deve ser desbloqueado.

## <a name="remarks"></a>Comentários

Quando CHECK_POLICY estiver definido como ON, o argumento HASHED não poderá ser usado.

Quando CHECK_POLICY for alterado para ON, o seguinte comportamento ocorrerá:

- O histórico de senhas é inicializado com o valor do hash da senha atual.

  Quando CHECK_POLICY for alterado para OFF, o seguinte comportamento ocorrerá:

- CHECK_EXPIRATION também será definido como OFF.
- O histórico de senhas será apagado.
- O valor de *lockout_time* é redefinido.

Se MUST_CHANGE for especificado, CHECK_EXPIRATION e CHECK_POLICY deverão ser definidos como ON. Caso contrário, a instrução falhará.

Se CHECK_POLICY for definido como OFF, CHECK_EXPIRATION não poderá ser definido como ON. Uma instrução ALTER LOGON com essa combinação de opções falhará.

Você não pode usar ALTER_LOGIN com o argumento DISABLE para negar acesso a um grupo do Windows. Isso ocorre por design. Por exemplo, ALTER_LOGIN [*domain\group*] DISABLE retornará a seguinte mensagem de erro:

    `"Msg 15151, Level 16, State 1, Line 1
    "Cannot alter the login '*Domain\Group*', because it does not exist or you do not have permission."`

Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], dados de logon necessários para autenticar uma conexão e as regras de firewall no nível de servidor são armazenados em cache temporariamente em cada banco de dados. Esse cache é atualizado periodicamente. Para forçar uma atualização do cache de autenticação e garantir que um banco de dados tenha a versão mais recente da tabela de logons, execute [DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).

## <a name="permissions"></a>Permissões

Requer a permissão ALTER ANY LOGIN.

Se a opção CREDENTIAL for usada, também será necessária a permissão ALTER ANY CREDENTIAL.

Se o logon sendo alterado for membro da função de servidor fixa **sysadmin** ou tiver a permissão CONTROL SERVER, a permissão CONTROL SERVER também será exigida quando as seguintes alterações forem efetuadas:

- Redefinição de senha sem fornecimento da senha antiga.
- Ativação de MUST_CHANGE, CHECK_POLICY ou CHECK_EXPIRATION.
- Alteração do nome de logon.
- Habilitação ou desabilitação do logon.
- Mapeamento do logon para uma credencial diferente.

Um administrador pode alterar a senha, o idioma padrão e o banco de dados padrão do seu próprio logon.

## <a name="examples"></a>Exemplos

Esses exemplos também incluem exemplos de uso de outros produtos SQL. Confira quais argumentos são compatíveis acima.

### <a name="a-enabling-a-disabled-login"></a>a. Habilitando um logon desabilitado

O exemplo seguinte ativa o logon `Mary5`.

```sql
ALTER LOGIN Mary5 ENABLE;
```

### <a name="b-changing-the-password-of-a-login"></a>B. Alterando a senha de um logon

O exemplo seguinte altera a senha de logon `Mary5` para uma senha forte.

```sql
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';
```

### <a name="c-changing-the-name-of-a-login"></a>C. Alterando o nome de um logon

O exemplo seguinte altera o nome de logon `Mary5` para `John2`.

```sql
ALTER LOGIN Mary5 WITH NAME = John2;
```

### <a name="d-mapping-a-login-to-a-credential"></a>D. Mapeando um logon para uma credencial

O exemplo seguinte mapeia o logon `John2` para a credencial `Custodian04`.

```sql
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;
```

### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. Mapeando um logon para uma credencial de Gerenciamento Extensível de Chaves

O exemplo seguinte mapeia o logon `Mary5` para a credencial de EKM `EKMProvider1`.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
ALTER LOGIN Mary5
ADD CREDENTIAL EKMProvider1;
GO
```

### <a name="f-unlocking-a-login"></a>F. Desbloqueando um logon

Para desbloquear um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute a seguinte instrução, substituindo \*\*\*\* pela senha da conta desejada.

```sql
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;

GO
```

Para desbloquear um logon sem alterar a senha, desative a política de verificação e ative-a novamente.

```sql
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;
GO
```

### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. Alterando a senha de um logon usando HASHED

O exemplo seguinte altera a senha do logon `TestUser` para um valor em que o hash já foi aplicado.

**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.

```sql
ALTER LOGIN TestUser WITH
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;
GO
```

## <a name="see-also"></a>Consulte Também

- [Credenciais](../../relational-databases/security/authentication-access/credentials-database-engine.md)
- [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)
- [DROP LOGIN](../../t-sql/statements/drop-login-transact-sql.md)
- [CREATE CREDENTIAL](../../t-sql/statements/create-credential-transact-sql.md)
- [EVENTDATA](../../t-sql/functions/eventdata-transact-sql.md)
- [EKM (Gerenciamento extensível de chaves)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)

::: moniker-end
