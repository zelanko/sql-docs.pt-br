---
title: MSdynamicsnapshotviews (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdynamicsnapshotviews_TSQL
- MSdynamicsnapshotviews
dev_langs:
- TSQL
helpviewer_keywords:
- MSdynamicsnapshotviews system table
ms.assetid: 4fc1822a-5d6e-4034-a2e2-363210232d3b
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8de7dd1571f7b9082144e97c8b35d9a39d6cabe8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67907319"
---
# <a name="msdynamicsnapshotviews-transact-sql"></a>MSdynamicsnapshotviews (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSdynamicsnapshotviews** tabela rastreia todas as exibições de instantâneo de dados filtrados temporário criadas pelo snapshot agent e é usada pelo sistema para limpar exibições no caso de um desligamento anormal do SQL Server Agent ou o Agente de instantâneo. Essa tabela é armazenada nos bancos de dados da publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**dynamic_snapshot_view_name**|**sysname**|O nome da exibição temporária do instantâneo de dados filtrado.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
