---
title: MSreplication_options (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSreplication_options
- MSreplication_options_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSreplication_options system table
ms.assetid: 23cf10d7-8bc1-4368-b5eb-e5576421e776
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dafab3a05bc7c5a3d8f819234a2d01f184c1ba5e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47749564"
---
# <a name="msreplicationoptions-transact-sql"></a>MSreplication_options (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSreplication_options** tabela armazena metadados que é usado internamente pela replicação. Essa tabela é armazenada na **mestre** banco de dados.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**optname**|**sysname**|Somente para uso interno.|  
|**value**|**bit**|Somente para uso interno.|  
|**versão_principal**|**int**|Somente para uso interno.|  
|**versão_secundária**|**int**|Somente para uso interno.|  
|**revisão**|**int**|Somente para uso interno.|  
|**install_failures**|**int**|Somente para uso interno.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
