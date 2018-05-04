---
title: sys. sysmembers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sysmembers_TSQL
- sysmembers
- sys.sysmembers
- sysmembers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmembers system table
- sys.sysmembers compatibility view
ms.assetid: ceb18341-f985-4849-ac83-21d67ab7b980
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 46340243b5f1c176625a7c4ab6c2681c400137ae
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="syssysmembers-transact-sql"></a>sys.sysmembers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada membro de uma função de banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**memberuid**|**smallint**|ID do usuário do membro da função. Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.|  
|**groupuid**|**smallint**|ID do usuário da função. Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
