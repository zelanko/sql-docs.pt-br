---
title: sp_unregistercustomresolver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_unregistercustomresolver_TSQL
- sp_unregistercustomresolver
helpviewer_keywords:
- sp_unregistercustomresolver
ms.assetid: 08bd20c8-c6be-4be2-be9f-2b5e1d7bee43
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 935796cb328807eb4413991eeac97a95bd9b9384
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891382"
---
# <a name="sp_unregistercustomresolver-transact-sql"></a>sp_unregistercustomresolver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Cancela o registro de um módulo de lógica comercial previamente registrado. Lógica comercial pode estar no formato de um componente COM ou de um assembly [!INCLUDE[msCoName](../../includes/msconame-md.md)].NET FRamework. Esse procedimento armazenado é executado no Distribuidor onde a lógica de negócios personalizada foi registrada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_unregistercustomresolver [ @article_resolver = ] 'article_resolver'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @article_resolver = ] 'article_resolver'`Especifica o nome da lógica de negócios personalizada que está sendo cancelada. *article_resolver* é **nvarchar (255)**, sem padrão. Se a lógica de negócios que está sendo removida for um componente COM, esse parâmetro será o nome amigável do componente. Se a lógica de negócios for um assembly .NET Framework, esse parâmetro será o nome do assembly.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_unregistercustomresolver** é usado na replicação de mesclagem.  
  
 Use [sp_enumcustomresolvers](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) em qualquer servidor na topologia de replicação para retornar a lista de módulos de lógica de negócios personalizados registrados ou resolvedores de com disponíveis para a topologia.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_unregistercustomresolver**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_lookupcustomresolver](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_registercustomresolver](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
