---
title: sp_syscollector_stop_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_stop_collection_set_TSQL
- sp_syscollector_stop_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_stop_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 4668cfb7-462f-40d0-948c-8f740a792a4d
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1464a9dfac11cf6b84a3895b94881d4825f9758c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spsyscollectorstopcollectionset-transact-sql"></a>sp_syscollector_stop_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Interrompe um conjunto de coleta.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_stop_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @stop_collection_job = ] stop_collection_job ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @collection_set_id = ] *collection_set_id*  
 É o identificador local exclusivo do conjunto de coleta. *collection_set_id* é **int** com um valor padrão de NULL. *collection_set_id* deve ter um valor se *nome* é NULL.  
  
 [ @name =] '*nome*'  
 É o nome do conjunto de coleta. *nome* é **sysname** com um valor padrão de NULL. *nome* deve ter um valor se *collection_set_id* é NULL.  
  
 [ @stop_collection_job = ] *stop_collection_job*  
 Especifica que o trabalho de coleta do conjunto de coleta será interrompido se estiver em execução. *stop_collection_job* é **bit** com um padrão de 1.  
  
 *stop_collection_job* aplica-se apenas aos conjuntos de coleta com o modo de coleta definido como cache. Para obter mais informações, consulte [sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 sp_syscollector_create_collection_set deve ser executado no contexto do banco de dados de sistema msdb.  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento, é necessária a associação na função de banco de dados fixa dc_operator (com a permissão EXECUTE).  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir interrompe um conjunto de coleta usando seu identificador.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_stop_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Coleta de dados](../../relational-databases/data-collection/data-collection.md)   
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
