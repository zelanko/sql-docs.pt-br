---
title: sp_syscollector_delete_collector_type (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_delete_collector_type
- sp_syscollector_delete_collector_type_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_delete_collector_type
ms.assetid: 3f32905e-0005-42cb-aef1-7bd04c51fbac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e7f36eb20b4a5f72ce980f8e35cb39580f4f5142
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537178"
---
# <a name="spsyscollectordeletecollectortype-transact-sql"></a>sp_syscollector_delete_collector_type (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exclui a definição de um tipo de coletor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_delete_collector_type [[ @collector_type_uid = ] 'collector_type_uid' ]  
          , [[ @name = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @collector_type_uid = ] 'collector_type_uid'` É o GUID para o tipo de coletor. *collector_type_uid* está **uniqueidentifier** e deve ter um valor se *nome* é NULL.  
  
`[ @name = ] 'name'` É o nome do tipo de coletor. *nome da* está **sysname** e deve ter um valor se *collector_type_uid* é NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Qualquer um dos *collector_type_uid* ou *nome* deve ter um valor, ambos não podem ser NULL.  
  
 Este procedimento lançará um erro caso existam itens de coleta deste tipo de coleta.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **dc_admin** (com permissão EXECUTE) a função de banco de dados fixa para executar esse procedimento.  
  
## <a name="example"></a>Exemplo  
 Este exemplo exclui o tipo de coletor de Consultas T-SQL Genérico.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_delete_collector_type @collector_type_uid = '302E93D1-3424-4be7-AA8E-84813ECF2419';  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
