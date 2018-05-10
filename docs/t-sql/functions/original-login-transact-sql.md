---
title: ORIGINAL_LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ORIGINAL_LOGIN_TSQL
- ORIGINAL_LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], context switches
- context switching [SQL Server], login names
- original login names [SQL Server]
- ORIGINAL_LOGIN function
- names [SQL Server], logins
ms.assetid: ddfb0991-cde3-4b97-a5b7-ee450133f160
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3461826caf7fb863176eece7285131797086f0f9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="originallogin-transact-sql"></a>ORIGINAL_LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o nome do logon que se conectou à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode usar essa função para retornar a identidade do logon original em sessões nas quais há muitas alternâncias de contexto explícitas ou implícitas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ORIGINAL_LOGIN( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **sysname**  
  
## <a name="remarks"></a>Remarks  
 Essa função pode ser útil ao examinar a identidade do contexto de conexão original. Enquanto funções como [SESSION_USER](../../t-sql/functions/session-user-transact-sql.md) e [CURRENT_USER](../../t-sql/functions/current-user-transact-sql.md) retornam o contexto de execução atual, ORIGINAL_LOGIN retorna a identidade do logon que se conectou primeiro à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na sessão.  
  
 Retorna NULL no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir alterna o contexto de execução da sessão atual do chamador das instruções para `login1`. As funções `SUSER_SNAME` e `ORIGINAL_LOGIN` são usadas para retornar o usuário da sessão atual (o usuário para quem o contexto foi alternado) e a conta de logon original.  
  
```  
USE AdventureWorks2012;  
GO  
--Create a temporary login and user.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE USER user1 FOR LOGIN login1;  
GO  
--Execute a context switch to the temporary login account.  
DECLARE @original_login sysname;  
DECLARE @current_context sysname;  
EXECUTE AS LOGIN = 'login1';  
SET @original_login = ORIGINAL_LOGIN();  
SET @current_context = SUSER_SNAME();  
SELECT 'The current executing context is: '+ @current_context;  
SELECT 'The original login in this session was: '+ @original_login  
GO  
-- Return to the original execution context  
-- and remove the temporary principal.  
REVERT;  
GO  
DROP LOGIN login1;  
DROP USER user1;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [REVERT &#40;Transact-SQL&#41;](../../t-sql/statements/revert-transact-sql.md)  
  
  
