---
description: sp_helpextendedproc (Transact-SQL)
title: sp_helpextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpextendedproc
- sp_helpextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpextendedproc
ms.assetid: 7e1f017e-c898-4225-b375-6a73ef9aac7b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 68bc88bdaddc873c0f272ffef37d6465cddb45af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493216"
---
# <a name="sp_helpextendedproc-transact-sql"></a>sp_helpextendedproc (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Relata os procedimentos armazenados estendidos atualmente definidos e o nome da biblioteca de vínculo dinâmico (DLL) à qual o procedimento (função) pertence.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use a [integração CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpextendedproc [ [@funcname = ] 'procedure' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @funcname = ] 'procedure'` É o nome do procedimento armazenado estendido para o qual as informações são relatadas. o *procedimento* é **sysname**, com um padrão de NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do procedimento armazenado estendido.|  
|**dll**|**nvarchar(255)**|O nome da DLL.|  
  
## <a name="remarks"></a>Comentários  
 Quando o *procedimento* é especificado, **sp_helpextendedproc** relatórios sobre o procedimento armazenado estendido especificado. Quando esse parâmetro não é fornecido, **sp_helpextendedproc** retorna todos os nomes de procedimentos armazenados estendidos e os nomes de dll aos quais cada procedimento armazenado estendido pertence.  
  
## <a name="permissions"></a>Permissões  
 A permissão para executar **sp_helpextendedproc** é concedida ao **público**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-reporting-help-on-all-extended-stored-procedures"></a>a. Relatando ajuda em todos os procedimentos armazenados estendidos  
 O exemplo a seguir relata todos os procedimentos armazenados estendidos.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc;  
GO  
```  
  
### <a name="b-reporting-help-on-a-single-extended-stored-procedure"></a>B. Relatando ajuda em um único procedimento armazenado estendido  
 O exemplo a seguir relata sobre o `xp_cmdshell` procedimento armazenado estendido.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc xp_cmdshell;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addextendedproc ](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropextendedproc ](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
