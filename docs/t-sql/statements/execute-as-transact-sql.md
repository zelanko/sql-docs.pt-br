---
title: EXECUTE AS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- EXECUTE AS
- EXECUTE_AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REVERT statement
- WITH NO REVERT clause
- sessions [SQL Server], execution context
- EXECUTE AS
- execution context [SQL Server]
- switching execution context
ms.assetid: 613b8271-7f7d-4378-b7a2-5a7698551dbd
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 6a038b8928eeda0df043ff42b621b95c48102b55
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="execute-as-transact-sql"></a>EXECUTE AS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Define o contexto de execução de uma sessão.  
  
 Por padrão, uma sessão é iniciada quando um usuário faz logon e é encerrada quando ele faz logoff. Todas as operações durante uma sessão estão sujeitas a verificações de permissão para aquele usuário. Quando uma instrução **EXECUTE AS** é executada, o contexto de execução da sessão é alternado para o logon ou o nome de usuário específico. Depois da alternância de contexto, as permissões são verificadas no logon e nos tokens de segurança do usuário para a conta, em vez da pessoa que chama a instrução **EXECUTE AS**. Em essência, o usuário ou a conta de logon são representados durante a execução da sessão ou do módulo, ou a alternância de contexto é explicitamente revertida.  
  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
{ EXEC | EXECUTE } AS <context_specification>  
[;]  
  
<context_specification>::=  
{ LOGIN | USER } = 'name'  
    [ WITH { NO REVERT | COOKIE INTO @varbinary_variable } ]   
