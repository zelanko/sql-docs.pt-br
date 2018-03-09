---
title: sys.sysfiles (Transact-SQL) | Microsoft Docs
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
- sysfiles
- sys.sysfiles_TSQL
- sys.sysfiles
- sysfiles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysfiles system table
- sys.sysfiles compatibility view
ms.assetid: 3b47f38d-1cff-404d-89d3-9342c451c802
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 46f241ec9402dc275f265419344bc2e3ccf4d007
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="syssysfiles-transact-sql"></a>sys.sysfiles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada arquivo em um banco de dados.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**fileid**|**smallint**|Número de identificação do arquivo exclusivo para cada banco de dados.|  
|**groupid**|**smallint**|Número de identificação do grupo de arquivos.|  
|**size**|**Int**|Tamanho do arquivo, em páginas de 8 KB.|  
|**maxsize**|**Int**|Tamanho de arquivo máximo, em páginas de 8 KB.<br /><br /> 0 = Sem crescimento.<br /><br /> -1 = Arquivo crescerá até que o disco esteja completo.<br /><br /> 268435456 = Arquivo de log crescerá a um tamanho máximo de 2 TB.<br /><br /> Observação: Bancos de dados que são atualizados com um tamanho de arquivo de log ilimitado informarão -1 para o tamanho máximo do arquivo de log.|  
|**growth**|**Int**|Tamanho de crescimento do banco de dados. Pode ser o número de páginas ou a porcentagem do tamanho do arquivo, dependendo do valor de **status**.<br /><br /> 0 = Sem crescimento.|  
|**status**|**Int**|Bits de status para o **crescimento** valor em megabytes (MB) ou kilobytes (KB).<br /><br /> 0x2 = Arquivo de disco.<br /><br /> 0x40 = Arquivo de log<br /><br /> 0x100000 = Crescimento. Este valor é uma porcentagem e não o número de páginas.|  
|**perf**|**Int**|Reservado.|  
|**name**|**sysname**|Nome lógico do arquivo.|  
|**filename**|**nvarchar(260)**|Nome do dispositivo físico. Isso inclui o caminho completo do arquivo.|  
  
## <a name="see-also"></a>Consulte também  
 [Mapeando tabelas do sistema para exibições do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
