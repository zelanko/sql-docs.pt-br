---
title: sp_migrate_user_to_contained (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/11/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_migrate_user_to_contained
- sp_migrate_user_to_contained_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_migrate_user_to_contained
ms.assetid: b3a49ff6-46ad-4ee7-b6fe-7e54213dc33e
author: stevestein
ms.author: sstein
ms.openlocfilehash: d5bcafb24313851f58fd18fc19ebabd0ee98f6dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022327"
---
# <a name="spmigrateusertocontained-transact-sql"></a>sp_migrate_user_to_contained (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Converte um usuário do banco de dados que foi mapeado para um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um usuário do banco de dados independente com senha. Em um banco de dados independente, use este procedimento para remover dependências na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] onde o banco de dados está instalado. **sp_migrate_user_to_contained** separa o usuário do original [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon, para que as configurações como senha e idioma padrão podem ser administradas separadamente para o banco de dados independente. **sp_migrate_user_to_contained** pode ser usado antes de mover o banco de dados independente para uma instância diferente de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] para eliminar dependências atual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logons da instância.  
  
> [!NOTE]
> Tenha cuidado ao usar **sp_migrate_user_to_contained**, pois você não poderá reverter o efeito. Este procedimento é usado somente em um banco de dados independente. Para obter mais informações, veja [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_migrate_user_to_contained [ @username = ] N'user' ,   
    [ @rename = ] { N'copy_login_name' | N'keep_name' } ,   
    [ @disablelogin = ] { N'disable_login' | N'do_not_disable_login' }   
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@username =** ] **N'***user***'**  
 Nome de um usuário do banco de dados independente atual que é mapeado para um logon autenticado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O valor será **sysname**, com um padrão de **nulo**.  
  
 [ **@rename =** ] **N'***copy_login_name***'**  | **N'***keep_name***'**  
 Quando um usuário de banco de dados com base em um logon tem um nome de usuário diferente do nome de logon, use *keep_name* para manter o nome de usuário de banco de dados durante a migração. Use *copy_login_name* para criar o novo usuário de banco de dados independente com o nome de logon, em vez do usuário. Quando um usuário de banco de dados baseado em um logon tem o mesmo nome de usuário do nome de logon, as duas opções criam o usuário do banco de dados independente, sem alterar o nome.  
  
 [ **@disablelogin =** ] **N'***disable_login***'**  | **N'***do_not_disable_login***'**  
 *disable_login* desabilita o logon no banco de dados mestre. Para se conectar quando o logon está desabilitado, a conexão deve fornecer o nome de banco de dados independente como o **catálogo inicial** como parte da cadeia de conexão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_migrate_user_to_contained** cria o usuário de banco de dados independente com senha, independentemente das propriedades ou permissões de logon. Por exemplo, o procedimento possa ser bem-sucedida se o logon está desabilitado ou se o usuário é negado a **CONNECT** permissão para o banco de dados.  
  
 **sp_migrate_user_to_contained** tem as seguintes restrições.  
  
-   O nome de usuário não pode existir no banco de dados.  
  
-   Usuários internos, como dbo e guest, não podem ser convertidos.  
  
-   O usuário não pode ser especificado a **EXECUTE AS** cláusula de um procedimento armazenado assinado.  
  
-   O usuário não pode possuir um procedimento armazenado que inclui o **EXECUTE AS OWNER** cláusula.  
  
-   **sp_migrate_user_to_contained** não pode ser usado em um banco de dados do sistema.  
  
## <a name="security"></a>Segurança  
 Ao migrar usuários, tenha cuidado para não desabilitar ou excluir todos os logons de administrador da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se todos os logons forem excluídos, consulte [conectar-se ao SQL Server ao sistema os administradores são bloqueados](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md).  
  
 Se o **BUILTIN\Administradores** logon estiver presente, os administradores podem se conectar iniciando a seu aplicativo usando o **executar como administrador** opção.  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão **CONTROL SERVER** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-migrating-a-single-user"></a>A. Migrando um único usuário  
 O exemplo a seguir migra um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominado `Barry` para um usuário de banco de dados independente com senha. O exemplo não altera o nome de usuário e mantém o logon como habilitado.  
  
```sql  
sp_migrate_user_to_contained   
@username = N'Barry',  
@rename = N'keep_name',  
@disablelogin = N'do_not_disable_login' ;  
  
```  
  
### <a name="b-migrating-all-database-users-with-logins-to-contained-database-users-without-logins"></a>B. Migrando todos os usuários do banco de dados com logons para usuários de bancos de dados independentes sem logons  
 O exemplo a seguir migra todos os usuários baseados em logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usuários de bancos de dados independentes com senhas. O exemplo exclui os logons que não estão habilitados. O exemplo deve ser executado no banco de dados independente.  
  
```sql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [Bancos de dados independentes](../../relational-databases/databases/contained-databases.md)  
  
  
