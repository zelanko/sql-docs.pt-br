---
title: sp_syscollector_enable_collector (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_enable_collector
- sp_syscollector_enable_collector_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_enable_collector
- data collector [SQL Server], stored procedures
ms.assetid: 53ff2b0d-b7da-4e3d-8f3d-35e857bc3720
author: stevestein
ms.author: sstein
ms.openlocfilehash: ab6087b68fba057e6acd91f43804b0e324992e1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68000809"
---
# <a name="sp_syscollector_enable_collector-transact-sql"></a>sp_syscollector_enable_collector (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Habilita o coletor de dados. Como há apenas um coletor de dados por servidor, nenhum parâmetro é necessário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dbo.sp_syscollector_enable_collector   
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhum  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Assume o coletor de dados no servidor como padrão.  
  
## <a name="permissions"></a>Permissões  
 É necessária a associação na função de banco de dados fixa **dc_admin** ou **dc_operator** (com a permissão EXECUTE) para executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir habilita o coletor de dados.  
  
```sql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_enable_collector;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de dados](../../relational-databases/data-collection/data-collection.md)  
  
  
