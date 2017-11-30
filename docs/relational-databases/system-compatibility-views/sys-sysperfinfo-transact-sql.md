---
title: sys. sysperfinfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysperfinfo_TSQL
- sys.sysperfinfo_TSQL
- sys.sysperfinfo
- sysperfinfo
dev_langs: TSQL
helpviewer_keywords:
- sys.sysperfinfo compatibility view
- sysperfinfo system table
ms.assetid: e22a81cd-27de-4690-9443-6aad6393bd3c
caps.latest.revision: "40"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 45b45736c76ec0da7f1dce103df9fea4ee22507a
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="syssysperfinfo-transact-sql"></a>sys.sysperfinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] representação dos contadores de desempenho internos que podem ser exibidos por meio do Monitor do sistema do Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|Desempenho do objeto, como nome, **SQLServer:LockManager** ou **SQLServer:BufferManager**.|  
|**counter_name**|**nchar(128)**|Nome do contador de desempenho dentro do objeto, como **solicitações de páginas** ou **bloqueios solicitados**.|  
|**nome_da_instância**|**nchar(128)**|Instância nomeada do contador. Por exemplo, há contadores mantidos para cada tipo de bloqueio, como **tabela**, **página**, **chave**, e assim por diante. O nome de instância distingue contadores semelhantes.|  
|**cntr_value**|**bigint**|Valor de contador real. Com frequência, será um contador que aumenta de forma monotônica ou de nível que conta ocorrências do evento de instância.|  
|**cntr_type**|**int**|Tipo de contador conforme definido pela arquitetura de desempenho do Windows.|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
