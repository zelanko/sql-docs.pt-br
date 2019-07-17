---
title: sp_getapplock (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_getapplock_TSQL
- sp_getapplock
dev_langs:
- TSQL
helpviewer_keywords:
- application locks
- sp_getapplock
ms.assetid: e1e85908-9f31-47cf-8af6-88c77e6f24c9
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f87a62e744bcd6032c58cdb3b327b747e5343d2a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124006"
---
# <a name="spgetapplock-transact-sql"></a>sp_getapplock (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Insere um bloqueio em um recurso de aplicativo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_getapplock [ @Resource = ] 'resource_name' ,  
     [ @LockMode = ] 'lock_mode'   
     [ , [ @LockOwner = ] 'lock_owner' ]   
     [ , [ @LockTimeout = ] 'value' ]  
     [ , [ @DbPrincipal = ] 'database_principal' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @Resource=] '*resource_name*'  
 É uma cadeia de caracteres especificando um nome que identifica o recurso de bloqueio. O aplicativo deve garantir que o nome do recurso seja exclusivo. O nome especificado é internamente transformado em hash para um valor que pode ser armazenado no gerenciador de bloqueio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *resource_name* está **nvarchar (255)** sem nenhum padrão. Se uma cadeia de caracteres do recurso for maior que **nvarchar (255)** , ele será truncado para **nvarchar (255)** .  
  
 *resource_name* é binário comparado e, portanto, diferencia maiusculas de minúsculas, independentemente das configurações de agrupamento do banco de dados atual.  
  
> [!NOTE]  
>  Depois que um bloqueio de aplicativo for adquirido, somente os primeiros 32 caracteres poderão ser recuperados em texto não criptografado, o restante será em modo hash.  
  
 [ @LockMode=] '*lock_mode*'  
 É o modo de bloqueio a ser obtido para um recurso específico. *lock_mode* é **nvarchar(32)** e não tem valor padrão. O valor pode ser qualquer um dos seguintes: **Compartilhado**, **Update**, **IntentShared**, **IntentExclusive**, ou **exclusivo**.  
  
 [ @LockOwner=] '*lock_owner*'  
 É o proprietário do bloqueio, que é o valor de *lock_owner* quando o bloqueio foi solicitado. *lock_owner* é **nvarchar(32)** . O valor pode ser **Transaction** (o padrão) ou **Session**. Quando o *lock_owner* valor estiver **transação**, por padrão ou explicitamente especificado, sp_getapplock deve ser executado de dentro de uma transação.  
  
 [ @LockTimeout=] '*valor*'  
 É um valor de tempo limite de bloqueio em milissegundos. O valor padrão é o mesmo que o valor retornado por@LOCK_TIMEOUT. Para indicar que uma solicitação de bloqueio deve retornar um código de retorno de -1 em vez de esperar pelo bloqueio quando a solicitação não pode ser concedida imediatamente, especifique 0.  
  
 [ @DbPrincipal=] '*database_principal*'  
 É o usuário, função ou função de aplicativo que tem permissões para um objeto em um banco de dados. O chamador da função deve ser um membro da *database_principal*, dbo ou db_owner fixa a função de banco de dados para chamar a função com êxito. O padrão é público.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 \>= 0 (êxito) ou < 0 (falha)  
  
|Valor|Resultado|  
|-----------|------------|  
|0|O bloqueio foi concedido com sucesso de forma síncrona.|  
|1|O bloqueio foi concedido com sucesso após outros bloqueios incompatíveis terem sido liberados.|  
|-1|A solicitação de bloqueio expirou.|  
|-2|A solicitação de bloqueio foi cancelada.|  
|-3|A solicitação de bloqueio foi selecionada como uma vítima de deadlock.|  
|-999|Indica uma validação de parâmetro ou outro erro de chamada.|  
  
## <a name="remarks"></a>Comentários  
 Bloqueios inseridos em um recurso são associados com a transação atual ou a sessão atual. Os bloqueios associados a uma transação atual são liberados quando a transação for confirmada ou revertida. Os bloqueios associados a sessão são liberados quando a sessão é desconectada. Quando o servidor é desligado por algum motivo, todos os bloqueios são liberados.  
  
 O recurso de bloqueio criado por sp_getapplock é criado no banco de dados atual para a sessão. Cada recurso de bloqueio é identificado pelos valores combinados de:  
  
-   A ID do banco de dados que contém o recurso de bloqueio.  
  
-   O princípio de banco de dados especificado no parâmetro @DbPrincipal.  
  
-   O nome do bloqueio especificado no parâmetro @Resource.  
  
 Somente um membro do banco de dados principal especificado no parâmetro @DbPrincipal pode adquirir bloqueios de aplicativo que especificam o banco de dados principal. Membros das funções dbo e db_owner são implicitamente considerados membros de todas as outras funções.  
  
 Bloqueios podem ser explicitamente liberados com sp_releaseapplock. Quando um aplicativo chama sp_getapplock várias vezes para o mesmo recurso de bloqueio, sp_releaseapplock deve ser chamado o mesmo número de vezes para liberar o bloqueio.  Quando um bloqueio é aberto com o `Transaction` proprietário de bloqueio, que o bloqueio é liberado quando a transação é confirmada ou revertida.
  
 Se sp_getapplock for chamado várias vezes para o mesmo recurso de bloqueio, mas o modo de bloqueio especificado em qualquer solicitação não for igual ao modo existente, o efeito no recurso será uma união dos dois modos de bloqueio. Na maioria dos casos, isto significa que o modo de bloqueio é promovido para o modo de bloqueio mais forte, o modo existente ou o modo solicitado recentemente. Esse modo de bloqueio mais forte é mantido até que bloqueio seja totalmente liberado, mesmo se chamadas de liberação de bloqueio ocorram antes daquele momento. Por exemplo, na seguinte sequência de chamadas, o recurso é mantido em modo `Exclusive` ao invés de modo `Shared`.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Shared';  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Exclusive';  
EXEC @result = sp_releaseapplock @Resource = 'Form1';  
COMMIT TRANSACTION;  
GO  
```  
  
 Um deadlock com um bloqueio de aplicativo não reverte a transação que solicitou o bloqueio de aplicativo. Qualquer reversão que poderia ser requerida como resultado do valor de retorno deve ser feita manualmente. Consequentemente, recomendamos que a verificação de erros seja incluída no código de forma que se forem retornados certos valores (por exemplo, -3), um ROLLBACK TRANSACTION ou ação alternativa seja iniciada.  
  
 Veja um exemplo:  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Exclusive';  
IF @result = -3  
BEGIN  
    ROLLBACK TRANSACTION;  
END  
ELSE  
BEGIN  
    EXEC @result = sp_releaseapplock @Resource = 'Form1';  
    COMMIT TRANSACTION;  
END;  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa o ID de banco de dados atual para qualificar o recurso. Logo, se sp_getapplock for executado, mesmo com valores de parâmetro idênticos em bancos de dados diferentes, o resultado criará bloqueios separados em recursos separados.  
  
 Use a exibição de gerenciamento dinâmico sys.dm_tran_locks ou o procedimento armazenado de sistema sp_lock para examinar informações de bloqueio ou use [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para monitorar os bloqueios.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir insere um bloqueio compartilhado que é associado à transação atual no recurso `Form1` no banco de dados `AdventureWorks2012`.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Shared';  
COMMIT TRAN;  
GO  
```  
  
 O exemplo a seguir especifica `dbo` como o principal do banco de dados.  
  
```  
BEGIN TRAN;  
EXEC sp_getapplock @DbPrincipal = 'dbo', @Resource = 'AdventureWorks2012',   
     @LockMode = 'Shared';  
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [APPLOCK_MODE &#40;Transact-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)   
 [APPLOCK_TEST &#40;Transact-SQL&#41;](../../t-sql/functions/applock-test-transact-sql.md)   
 [sp_releaseapplock &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)  
  
  
