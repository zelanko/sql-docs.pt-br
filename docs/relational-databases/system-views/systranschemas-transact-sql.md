---
title: systranschemas (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- systranschemas
- systranschemas_TSQL
dev_langs: TSQL
helpviewer_keywords: systranschemas system table
ms.assetid: 864c3966-cb61-4f2b-8939-ccda112de853
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f5f5c9502b9116bc60797c537edb27fdf79d3080
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="systranschemas-transact-sql"></a>systranschemas (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **systranschemas** tabela é usada para controlar as alterações de esquema em artigos publicados em publicações transacionais e de instantâneo. Essa tabela é armazenada nos bancos de dados de assinatura e publicação.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**tabid**|**int**|Identifica o artigo de tabela em que a alteração de esquema ocorreu.|  
|**startlsn**|**binary**|Valor LSN no início da alteração de esquema.|  
|**endlsn**|**binary**|Valor LSN no fim da alteração de esquema.|  
|**TypeId**|**int**|Tipo de alteração de esquema.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