| CALLER  
```  
  
## <a name="arguments"></a>Argumentos  
 Logon  
 **Aplica-se a**: do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica que o contexto de execução a ser representado é um logon. O escopo de representação é em nível de servidor.  
  
> [!NOTE]  
>  Essa opção não está disponível em um banco de dados independente nem no banco de dados SQL.  
  
 Usuário  
 Especifica que o contexto a ser representado é um usuário no banco de dados atual. O escopo de representação é restrito ao banco de dados atual. Uma opção de contexto para um usuário de banco de dados não herda as permissões em nível de servidor desse usuário.  
  
> [!IMPORTANT]  
>  Enquanto a opção de contexto para o usuário do banco de dados estiver ativa, qualquer tentativa de acessar os recursos fora do banco de dados provocará falha na instrução. Isso inclui instruções USE *database*, consultas distribuídas e consultas que fazem menção a outro banco de dados que usa identificadores em três ou quatro partes.  
  
 **'** *name* **'**  
 É um usuário ou nome de logon válido. *name* deve ser membro da função de servidor fixa **sysadmin** ou existir como uma entidade de segurança em [sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) ou [sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md), respectivamente.  
  
 *name* pode ser especificado como uma variável local.  
  
 *name* deve ser uma conta singleton e não pode ser um grupo, função, certificado, chave ou conta interna, como NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService ou NT AUTHORITY\LocalSystem.  
  
 Para obter mais informações, consulte [Especificando um nome de logon ou usuário](#_user) mais adiante neste tópico.  
  
 NO REVERT  
 Especifica que a alternância de contexto não pode ser revertida para o contexto anterior. A opção **NO REVERT** pode ser usada apenas no nível ad hoc.  
  
 Para obter mais informações sobre como reverter para o contexto anterior, veja [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md).  
  
 COOKIE INTO **@***varbinary_variable*  
 Especifica que o contexto de execução só pode ser revertido para o contexto anterior se a instrução de chamada REVERT WITH COOKIE contém o valor **@***varbinary_variable* correto. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] passa o cookie para **@***varbinary_variable*. A opção **COOKIE INTO** pode ser usada apenas no nível ad hoc.  
  
 **@** *varbinary_variable* é **varbinary (8000)**.  
  
> [!NOTE]  
>  O parâmetro **OUTPUT** de cookie está documentado atualmente como **varbinary(8000)**, que tem o tamanho máximo correto. No entanto, a implementação atual retorna **varbinary(100)**. Os aplicativos devem reservar **varbinary(8000)** para que o aplicativo continue a operar corretamente se o tamanho de retorno do cookie aumentar em uma versão futura.  
  
 CALLER  
 Quando usado em um módulo, especifica que as instruções dentro dele são executadas no contexto do chamador do módulo.  
  
 Quando usado fora de um módulo, a instrução não tem nenhuma ação.  
  
## <a name="remarks"></a>Remarks  
 A alteração no contexto de execução permanece em vigor até que uma das seguintes situações ocorra:  
  
-   Outra instrução EXECUTE AS é executada.  
  
-   Uma instrução REVERT é executada.  
  
-   A sessão é descartada.  
  
-   O procedimento armazenado ou gatilho onde o comando foi executado se encerra.  
  
Você pode criar uma pilha de contexto de execução chamando a instrução EXECUTE AS várias vezes em várias entidades. Quando chamada, a instrução REVERT alterna o contexto para o logon ou usuário no próximo nível acima da pilha de contexto. Para obter uma demonstração desse comportamento, veja o [Exemplo A](#_exampleA).  
  
##  <a name="_user"></a> Especificando um nome de logon ou usuário  
 O nome de usuário ou de logon especificado em EXECUTE AS \<context_specification> deve existir como uma entidade de segurança em **sys.database_principals** ou **sys.server_principals**, respectivamente, caso contrário, a instrução EXECUTE AS falhará. Além disso, as permissões IMPERSONATE devem ser concedidas na entidade de segurança. A menos que o chamador seja o proprietário do banco de dados ou membro da função de servidor fixa **sysadmin**, a entidade de segurança deverá existir quando o usuário estiver acessando o banco de dados ou a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de uma associação de grupo do Windows. Por exemplo, considere as seguintes condições: 
  
-   O grupo **CompanyDomain\SQLUsers** tem acesso ao banco de dados **Sales**.  
  
-   **CompanyDomain\SqlUser1** é um membro de **SQLUsers** e, por isso, tem acesso implícito ao banco de dados **Sales**.  
  
 Embora **CompanyDomain\SqlUser1** tenha acesso ao banco de dados por meio de associação no grupo **SQLUsers**, a instrução `EXECUTE AS USER = 'CompanyDomain\SqlUser1'` falhará porque `CompanyDomain\SqlUser1` não existe como entidade de segurança no banco de dados.  
  
Se o usuário ficou órfão (o logon associado não existe mais) e ele não foi criado com **WITHOUT LOGIN**, **EXECUTE AS** falhará para o usuário.  
  
## <a name="best-practice"></a>Prática recomendada  
 Especifique um logon ou usuário que tenha pelo menos os privilégios necessários para executar as operações da sessão. Por exemplo, não especifique um nome de logon com permissões em nível de servidor se apenas as permissões em nível de banco de dados forem necessárias; ou não especifique uma conta de proprietário de banco de dados, a menos que essas permissões sejam necessárias.  
  
> [!CAUTION]  
>  A instrução EXECUTE AS pode ser bem-sucedida, desde que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] possa resolver o nome. Se existir um usuário de domínio, o Windows poderá resolver o usuário para o [!INCLUDE[ssDE](../../includes/ssde-md.md)], embora o usuário Windows não tenha acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso pode levar a uma condição em que um logon sem acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pareça estar conectado, embora o logon representado só tenha as permissões concedidas a público ou convidado.  
  
## <a name="using-with-no-revert"></a>Usando WITH NO REVERT  
 Quando a instrução EXECUTE AS inclui a cláusula opcional WITH NO REVERT, o contexto de execução de uma sessão não pode ser redefinido usando REVERT ou executando outra instrução EXECUTE AS. O contexto definido pela instrução permanece até que a sessão seja descartada.  
  
 Quando a cláusula WITH NO REVERT COOKIE = @*varbinary_variabl*e for especificada, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] passa o valor do cookie para @*varbinary_variabl*e. O contexto de execução definido por essa instrução poderá ser revertido somente para o contexto anterior se a instrução de chamada REVERT WITH COOKIE = @*varbinary_variable* tiver o mesmo valor *@varbinary_variable*.  
  
 Essa opção é útil em um ambiente no qual um pool de conexão é usado. O pool de conexão é a manutenção de um grupo de conexões de banco de dados para reutilização por aplicativos em um servidor de aplicativos. Como o valor passado para *@varbinary_variable* é conhecido apenas pelo chamador da instrução EXECUTE AS (no caso, o aplicativo), o chamador pode garantir que o contexto de execução estabelecido não possa ser alterado por mais ninguém.  
  
## <a name="determining-the-original-login"></a>Determinando o logon original  
 Use a função [ORIGINAL_LOGIN](../../t-sql/functions/original-login-transact-sql.md) para retornar o nome do logon que conectou à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode usar essa função para retornar a identidade do logon original em sessões nas quais há muitas alternâncias de contexto explícitas ou implícitas.  
  
## <a name="permissions"></a>Permissões  
 Para especificar **EXECUTE AS** em um logon, o chamador precisa ter permissão **IMPERSONATE** no nome de logon especificado e não deve ter negada a permissão **IMPERSONATE ANY LOGIN**. Para especificar **EXECUTE AS** em um usuário de banco de dados, o chamador precisa ter permissões **IMPERSONATE** no nome de usuário especificado. Quando **EXECUTE AS CALLER** for especificado, as permissões **IMPERSONATE** não são necessárias.  
  
## <a name="examples"></a>Exemplos  
  
###  <a name="_exampleA"></a> A. Usando EXECUTE AS e REVERT para alternar o contexto  
 O exemplo a seguir cria uma pilha de execução de contexto usando várias entidades. A instrução `REVERT` é usada para redefinir o contexto de execução para o chamador anterior. A instrução `REVERT` é executada várias vezes movendo a pilha para cima até o contexto de execução ser definido como o chamador original.  
  
```  
USE AdventureWorks2012;  
GO  
--Create two temporary principals  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE LOGIN login2 WITH PASSWORD = 'Uor80$23b';  
GO  
CREATE USER user1 FOR LOGIN login1;  
CREATE USER user2 FOR LOGIN login2;  
GO  
--Give IMPERSONATE permissions on user2 to user1  
--so that user1 can successfully set the execution context to user2.  
GRANT IMPERSONATE ON USER:: user2 TO user1;  
GO  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- Set the execution context to login1.   
EXECUTE AS LOGIN = 'login1';  
--Verify the execution context is now login1.  
SELECT SUSER_NAME(), USER_NAME();  
--Login1 sets the execution context to login2.  
EXECUTE AS USER = 'user2';  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- The execution context stack now has three principals: the originating caller, login1 and login2.  
--The following REVERT statements will reset the execution context to the previous context.  
REVERT;  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
REVERT;  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
  
