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
ms.openlocfilehash: b158c4571deadadeaee23ffa6e46eb48a8c8446e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299588"
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

`[ @rolename = ] 'role'`É o nome da função de aplicação definida no banco de dados atual. *função* é **sysname,** sem padrão. *função* deve existir no banco de dados atual.  
  
`[ @password = ] { encrypt N'password' }`É a senha necessária para ativar a função de aplicativo. *senha* é **sysname,** sem padrão. *a senha* pode ser ofuscada usando a função **criptografada** ODBC. Quando você usa a função **criptografar,** a senha deve ser convertida em uma seqüência unicode colocando **N** antes da primeira marca de cotação.  
  
 A opção de criptografia não é suportada em conexões que estão usando **sqlClient**.  
  
> [!IMPORTANT]  
> A função **de criptografia** ODBC não fornece criptografia. Você não deve confiar nessa função para proteger senhas que são transmitidas pela rede. Se essas informações forem transmitidas através de uma rede, use TLS ou IPSec.
  
 **@encrypt= 'nenhum'**  
 Especifica que nenhuma ofuscação deve ser usada. A senha é transmitida para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como texto sem-formatação. Esse é o padrão.  
  
 **@encrypt= 'odbc'**  
 Especifica que o ODBC ofuscará a senha usando a função **criptografada** ODBC antes de enviar a senha para o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Isso pode ser especificado somente quando um cliente ODBC ou o provedor OLE DB para SQL Server for utilizado.  
  
`[ @fCreateCookie = ] true | false`Especifica se um cookie deve ser criado. **verdade** é implicitamente convertida em 1. **falso** é implicitamente convertido em 0.  
  
`[ @cookie = ] @cookie OUTPUT`Especifica um parâmetro de saída para conter o cookie. O cookie é gerado somente se o valor de ** \@fCreateCookie** for **verdadeiro**. **varbinary(8000)**  
  
> [!NOTE]  
> O parâmetro **OUTPUT** de cookie para **sp_setapprole** está documentado atualmente como **varbinary(8000)** , que tem o tamanho máximo correto. No entanto, a implementação atual retorna **varbinary(50)** . Os aplicativos devem continuar a reservar **varbinary (8000)** para que o aplicativo continue a funcionar corretamente se o tamanho do retorno do cookie aumentar em uma versão futura.
  
## <a name="return-code-values"></a>Valores do código de retorno

 0 (êxito) e 1 (falha)  
  
## <a name="remarks"></a>Comentários

 Depois que uma função de aplicativo é ativada usando **sp_setapprole,** a função permanece ativa até que o usuário se desconecte do servidor ou execute **sp_unsetapprole**. **sp_setapprole** só podem ser [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas por declarações diretas. **sp_setapprole** não pode ser executada dentro de outro procedimento armazenado ou dentro de uma transação definida pelo usuário.  
  
 Para obter uma visão geral das funções do aplicativo, consulte [Funções de aplicativo](../../relational-databases/security/authentication-access/application-roles.md).  
  
> [!IMPORTANT]  
> Para proteger a senha da função do aplicativo quando ela é transmitida através de uma rede, você deve sempre usar uma conexão criptografada ao ativar uma função de aplicativo.
> A [!INCLUDE[msCoName](../../includes/msconame-md.md)] opção **de criptografia** ODBC não é suportada pelo **SqlClient**. Se for necessário armazenar credenciais, criptografe-as com as funções da API de criptografia. A *senha* do parâmetro é armazenada como um hash unidirecional. Para preservar a compatibilidade [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]com versões anteriores da política de complexidade de senha saem aplicadas por **sp_addapprole**. Para impor a política de complexidade de senha, use [CRIAR FUNÇÃO DE APLICATIVO](../../t-sql/statements/create-application-role-transact-sql.md).  
  
## <a name="permissions"></a>Permissões

Requer adesão em **público** e conhecimento da senha para a função.  
  
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

 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md) [Segurança Armazenada Procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md) CRIAR PAPEL DO APLICATIVO &#40;[TRANSACT-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md) PAPEL DO APLICATIVO DROP &#40;[Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md) sp_unsetapprole &#40;[Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unsetapprole-transact-sql.md)
