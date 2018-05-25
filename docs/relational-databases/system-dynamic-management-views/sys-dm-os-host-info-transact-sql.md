---
title: sys.dm_os_host_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sys.dm_os_host_info
- sys.dm_os_host_info_TSQL
- dm_os_host_info
- dm_os_host_info_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_host_info dynamic management view
ms.assetid: 9bb6ef86-957b-4ca1-ad20-ca2f8460a86d
caps.latest.revision: 9
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 0aa5f28f52c9d0df4e942809612e1ca59a1cb3c5
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmoshostinfo-transact-sql"></a>sys.dm_os_host_info (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Retorna uma linha que exibe informações de versão do sistema operacional.  
  
|Nome da coluna |Tipo de dados |Description |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |O tipo de sistema operacional: Windows ou Linux |
|**host_distribution** |**nvarchar(256)** |Descrição do sistema operacional. |
|**host_release**|**nvarchar(256)**|Versão do sistema operacional [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (número da versão). Para obter uma lista de valores e descrições, consulte [versão do sistema operacional (Windows)](http://msdn.microsoft.com/library/ms724832\(VS.85\).aspx). <br> Para o Linux, retorna uma cadeia de caracteres vazia. |  
|**host_service_pack_level**|**nvarchar(256)**|Nível de service pack do sistema operacional Windows. <br> Para o Linux, retorna uma cadeia de caracteres vazia. |  
|**host_sku**|**Int**|ID da SKU (Stock Keeping Unit, unidade de manutenção de estoque) do Windows. Para obter uma lista de IDs de SKU e descrições, consulte [função GetProductInfo](http://msdn.microsoft.com/library/ms724358.aspx). Permite valor nulo. <br> Para o Linux, retorna NULL. |  
|**os_language_version**|**Int**|LCID (locale identifier, ID de localidade) do sistema operacional. Para obter uma lista de valores LCID e descrições, consulte [IDs de localidade atribuídas pela Microsoft](http://go.microsoft.com/fwlink/?LinkId=208080). Não pode ser nulo.|  

## <a name="remarks"></a>Remarks  
Essa exibição é semelhante ao [sys.DM os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md), adição de colunas para diferenciar o Windows e Linux.
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
O `SELECT` permissão `sys.dm_os_host_info` é concedida para o `public` função por padrão. Se revogado, requer `VIEW SERVER STATE` permissão no servidor.   
 
>  [!CAUTION]
>  Começando com a versão [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] CTP 1.3, [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] requer a versão 17 `SELECT` permissão `sys.dm_os_host_info` para se conectar a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Se `SELECT` permissão é revogada de `public`, somente logons com `VIEW SERVER STATE` permissão pode se conectar com a versão mais recente do SSMS. (Outras ferramentas, como `sqlcmd.exe` podem se conectar sem `SELECT` permissão em `sys.dm_os_host_info`.)

  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todas as colunas da **sys.dm_os_host_info** exibição.  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

Aqui está um exemplo conjunto de resultados no Windows:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |1046 |  

Aqui está um exemplo conjunto de resultados no Linux:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULL   |1046 |  

  
## <a name="see-also"></a>Consulte também  
 [sys.dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 

