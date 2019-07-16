---
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 65fe8e1496fba4e622d63f1ce560aba4c1acfb83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022245"
---
# <a name="spunsetapprole-transact-sql"></a>sp_unsetapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Desativa uma função de aplicativo e reverte para o contexto de segurança anterior.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_unsetapprole @cookie   
```  
  
## <a name="arguments"></a>Argumentos  
 **@cookie**  
 Especifica o cookie criado quando a função de aplicativo foi ativada. O cookie é criado pelo [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md). **varbinary(8000)** .  
  
> [!NOTE]  
>  O parâmetro **OUTPUT** de cookie para **sp_setapprole** está documentado atualmente como **varbinary(8000)** , que tem o tamanho máximo correto. No entanto, a implementação atual retorna **varbinary(50)** . Aplicativos devem continuar a reservar **varbinary(8000)** para que o aplicativo continue a operar corretamente se o cookie retornar aumentos de tamanho em uma versão futura.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) e 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Depois de um aplicativo de função for ativada por meio **sp_setapprole**, a função permanece ativa até que o usuário se desconecta do servidor ou executa **sp_unsetapprole**.  
  
 Para obter uma visão geral das funções de aplicativo, consulte [funções de aplicativo](../../relational-databases/security/authentication-access/application-roles.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **pública** e conhecimento do cookie salvo quando a função de aplicativo foi ativada.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [sp_setapprole &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos de segurança armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [DROP APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-application-role-transact-sql.md)  
  
  
