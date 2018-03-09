---
title: sp_OADestroy (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_OADestroy_TSQL
- sp_OADestroy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OADestroy
ms.assetid: 0bd1cff4-ceff-4095-9ae4-e1e65a80f5d6
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 409ce43749b6047d7874475a4c1afc6bccd34fb2
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spoadestroy-transact-sql"></a>sp_OADestroy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Destrói um objeto OLE criado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_OADestroy objecttoken      
```  
  
## <a name="arguments"></a>Argumentos  
 *objecttoken*  
 É o token de objeto de um objeto OLE que foi criado anteriormente usando **sp_OACreate**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha) que é o valor inteiro do HRESULT retornado pelo objeto de Automação OLE.  
  
 Para obter mais informações sobre códigos de retorno HRESULT, consulte [OLE Automation códigos de retorno e informações de erro](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="remarks"></a>Comentários  
 Se **sp_OADestroy** não for chamado, o criado objeto OLE é destruído automaticamente no final do lote.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir destrói criado anteriormente **SQLServer** objeto.  
  
```  
EXEC @hr = sp_OADestroy @object;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Automação OLE armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Script de exemplo de automação](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
