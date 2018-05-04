---
title: sys. filetable_system_defined_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.filetable_system_defined_objects_TSQL
- filetable_system_defined_objects
- filetable_system_defined_objects_TSQL
- sys.filetable_system_defined_objects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filetable_system_defined_objects catalog view
ms.assetid: 62022e6b-46f6-495f-b14b-53f41e040361
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 97a5ae542235db8c4992e6d8f2c03f38924543d8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysfiletablesystemdefinedobjects-transact-sql"></a>sys.filetable_system_defined_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe uma lista dos objetos definidos pelo sistema que são relacionados a FileTables. Contém uma linha para cada objeto definido pelo sistema.  
  
 Quando você cria uma FileTable, objetos relacionados, como restrições e índices, são criados ao mesmo tempo. Você não pode alterar ou remover esses objetos. Eles desaparecem apenas quando a própria FileTable é removida.  
  
 Para obter mais informações sobre FileTables, veja [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
|Coluna|Data type|Description|  
|------------|---------------|-----------------|  
|**object_id**|**Int**|ID do objeto definido pelo sistema relacionado a uma FileTable.<br /><br /> Faz referência ao objeto em **sys. Objects**.|  
|**parent_object_id**|**Int**|ID do objeto da FileTable pai.<br /><br /> Faz referência ao objeto em **sys. Objects**.|  
  
## <a name="see-also"></a>Consulte também  
 [Criar, alterar e remover FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
