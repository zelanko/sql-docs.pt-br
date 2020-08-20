---
description: sys.sysperfinfo (Transact-SQL)
title: sys.sysperfinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1122c224e21fa633c2c04cd156a49878fefc7daa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482094"
---
# <a name="syssysperfinfo-transact-sql"></a>sys.sysperfinfo (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] representação dos contadores de desempenho internos que podem ser exibidos por meio do monitor do sistema do Windows.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|Nome do objeto de desempenho, como **SqlServer: LockManager** ou **SqlServer: BufferManager**.|  
|**counter_name**|**nchar(128)**|Nome do contador de desempenho no objeto, como solicitações de **página** ou **bloqueios solicitados**.|  
|**instance_name**|**nchar(128)**|Instância nomeada do contador. Por exemplo, há contadores mantidos para cada tipo de bloqueio, como **tabela**, **página**, **chave**e assim por diante. O nome de instância distingue contadores semelhantes.|  
|**cntr_value**|**bigint**|Valor de contador real. Com frequência, será um contador que aumenta de forma monotônica ou de nível que conta ocorrências do evento de instância.|  
|**cntr_type**|**int**|Tipo de contador conforme definido pela arquitetura de desempenho do Windows.|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