--Remove temporary principals.  
DROP LOGIN login1;  
DROP LOGIN login2;  
DROP USER user1;  
DROP USER user2;  
GO  
```  
  
### <a name="b-using-the-with-cookie-clause"></a>B. Usando a cláusula WITH COOKIE  
 O exemplo a seguir define o contexto de execução de uma sessão para determinado usuário e especifica a cláusula WITH NO REVERT COOKIE = @*varbinary_variabl*e. A instrução `REVERT` deve especificar o valor passado para a variável `@cookie` na instrução `EXECUTE AS` para reverter com êxito o contexto de volta para o chamador. Para executar este exemplo, o logon `login1` e o usuário `user1` criados no exemplo A devem existir.  
  
```  
DECLARE @cookie varbinary(8000);  
EXECUTE AS USER = 'user1' WITH COOKIE INTO @cookie;  
-- Store the cookie in a safe location in your application.  
-- Verify the context switch.  
SELECT SUSER_NAME(), USER_NAME();  
--Display the cookie value.  
SELECT @cookie;  
GO  
-- Use the cookie in the REVERT statement.  
DECLARE @cookie varbinary(8000);  
-- Set the cookie value to the one from the SELECT @cookie statement.  
SET @cookie = <value from the SELECT @cookie statement>;  
REVERT WITH COOKIE = @cookie;  
-- Verify the context switch reverted.  
SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)   
 [EXECUTE AS Clause &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)  
  
  

