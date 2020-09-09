---
description: sp_unsetapprole (Transact-SQL)
title: sp_unsetapprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_unsetapprole_TSQL
- sp_unsetapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_unsetapprole
ms.assetid: 4c4033d3-1a34-4dfb-835d-e3293d1a442d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b024d959c49cfba5d2d1daeef526ac5d5a484458
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547245"
---
# <a name="sp_unsetapprole-transact-sql"></a>sp_unsetapprole (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Desativa uma função de aplicativo e reverte para o contexto de segurança anterior.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_unsetapprole @cookie   
```  
  
## <a name="arguments"></a>Argumentos  
 **\@cookie**  
 Especifica o cookie criado quando a função de aplicativo foi ativada. O cookie é criado por [sp_setapprole &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md). **varbinary (8000)**.  
  
> [!NOTE]  
>  O parâmetro **OUTPUT** de cookie para **sp_setapprole** está documentado atualmente como **varbinary(8000)** , que tem o tamanho máximo correto. No entanto, a implementação atual retorna **varbinary(50)** . Os aplicativos devem continuar a reservar **varbinary (8000)** para que o aplicativo continue a funcionar corretamente se o tamanho de retorno do cookie aumentar em uma versão futura.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) e 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Depois que uma função de aplicativo é ativada usando **sp_setapprole**, a função permanece ativa até que o usuário seja desconectado do servidor ou execute **sp_unsetapprole**.  
  
 Para obter uma visão geral das funções de aplicativo, consulte [funções de aplicativo](../../relational-databases/security/authentication-access/application-roles.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação em **público** e conhecimento do cookie salvo quando a função de aplicativo foi ativada.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="activating-an-application-role-with-a-cookie-then-reverting-to-the-previous-context"></a>Ativando uma função de aplicativo com um cookie e revertendo para o contexto anterior  
 O exemplo a seguir ativa a função de aplicativo `Sales11` com a senha `fdsd896#gfdbfdkjgh700mM` e cria um cookie. O exemplo retorna o nome do usuário atual e, em seguida, reverte para o contexto original executando **sp_unsetapprole**.  
  
```  
DECLARE @cookie varbinary(8000);  
EXEC sp_setapprole 'Sales11', 'fdsd896#gfdbfdkjgh700mM'  
    , @fCreateCookie = true, @cookie = @cookie OUTPUT;  
-- The application role is now active.  
SELECT USER_NAME();  
-- This will return the name of the application role, Sales11.  
EXEC sp_unsetapprole @cookie;  
-- The application role is no longer active.  
-- The original context has now been restored.  
GO  
SELECT USER_NAME();  
-- This will return the name of the original user.   
GO   
```  
  
## <a name="see-also"></a>Consulte Também  
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)  
  
  
