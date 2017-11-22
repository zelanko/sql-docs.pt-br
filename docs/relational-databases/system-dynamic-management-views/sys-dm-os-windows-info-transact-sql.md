---
title: sys.DM os_windows_info (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_os_windows_info
- dm_os_windows_info_TSQL
- sys.dm_os_windows_info
- sys.dm_os_windows_info_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.dm_os_windows_info dynamic management view
ms.assetid: adc81283-fdc2-46c0-bb48-abe82bbf2459
caps.latest.revision: "15"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 759ac050225bdc1abd78a6400152c6ee7f89dcfd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sysdmoswindowsinfo-transact-sql"></a>sys.dm_os_windows_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha que exibe informações de versão de sistema operacional Windows.  
  
  Aplica-se somente ao SQL Server em execução no Windows. Para ver informações semelhantes para SQL Server em execução em um host diferente do Windows, como o Linux, use [sys.dm_os_host_info &#40; Transact-SQL &#41; ](~/relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md). 
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**windows_release**|**nvarchar(256)**|Para Windows, retorna o número de versão. Para obter uma lista de valores e descrições, consulte [versão do sistema operacional (Windows)](http://msdn.microsoft.com/library/ms724832\(VS.85\).aspx). Não pode ser NULL.|  
|**windows_service_pack_level**|**nvarchar(256)**| Para Windows, retorna o número do service pack. Não pode ser NULL. |  
|**windows_sku**|**int**|Para Windows, retorna a ID do estoque mantendo unidade (SKU) do Windows. Para obter uma lista de IDs de SKU e descrições, consulte [função GetProductInfo](http://msdn.microsoft.com/library/ms724358.aspx). É anulável. |  
|**os_language_version**|**int**| Para Windows, retorna o identificador de localidade (LCID) do Windows do sistema operacional. Para obter uma lista de valores LCID e descrições, consulte [IDs de localidade atribuídas pela Microsoft](http://go.microsoft.com/fwlink/?LinkId=208080). Não pode ser NULL.|  
  
  
## <a name="permissions"></a>Permissões  
Por padrão, a permissão SELECT em sys.DM os_windows_info é concedida a função public. Se revogado, requer permissão VIEW SERVER STATE no servidor.  

## <a name="limitations-and-restrictions"></a>Limitações e restrições
Para ver informações de SQL em execução em um host diferente do Windows, como o Linux, use [sys.dm_os_host_info &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md). 
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todas as colunas da **sys.DM os_windows_info** exibição.  
  
```  
SELECT windows_release, windows_service_pack_level, windows_sku, os_language_version  
FROM sys.dm_os_windows_info;  
```  
  
 Este é um exemplo de conjunto de resultados.  
  
 `windows_release  windows_service_pack_level   windows_sku   os_language_version`  
  
 `---------------  ---------------------------  ------------  -------------------`  
  
 `6.0              Service Pack 2                4            1033`  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_host_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md)  
  
  

