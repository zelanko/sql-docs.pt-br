---
title: sp_addlogin (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_addlogin
- sp_addlogin_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 09a8425f9c3d773af00a0418ff4430839c221d87
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spaddlogin-transact-sql"></a>sp_addlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cria um novo logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite a um usuário se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use [CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) em vez disso.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ @loginame=] '*login*'  
 É o nome do logon. *logon* é **sysname**, sem padrão.  
  
 [ @passwd=] '*senha*'  
 É a senha de logon. *senha* é **sysname**, com um padrão NULL.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb=] '*banco de dados*'  
 É o banco de dados padrão do logon (o banco de dados ao qual o logon foi conectado pela primeira vez após a conexão). *banco de dados* é **sysname**, com um padrão de **mestre**.  
  
 [ @deflanguage=] '*idioma*'  
 É o idioma padrão do logon. *idioma* é **sysname**, com um padrão NULL. Se *idioma* não for especificado, o padrão *idioma* do novo logon é definido como o idioma padrão atual do servidor.  
  
 [ @sid=] '*sid*'  
 É o número de identificação de segurança (SID). *SID* é **varbinary (16)**, com um padrão NULL. Se *sid* for NULL, o sistema gera um SID para o novo logon. Apesar do uso de um **varbinary** tipo de dados, valores diferentes de NULL devem ter exatamente 16 bytes de comprimento e não deve existir. Especificando *sid* é útil, por exemplo, quando você está criando scripts ou movendo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logons de um servidor para outro e você deseja que os logons tenham o mesmo SID em servidores diferentes.  
  
 [ @encryptopt=] '*encryption_option*'  
 Especifica se a senha é passada como texto não criptografado ou como o hash da senha de texto não criptografado. Observe que não há nenhuma criptografia. A palavra "criptografia" é usada nesta discussão por causa de compatibilidade com versões anteriores. Se uma senha de texto não criptografado for passada, ocorrerá hash. O hash é armazenado. *encryption_option* é **varchar (20)**, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|NULL|A senha é passada sem-criptografia. Esse é o padrão.|  
|**skip_encryption**|A senha já tem hash. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve armazenar o valor sem hash.|  
|**skip_encryption_old**|A senha foi fornecida com hash por uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve armazenar o valor sem hash. Essa opção só é fornecida com a finalidade de atualização.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem conter 1 a 128 caracteres, inclusive cartas, símbolos e números. Logons não podem conter uma barra invertida (\\); ser um nome de logon reservado, por exemplo, sa ou público, nem existirem; nem ser nulo ou uma cadeia de caracteres vazia (`''`).  
  
 Se o nome de um banco de dados padrão for fornecido, não será possível conectar-se ao banco de dados especificado sem executar a instrução USE. No entanto, você não pode usar o banco de dados padrão até que você terá acesso ao banco de dados pelo proprietário do banco de dados (usando [sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md) ou [sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) ou [sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md).  
  
 O número de SID é um GUID que identificará o logon exclusivamente no servidor.  
  
 A alteração do idioma padrão de servidor não altera o idioma padrão de logons existentes. Para alterar o idioma padrão do servidor, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
 Usando **skip_encryption** para suprimir a senha de hash é útil se a senha já tem hash quando o logon é adicionado a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se a senha foi hash por uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use **skip_encryption_old**.  
  
 sp_addlogin não pode ser executado em uma transação definida pelo usuário.  
  
 A tabela a seguir mostra vários procedimentos armazenados que são usados com sp_addlogin.  
  
|Procedimento armazenado|Description|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|Adiciona um usuário ou grupo do Windows.|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|Altera a senha de um usuário.|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|Altera o banco de dados padrão de um usuário.|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|Altera o idioma padrão de um usuário.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY LOGIN.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-sql-server-login"></a>A. Criação de um logon do SQL Server  
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
  
## <a name="see-also"></a>Consulte também  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_droplogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpuser &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [sp_revokelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
