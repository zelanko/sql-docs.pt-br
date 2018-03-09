---
title: sys.sysperfinfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-compatibility-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysperfinfo_TSQL
- sys.sysperfinfo_TSQL
- sys.sysperfinfo
- sysperfinfo
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysperfinfo compatibility view
- sysperfinfo system table
ms.assetid: e22a81cd-27de-4690-9443-6aad6393bd3c
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 92d1cb29e339017f13c5b784f2b1459cf1a19432
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
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
|**instance_name**|**nchar(128)**|Instância nomeada do contador. Por exemplo, há contadores mantidos para cada tipo de bloqueio, como **tabela**, **página**, **chave**, e assim por diante. O nome de instância distingue contadores semelhantes.|  
|**cntr_value**|**bigint**|Valor de contador real. Com frequência, será um contador que aumenta de forma monotônica ou de nível que conta ocorrências do evento de instância.|  
|**cntr_type**|**Int**|Tipo de contador conforme definido pela arquitetura de desempenho do Windows.|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
