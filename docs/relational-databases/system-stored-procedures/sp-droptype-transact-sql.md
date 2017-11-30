---
title: sp_droptype (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_droptype_TSQL
- sp_droptype
dev_langs: TSQL
helpviewer_keywords: sp_droptype
ms.assetid: e78464ac-2370-4c4e-9cc0-06aebc07cec5
caps.latest.revision: "33"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95c6a5166d3e1dec0bef153c3c545bdc36d879aa
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="spdroptype-transact-sql"></a>sp_droptype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exclui um tipo de dados de alias de **systypes**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_droptype [ @typename = ] 'type'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@typename=**] **'***tipo***'**  
 É o nome de um tipo de dados de alias que você possui. *tipo* é **sysname**, sem padrão.  
  
## <a name="return-code-type"></a>Tipo de código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Comentários  
 O **tipo** alias o tipo de dados não pode ser descartado se tabelas ou outros objetos de banco de dados fazem referência a ele.  
  
> [!NOTE]  
>  Um tipo de dados alias não pode ser descartado se o tipo de dados de alias for usado em uma definição de tabela ou se uma regra ou padrão forem associados a ele.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **db_owner** função de banco de dados fixa ou **db_ddladmin** função fixa de banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta o tipo de dados de alias `birthday`.  
  
> [!NOTE]  
>  Este tipo de dados de alias já deve existir ou este exemplo retornará uma mensagem de erro.  
  
```  
USE master;  
GO  
EXEC sp_droptype 'birthday';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Mecanismo de banco de dados armazenados procedimentos &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [sp_addtype &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addtype-transact-sql.md)   
 [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
