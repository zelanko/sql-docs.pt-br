---
title: sp_setapprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/12/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_setapprole
- sp_setapprole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_setapprole
ms.assetid: cf0901c0-5f90-42d4-9d5b-8772c904062d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: de85505295ceff98f404b2ba4c1effe3946fdbe5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72304968"
---
# <a name="sp_setapprole-transact-sql"></a>sp_setapprole (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Ativa as permissões associadas a uma função de aplicativo no banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  

```sql
sp_setapprole [ @rolename = ] 'role',  
    [ @password = ] { encrypt N'password' }
      |  
        'password' [ , [ @encrypt = ] { 'none' | 'odbc' } ]  
        [ , [ @fCreateCookie = ] true | false ]  
    [ , [ @cookie = ] @cookie OUTPUT ]  
```

## <a name="arguments"></a>Argumentos

`[ @rolename = ] 'role'`É o nome da função de aplicativo definida no banco de dados atual. *role* é **sysname**, sem padrão. a *função* deve existir no banco de dados atual.  
  
`[ @password = ] { encrypt N'password' }`É a senha necessária para ativar a função de aplicativo. a *senha* é **sysname**, sem padrão. a *senha* pode ser ofuscada usando a função ODBC **Encrypt** . Quando você usa a função **Encrypt** , a senha deve ser convertida em uma cadeia de caracteres Unicode, colocando **N** antes da primeira aspa.  
  
 Não há suporte para a opção Encrypt em conexões que estão usando o **SqlClient**.  
  
> [!IMPORTANT]  
> A função ODBC **Encrypt** não fornece criptografia. Você não deve confiar nessa função para proteger senhas que são transmitidas pela rede. Se essas informações forem transmitidas por uma rede, use SSL ou IPSec.
  
 **@encrypt= ' nenhum '**  
 Especifica que nenhuma ofuscação deve ser usada. A senha é transmitida para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como texto sem-formatação. Esse é o padrão.  
  
 **@encrypt= ' ODBC '**  
 Especifica que o ODBC ofusca a senha usando a função de **criptografia** ODBC antes de enviar a senha para o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Isso pode ser especificado somente quando um cliente ODBC ou o provedor OLE DB para SQL Server for utilizado.  
  
`[ @fCreateCookie = ] true | false`Especifica se um cookie deve ser criado. **true** é convertido implicitamente em 1. **false** é convertido implicitamente em 0.  
  
`[ @cookie = ] @cookie OUTPUT`Especifica um parâmetro de saída para conter o cookie. O cookie será gerado somente se o valor de ** \@fCreateCookie** for **true**. **varbinary (8000)**  
  
> [!NOTE]  
> O parâmetro **OUTPUT** de cookie para **sp_setapprole** está documentado atualmente como **varbinary(8000)** , que tem o tamanho máximo correto. No entanto, a implementação atual retorna **varbinary(50)** . Os aplicativos devem continuar a reservar **varbinary (8000)** para que o aplicativo continue a funcionar corretamente se o tamanho de retorno do cookie aumentar em uma versão futura.
  
## <a name="return-code-values"></a>Valores do código de retorno

 0 (êxito) e 1 (falha)  
  
## <a name="remarks"></a>Comentários

 Depois que uma função de aplicativo é ativada usando **sp_setapprole**, a função permanece ativa até que o usuário seja desconectado do servidor ou execute **sp_unsetapprole**. **sp_setapprole** pode ser executado somente por instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] diretas. **sp_setapprole** não pode ser executado em outro procedimento armazenado ou em uma transação definida pelo usuário.  
  
 Para obter uma visão geral das funções de aplicativo, consulte [funções de aplicativo](../../relational-databases/security/authentication-access/application-roles.md).  
  
> [!IMPORTANT]  
> Para proteger a senha da função de aplicativo quando ela é transmitida por uma rede, você sempre deve usar uma conexão criptografada ao habilitar uma função de aplicativo.
> A [!INCLUDE[msCoName](../../includes/msconame-md.md)] opção ODBC **Encrypt** não é suportada pelo **SqlClient**. Se for necessário armazenar credenciais, criptografe-as com as funções da API de criptografia. A *senha* do parâmetro é armazenada como um hash unidirecional. Para preservar a compatibilidade com versões anteriores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]do, a política de complexidade de senha não é imposta pelo **sp_addapprole**. Para impor a política de complexidade de senha, use [criar função de aplicativo](../../t-sql/statements/create-application-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissões

Requer associação em **público** e conhecimento da senha para a função.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-activating-an-application-role-without-the-encrypt-option"></a>a. Ativando uma função de aplicativo sem a opção de criptografia

 O exemplo a seguir ativa uma função de aplicativo `SalesAppRole`, com a senha de texto sem-formatação `AsDeF00MbXX`, criada com permissões projetadas especificamente para o aplicativo usado pelo usuário atual.

```sql
EXEC sys.sp_setapprole 'SalesApprole', 'AsDeF00MbXX';  
GO
```

### <a name="b-activating-an-application-role-with-a-cookie-and-then-reverting-to-the-original-context"></a>B. Ativando uma função de aplicativo com um cookie e revertendo para o contexto original

 O exemplo a seguir ativa a função de aplicativo `Sales11` com a senha `fdsd896#gfdbfdkjgh700mM` e cria um cookie. O exemplo retorna o nome do usuário atual e, em seguida, reverte para o contexto original executando `sp_unsetapprole`.  

```sql
DECLARE @cookie varbinary(8000);  
EXEC sys.sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sys.sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.
GO
```

## <a name="see-also"></a>Consulte Também

 [Procedimentos armazenados do sistema &#40;&#41;procedimentos armazenados de segurança do Transact-sql](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) [&#40;transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md) [criar função de aplicativo &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md) [remover função de aplicativo &#40;Transact-sql&#41;](../../t-sql/statements/drop-application-role-transact-sql.md) [sp_unsetapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)
