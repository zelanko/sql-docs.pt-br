---
title: sys. filetable_system_defined_objects (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 118646e7d12940291c0f4f6a79744495e596cf36
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031088"
---
# <a name="sysfiletablesystemdefinedobjects-transact-sql"></a>sys.filetable_system_defined_objects (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe uma lista dos objetos definidos pelo sistema que são relacionados a FileTables. Contém uma linha para cada objeto definido pelo sistema.  
  
 Quando você cria uma FileTable, objetos relacionados, como restrições e índices, são criados ao mesmo tempo. Você não pode alterar ou remover esses objetos. Eles desaparecem apenas quando a própria FileTable é removida.  
  
 Para obter mais informações sobre FileTables, veja [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
|coluna|Data type|Description|  
|------------|---------------|-----------------|  
|**object_id**|**int**|ID do objeto definido pelo sistema relacionado a uma FileTable.<br /><br /> Faz referência ao objeto no **sys. Objects**.|  
|**parent_object_id**|**int**|ID do objeto da FileTable pai.<br /><br /> Faz referência ao objeto no **sys. Objects**.|  
  
## <a name="see-also"></a>Consulte também  
 [Criar, alterar e remover FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md)  
  
  
