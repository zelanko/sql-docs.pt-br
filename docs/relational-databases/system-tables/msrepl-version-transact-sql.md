---
title: MSrepl_version (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSrepl_version
- MSrepl_version_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_version system table
ms.assetid: c1330f03-940b-4564-ac42-6030c6e21173
author: stevestein
ms.author: sstein
ms.openlocfilehash: 45dad1cfaa6057cd50ee4c01b484df8250121a46
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079150"
---
# <a name="msreplversion-transact-sql"></a>MSrepl_version (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSrepl_version** tabela contém uma linha com a versão atual da replicação instalada. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**major_version**|**int**|O número da versão principal do banco de dados de distribuição.|  
|**minor_version**|**int**|O número da versão secundária do banco de dados de distribuição.|  
|**revision**|**int**|O número de revisão.|  
|**db_existed**|**bit**|Indica se o banco de dados de distribuição existe antes **sp_adddistributiondb** é chamado.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
