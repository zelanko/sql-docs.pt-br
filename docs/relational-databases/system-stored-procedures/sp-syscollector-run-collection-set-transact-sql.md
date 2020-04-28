---
title: sp_syscollector_run_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_run_collection_set_TSQL
- sp_syscollector_run_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_run_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 7bbaee48-dfc7-45c0-b11f-c636b6a7e720
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3807a53921572bbe20b4c459bff34958cbb42001
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72305000"
---
# <a name="sp_syscollector_run_collection_set-transact-sql"></a>sp_syscollector_run_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia um conjunto de coleta se o coletor já estiver habilitado e o conjunto de coleta estiver configurado para o modo de coleta sem armazenamento em cache.  
  
> [!NOTE]  
>  Este procedimento falhará se for executado em um conjunto de coleta configurado para o modo de coleta em cache.  
  
 sp_syscollector_run_collection_set permite que um usuário tire instantâneos de dados sob demanda.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_run_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @collection_set_id = ] collection_set_id`É o identificador local exclusivo para o conjunto de coleta. *collection_set_id* é **int** e deve ter um valor se *Name* for NULL.  
  
`[ @name = ] 'name'`É o nome do conjunto de coleta. o *nome* é **sysname** e deve ter um valor se *collection_set_id* for NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 O *collection_set_id* ou o *nome* deve ter um valor, ambos não podem ser nulos.  
  
 Este procedimento iniciará a coleta e carregará trabalhos para o conjunto de coleta especificado e iniciará imediatamente o trabalho do agente de coleta se o conjunto de coleta tiver seu ** \@collection_mode** definido como não armazenado em cache (1). Para obter mais informações, consulte [sp_syscollector_create_collection_set &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
 sp_sycollector_run_collection_set também pode ser usado para executar um conjunto de coleta que não tenha uma agenda.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa **dc_operator** (com permissão de execução) para executar este procedimento.  
  
## <a name="example"></a>Exemplo  
 Inicia um conjunto de coleta usando seu identificador.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_run_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de dados](../../relational-databases/data-collection/data-collection.md)  
  
  
