---
title: sp_syscollector_upload_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_upload_collection_set
- sp_syscollector_upload_collection_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_upload_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: eed9232c-2b0a-4b6a-8ba0-76b7c99f48dc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9017209ef2e4b500ee6a90e14830b520ed2a588d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47780894"
---
# <a name="spsyscollectoruploadcollectionset-transact-sql"></a>sp_syscollector_upload_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia um carregamento de dados do conjunto de coleta se o conjunto de dados estiver habilitado.  
  
> [!IMPORTANT]  
>  Esse procedimento armazenado só pode ser usado para conjuntos de coleta que são configurados para a coleta e o carregamento dos dados em cache.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_upload_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@collection_set_id =** ] *collection_set_id*  
 É o identificador local exclusivo do conjunto de coleta. *collection_set_id* está **int** e deve ter um valor se *nome* é NULL.  
  
 [  **@name =** ] **'***nome***'**  
 É o nome do conjunto de coleta. *nome da* está **sysname** e deve ter um valor se *collection_set_id* é NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Qualquer um dos *collection_set_id* ou *nome* deve ter um valor; ambos não podem ser NULL.  
  
 Este procedimento pode ser usado para iniciar uma carga sob demanda de um conjunto de coleta em execução. Só pode ser usado para conjuntos de coleta configurados para a coleta e o carregamento dos dados em cache. Isto permite que o usuário obtenha dados para analisar sem precisar aguardar um carregamento programado.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na **dc_operator** (com permissão EXECUTE) a função de banco de dados fixa para executar esse procedimento.  
  
## <a name="example"></a>Exemplo  
 Efetua o carregamento sob demanda de um conjunto de coleta chamado `Simple Collection Set`.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_upload_collection_set @name = 'Simple Collection Set' ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
