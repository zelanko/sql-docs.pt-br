---
title: Executar como (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e389fdc50da662deeab7eba030a367e5fc7e97cb
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="execute-as-transact-sql"></a>EXECUTE AS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Define o contexto de execução de uma sessão.  
  
 Por padrão, uma sessão é iniciada quando um usuário faz logon e é encerrada quando ele faz logoff. Todas as operações durante uma sessão estão sujeitas a verificações de permissão para aquele usuário. Quando um **EXECUTE AS** instrução é executada, o contexto de execução da sessão é alternado para o nome de logon ou usuário especificado. Após a alternância de contexto, as permissões são verificadas no logon e usuário tokens de segurança para essa conta em vez da pessoa que chama o **EXECUTE AS** instrução. Em essência, o usuário ou a conta de logon são representados durante a execução da sessão ou do módulo, ou a alternância de contexto é explicitamente revertida.  
  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
>  Essa opção não está disponível em um banco de dados independente ou no banco de dados SQL.  
  
 Usuário  
 Especifica que o contexto a ser representado é um usuário no banco de dados atual. O escopo de representação é restrito ao banco de dados atual. Uma opção de contexto para um usuário de banco de dados não herda as permissões em nível de servidor desse usuário.  
  
> [!IMPORTANT]  
>  Enquanto a opção de contexto para o usuário do banco de dados estiver ativa, qualquer tentativa de acessar os recursos fora do banco de dados provocará falha na instrução. Isso inclui usar *banco de dados* instruções, consultas distribuídas e consultas que fazem referência a outro banco de dados que usa identificadores de três ou quatro partes.  
  
 **'** *nome* **'**  
 É um usuário ou nome de logon válido. *nome* deve ser um membro do **sysadmin** função de servidor fixa ou existir como entidade de segurança em [database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md) ou [sys. server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md), respectivamente.  
  
 *nome* pode ser especificado como uma variável local.  
  
 *nome* deve ser uma conta singleton e não pode ser um grupo, função, certificado, chave ou conta interna, como NT AUTHORITY\LocalService, NT AUTHORITY\NetworkService ou NT authority\localsystem..  
  
 Para obter mais informações, consulte [especificando um nome de logon ou usuário](#_user) mais adiante neste tópico.  
  
 NO REVERT  
 Especifica que a alternância de contexto não pode ser revertida para o contexto anterior. O **NO REVERT** opção pode ser usada apenas no nível adhoc.  
  
 Para obter mais informações sobre como reverter para o contexto anterior, consulte [REVERT &#40; Transact-SQL &#41; ](../../t-sql/statements/revert-transact-sql.md).  
  
 COOKIE em  **@**  *varbinary_variable*  
 Especifica o contexto de execução só pode ser revertido para o contexto anterior se a instrução de chamada REVERT WITH COOKIE contiver corretas  **@**  *varbinary_variable* valor. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] passa o cookie para  **@**  *varbinary_variable*. O **COOKIE em** opção pode ser usada apenas no nível adhoc.  
  
 **@***varbinary_variable* é **varbinary (8000)**.  
  
> [!NOTE]  
>  O cookie **saída** parâmetro está documentado atualmente como **varbinary (8000)** que é o comprimento máximo correto. No entanto, a implementação atual retorna **varbinary(100)**. Aplicativos devem reservar **varbinary (8000)** para que o aplicativo continua a operar corretamente se o cookie retornar aumentos de tamanho em uma versão futura.  
  
 CALLER  
 Quando usado em um módulo, especifica que as instruções dentro dele são executadas no contexto do chamador do módulo.  
  
 Quando usado fora de um módulo, a instrução não tem nenhuma ação.  
  
## <a name="remarks"></a>Comentários  
 A alteração no contexto de execução permanece em vigor até que uma das seguintes situações ocorra:  
  
-   Outra instrução EXECUTE AS é executada.  
  
-   Uma instrução REVERT é executada.  
  
-   A sessão é descartada.  
  
-   O procedimento armazenado ou gatilho onde o comando foi executado se encerra.  
  
Você pode criar uma pilha de contexto de execução chamando a instrução EXECUTE AS várias vezes em várias entidades. Quando chamada, a instrução REVERT alterna o contexto para o logon ou usuário no próximo nível acima da pilha de contexto. Para ver uma demonstração desse comportamento, consulte [exemplo um](#_exampleA).  
  
##  <a name="_user"></a>Especificando um nome de logon ou usuário  
 O nome de usuário ou logon especificado em EXECUTE AS \<context_specification > deve existir como entidade de segurança em **database_principals** ou **sys. server_principals**, respectivamente, ou o EXECUTE a instrução falhará. Além disso, as permissões IMPERSONATE devem ser concedidas na entidade de segurança. A menos que o chamador seja o proprietário do banco de dados, ou é um membro do **sysadmin** função de servidor fixa, o principal deverá existir quando o usuário estiver acessando o banco de dados ou instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de uma janela de associação de grupo. Por exemplo, considere as seguintes condições: 
  
-   **CompanyDomain\SQLUsers** grupo tem acesso para o **vendas** banco de dados.  
  
-   **CompanyDomain\SqlUser1** é um membro de **SQLUsers** e, portanto, tem acesso implícito ao **vendas** banco de dados.  
  
 Embora **CompanyDomain\SqlUser1** tem acesso ao banco de dados por meio de associação a **SQLUsers** grupo, a instrução `EXECUTE AS USER = 'CompanyDomain\SqlUser1'` falha porque `CompanyDomain\SqlUser1` não existe como uma entidade no o banco de dados.  
  
Se o usuário ficou órfão (o logon associado não existe mais), e o usuário não foi criado com **sem logon**, **EXECUTE AS** irá falhar para o usuário.  
  
## <a name="best-practice"></a>Prática recomendada  
 Especifique um logon ou usuário que tenha pelo menos os privilégios necessários para executar as operações da sessão. Por exemplo, não especifique um nome de logon com permissões em nível de servidor se apenas as permissões em nível de banco de dados forem necessárias; ou não especifique uma conta de proprietário de banco de dados, a menos que essas permissões sejam necessárias.  
  
> [!CAUTION]  
>  A instrução EXECUTE AS pode ser bem-sucedida, desde que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] possa resolver o nome. Se existir um usuário de domínio, o Windows poderá resolver o usuário para o [!INCLUDE[ssDE](../../includes/ssde-md.md)], embora o usuário Windows não tenha acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isso pode levar a uma condição em que um logon sem acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pareça estar conectado, embora o logon representado só tenha as permissões concedidas a público ou convidado.  
  
## <a name="using-with-no-revert"></a>Usando WITH NO REVERT  
 Quando a instrução EXECUTE AS inclui a cláusula opcional WITH NO REVERT, o contexto de execução de uma sessão não pode ser redefinido usando REVERT ou executando outra instrução EXECUTE AS. O contexto definido pela instrução permanece até que a sessão seja descartada.  
  
 Quando o WITH NO REVERT COOKIE = @*varbinary_variabl*cláusula for especificada, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] passa o valor do cookie para @*varbinary_variabl*e. O contexto de execução definido por essa instrução só poderá ser revertida para o contexto anterior se a chamada REVERT WITH COOKIE = @*varbinary_variable* declaração contém o mesmo  *@varbinary_variable*  valor.  
  
 Essa opção é útil em um ambiente no qual um pool de conexão é usado. O pool de conexão é a manutenção de um grupo de conexões de banco de dados para reutilização por aplicativos em um servidor de aplicativos. Como o valor passado para  *@varbinary_variable*  é conhecido apenas pelo chamador de EXECUTE AS instrução, o chamador pode garantir que o contexto de execução estabelecido não pode ser alterado por outra pessoa.  
  
## <a name="determining-the-original-login"></a>Determinando o logon original  
 Use o [ORIGINAL_LOGIN](../../t-sql/functions/original-login-transact-sql.md) função para retornar o nome de logon que se conectou à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode usar essa função para retornar a identidade do logon original em sessões nas quais há muitas alternâncias de contexto explícitas ou implícitas.  
  
## <a name="permissions"></a>Permissões  
 Para especificar **EXECUTE AS** em um logon, o chamador deve ter **REPRESENTAR** permissão no logon especificado nome e não deve ser negado a **REPRESENTAR qualquer logon** permissão . Para especificar **EXECUTE AS** em um usuário de banco de dados, o chamador deve ter **REPRESENTAR** permissões no nome de usuário especificado. Quando **EXECUTE AS CALLER** for especificado, **REPRESENTAR** permissões não são necessárias.  
  
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
 O exemplo a seguir define o contexto de execução de uma sessão para um usuário especificado e especifica o WITH NO REVERT COOKIE = @*varbinary_variabl*cláusula. A instrução `REVERT` deve especificar o valor passado para a variável `@cookie` na instrução `EXECUTE AS` para reverter com êxito o contexto de volta para o chamador. Para executar este exemplo, o logon `login1` e o usuário `user1` criados no exemplo A devem existir.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [REVERTER &#40; Transact-SQL &#41;](../../t-sql/statements/revert-transact-sql.md)   
 [Executar como a cláusula &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)  
  
  


