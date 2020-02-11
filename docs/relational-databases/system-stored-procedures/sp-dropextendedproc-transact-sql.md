---
title: sp_dropextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproc
- sp_dropextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproc
ms.assetid: dd93af2c-1b7d-4e39-af23-2d21d270a381
author: stevestein
ms.author: sstein
ms.openlocfilehash: b12ebcfb662db9740efdf918f0857b94144e0ceb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68054301"
---
# <a name="sp_dropextendedproc-transact-sql"></a>sp_dropextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Descarta um procedimento armazenado estendido.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use a [integração CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_dropextendedproc [ @functname = ] 'procedure'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @functname = ] 'procedure'`É o nome do procedimento armazenado estendido a ser solto. o *procedimento* é **nvarchar (517)**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 A execução de **sp_dropextendedproc** descarta o nome do procedimento armazenado estendido definido pelo usuário da exibição do catálogo [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) e remove a entrada da exibição do catálogo [Sys. extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) . Esse procedimento armazenado só pode ser executado no banco de dados **mestre** .  
  
**sp_dropextendedproc** não remove os procedimentos armazenados estendidos do sistema. Em vez disso, o administrador do sistema deve negar a permissão EXECUTE no procedimento armazenado estendido para a função **pública** .  
  
 **sp_dropextendedproc** não pode ser executado dentro de uma transação.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_dropextendedproc**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir descarta o procedimento armazenado estendido `xp_hello`.  
  
> [!NOTE]  
>  Esse procedimento armazenado estendido já deve existir, caso contrário, o exemplo retornará uma mensagem de erro.  
  
```  
USE master;  
GO  
EXEC sp_dropextendedproc 'xp_hello';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addextendedproc](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpextendedproc](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
