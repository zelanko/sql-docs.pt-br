---
title: sys.dm_os_windows_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_windows_info
- dm_os_windows_info_TSQL
- sys.dm_os_windows_info
- sys.dm_os_windows_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_windows_info dynamic management view
ms.assetid: adc81283-fdc2-46c0-bb48-abe82bbf2459
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b61127c2844117b2d9c042b352129a1860e227c6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47743184"
---
# <a name="sysdmoswindowsinfo-transact-sql"></a>sys.dm_os_windows_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha que exibe informações de versão de sistema operacional Windows.  
  
  Aplica-se somente ao SQL Server em execução no Windows. Para ver informações semelhantes para o SQL Server em execução em um host não Windows, como o Linux, use [DM os_host_info &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md). 
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**windows_release**|**nvarchar(256)**|Para Windows, retorna o número de versão. Para obter uma lista de valores e descrições, consulte [versão do sistema operacional (Windows)](/windows/desktop/SysInfo/operating-system-version). Não pode ser NULL.|  
|**windows_service_pack_level**|**nvarchar(256)**| Para Windows, retorna o número do service pack. Não pode ser NULL. |  
|**windows_sku**|**int**|Para Windows, retorna a ID do Windows estoque mantendo SKU (unidade). Para obter uma lista de IDs e descrições, consulte [função GetProductInfo](http://msdn.microsoft.com/library/ms724358.aspx). É anulável. |  
|**os_language_version**|**int**| Para Windows, retorna o identificador de localidade (LCID) do Windows do sistema operacional. Para obter uma lista de valores LCID e descrições, consulte [IDs de localidade atribuídas pela Microsoft](http://go.microsoft.com/fwlink/?LinkId=208080). Não pode ser NULL.|  
  
  
## <a name="permissions"></a>Permissões  
Por padrão, a permissão SELECT no sys.dm_os_windows_info é concedida à função pública. Se revogado, requer a permissão VIEW SERVER STATE no servidor.  

## <a name="limitations-and-restrictions"></a>Limitações e restrições
Para ver informações para o SQL em execução em um host não Windows, como o Linux, use [DM os_host_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-host-info-transact-sql.md). 
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todas as colunas do **sys.dm_os_windows_info** exibição.  
  
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
  
  

