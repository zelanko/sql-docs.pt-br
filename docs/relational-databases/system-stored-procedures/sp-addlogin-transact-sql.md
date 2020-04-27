---
title: sp_addlogin (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlogin
- sp_addlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5868120af1e98c4b2f3be78f2cf7927df53b42d1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68072660"
---
# <a name="sp_addlogin-transact-sql"></a>sp_addlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um novo logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite a um usuário se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [Create login](../../t-sql/statements/create-login-transact-sql.md) .  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addlogin [ @loginame = ] 'login'   
    [ , [ @passwd = ] 'password' ]   
    [ , [ @defdb = ] 'database' ]   
    [ , [ @deflanguage = ] 'language' ]   
    [ , [ @sid = ] sid ]   
    [ , [ @encryptopt = ] 'encryption_option' ]   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @loginame= ] '*logon*'  
 É o nome do logon. o *logon* é **sysname**, sem padrão.  
  
 [ @passwd= ] '*senha*'  
 É a senha de logon. a *senha* é **sysname**, com um padrão de NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb= ] '*banco de dados*'  
 É o banco de dados padrão do logon (o banco de dados ao qual o logon foi conectado pela primeira vez após a conexão). o *banco de dados* é **sysname**, com um padrão de **Master**.  
  
 [ @deflanguage= ] '*idioma*'  
 É o idioma padrão do logon. o *idioma* é **sysname**, com um padrão de NULL. Se o *idioma* não for especificado, o *idioma* padrão do novo logon será definido como o idioma padrão atual do servidor.  
  
 [ @sid= ] '*Sid*'  
 É o número de identificação de segurança (SID). *Sid* é **varbinary (16)**, com um padrão de NULL. Se *Sid* for NULL, o sistema gerará um SID para o novo logon. Apesar do uso de um tipo de dados **varbinary** , valores diferentes de NULL devem ter exatamente 16 bytes de comprimento e ainda não devem existir. A especificação de *Sid* é útil, por exemplo, quando você está criando scripts [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou movendo logons de um servidor para outro e deseja que os logons tenham o mesmo SID em servidores diferentes.  
  
 [ @encryptopt= ] '*encryption_option*'  
 Especifica se a senha é passada como texto não criptografado ou como o hash da senha de texto não criptografado. Observe que não há nenhuma criptografia. A palavra "criptografia" é usada nesta discussão por causa de compatibilidade com versões anteriores. Se uma senha de texto não criptografado for passada, ocorrerá hash. O hash é armazenado. *encryption_option* é **varchar (20)** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|NULO|A senha é passada sem-criptografia. Esse é o padrão.|  
|**skip_encryption**|A senha já tem hash. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve armazenar o valor sem hash.|  
|**skip_encryption_old**|A senha foi fornecida com hash por uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve armazenar o valor sem hash. Essa opção só é fornecida com a finalidade de atualização.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem conter 1 a 128 caracteres, inclusive cartas, símbolos e números. Os logons não podem conter uma barra\\invertida (); ser um nome de logon reservado, por exemplo, SA ou público, ou já existe; ou ser nulo ou uma cadeia de caracteres`''`vazia ().  
  
 Se o nome de um banco de dados padrão for fornecido, não será possível conectar-se ao banco de dados especificado sem executar a instrução USE. No entanto, você não pode usar o banco de dados padrão até receber acesso a esse banco de dados pelo proprietário do banco de dados (usando [sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) ou [sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) ou [sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md).  
  
 O número de SID é um GUID que identificará o logon exclusivamente no servidor.  
  
 A alteração do idioma padrão de servidor não altera o idioma padrão de logons existentes. Para alterar o idioma padrão do servidor, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 Usar **skip_encryption** para suprimir o hash de senha será útil se a senha já estiver com hash quando o logon for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]adicionado ao. Se a senha tiver sido armazenada em hash por uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]versão anterior do, use **skip_encryption_old**.  
  
 sp_addlogin não pode ser executado em uma transação definida pelo usuário.  
  
 A tabela a seguir mostra vários procedimentos armazenados que são usados com sp_addlogin.  
  
|Procedimento armazenado|Descrição|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|Adiciona um usuário ou grupo do Windows.|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|Altera a senha de um usuário.|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|Altera o banco de dados padrão de um usuário.|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|Altera o idioma padrão de um usuário.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY LOGIN.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-sql-server-login"></a>a. Criação de um logon do SQL Server  
 O exemplo a seguir cria um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o usuário `Victoria`, com uma senha de `B1r12-36`, sem especificar um banco de dados padrão.  
  
```  
EXEC sp_addlogin 'Victoria', 'B1r12-36';  
GO  
```  
  
### <a name="b-creating-a-sql-server-login-that-has-a-default-database"></a>B. Criação de um logon do SQL Server que tem um banco de dados padrão  
 O exemplo a seguir cria um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o usuário `Albert`, com uma senha de `B5432-3M6` e um banco de dados padrão de `corporate`.  
  
```  
EXEC sp_addlogin 'Albert', 'B5432-3M6', 'corporate';  
GO  
```  
  
### <a name="c-creating-a-sql-server-login-that-has-a-different-default-language"></a>C. Criação de um logon do SQL Server que tem um idioma padrão diferente  
 O exemplo a seguir cria um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o usuário `TzTodorov`, com uma senha de `709hLKH7chjfwv`, um banco de dados padrão de `AdventureWorks2012` e um idioma padrão de `Bulgarian`.  
  
```  
EXEC sp_addlogin 'TzTodorov', '709hLKH7chjfwv', 'AdventureWorks2012', N'български'  
```  
  
### <a name="d-creating-a-sql-server-login-that-has-a-specific-sid"></a>D. Criação de um logon do SQL Server logon que tem um SID específico  
 O exemplo a seguir cria um logon de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o usuário `Michael`, com uma senha de `B548bmM%f6`, um banco de dados padrão de `AdventureWorks2012`, um idioma padrão de `us_english` e um SID de `0x0123456789ABCDEF0123456789ABCDEF`.  
  
```  
EXEC sp_addlogin 'Michael', 'B548bmM%f6', 'AdventureWorks2012', 'us_english', 0x0123456789ABCDEF0123456789ABCDEF  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CRIAR logon &#40;&#41;Transact-SQL](../../t-sql/statements/create-login-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droplogin](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpuser](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_revokelogin](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [&#41;&#40;Transact-SQL de xp_logininfo](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
