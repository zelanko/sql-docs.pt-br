---
title: sp_syscollector_start_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_start_collection_set_TSQL
- sp_syscollector_start_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_start_collection_set
ms.assetid: d8357180-f51e-4681-99f9-0596fe2d2b53
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67ac114cfdbcea9cf8585b6eb76cfa4467919529
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="spsyscollectorstartcollectionset-transact-sql"></a>sp_syscollector_start_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia um conjunto de coleta se o coletor já estiver habilitado e o conjunto de coleta não estiver sendo executado. Se o coletor não estiver habilitado, habilite o coletor executando [sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md) e, em seguida, use esse procedimento armazenado para iniciar um conjunto de coleta.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_start_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@collection_set_id =** ] *collection_set_id*  
 É o identificador local exclusivo do conjunto de coleta. *collection_set_id* é **int** com um valor padrão de NULL. *collection_set_id* deve ter um valor se *nome* é NULL.  
  
 [  **@name =** ] '*nome*'  
 É o nome do conjunto de coleta. *nome* é **sysname** com um valor padrão de NULL. *nome* deve ter um valor se *collection_set_id* é NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 sp_syscollector_create_collection_set deve ser executado no contexto do banco de dados do sistema msdb e o SQL Server Agent deve estar habilitado.  
  
 Este procedimento falha quando executado em um conjunto de coleta que não tem uma agenda. Se o conjunto de coleta não tem uma agenda (porque seu modo de coleta está definido como não cache, por exemplo), use o [sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md) procedimento armazenado para iniciar o conjunto de coleta.  
  
 Este procedimento habilita os trabalhos de carregamento e de coleta para o conjunto de coleta especificado e iniciará imediatamente o trabalho do agente de coleta, se o conjunto de coleta tiver seu modo de coleta definido como armazenado em cache (0). Para obter mais informações, consulte [sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
 Se o conjunto de coleta não contiver nenhum item de coleta, essa operação não terá nenhum efeito. O erro 14685 é retornado como um aviso.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa dc_operator para executar esse procedimento. Se o conjunto de coleta não tiver uma conta proxy, a associação da função de servidor fixa sysadmin será necessária.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir inicia um conjunto de coleta usando seu identificador.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Coleta de dados](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
