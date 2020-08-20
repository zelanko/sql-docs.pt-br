---
description: sys. dm_os_host_info (Transact-SQL)
title: sys. dm_os_host_info (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/10/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eb99e12c75a3f10ca88dc7668d194840f360be2e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489815"
---
# <a name="sysdm_os_host_info-transact-sql"></a>sys. dm_os_host_info (Transact-SQL)
[!INCLUDE[SQL Server 2017](../../includes/applies-to-version/sqlserver2017.md)]

Retorna uma linha que exibe informações de versão do sistema operacional.  
  
|Nome da coluna |Tipo de dados |Descrição |  
|-----------------|---------------|-----------------|  
|**host_platform** |**nvarchar(256)** |O tipo de sistema operacional: Windows ou Linux |
|**host_distribution** |**nvarchar(256)** |Descrição do sistema operacional. |
|**host_release**|**nvarchar(256)**|Versão do sistema operacional [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows (número da versão). Para obter uma lista de valores e descrições, consulte [versão do sistema operacional (Windows)](/windows/desktop/SysInfo/operating-system-version). <br> Para o Linux, retorna uma cadeia de caracteres vazia. |  
|**host_service_pack_level**|**nvarchar(256)**|Nível de service pack do sistema operacional Windows. <br> Para o Linux, retorna uma cadeia de caracteres vazia. |  
|**host_sku**|**int**|ID da SKU (Stock Keeping Unit, unidade de manutenção de estoque) do Windows. Para obter uma lista de IDs e descrições de SKU, consulte a [função GetProductInfo](https://msdn.microsoft.com/library/ms724358.aspx). Permite valor nulo. <br> Para o Linux, retorna NULL. |  
|**os_language_version**|**int**|LCID (locale identifier, ID de localidade) do sistema operacional. Para obter uma lista de valores e descrições de LCID, consulte [IDs de localidade atribuídas pela Microsoft](https://go.microsoft.com/fwlink/?LinkId=208080). Não pode ser nulo.|  

## <a name="remarks"></a>Comentários  
Essa exibição é semelhante a [Sys. dm_os_windows_info](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md), adicionando colunas para diferenciar o Windows e o Linux.
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
A `SELECT` permissão on `sys.dm_os_host_info` é concedida à `public` função por padrão. Se revogado, requer `VIEW SERVER STATE` permissão no servidor.   
 
> [!CAUTION]
>  A partir [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] da versão CTP 1,3, [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] a versão 17 requer `SELECT` permissão on para `sys.dm_os_host_info` se conectar ao [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] . Se `SELECT` a permissão for revogada de `public` , somente os logons com `VIEW SERVER STATE` permissão poderão se conectar com a versão mais recente do SSMS. (Outras ferramentas, como o `sqlcmd.exe` podem se conectar sem `SELECT` permissão em `sys.dm_os_host_info` .)

  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna todas as colunas da exibição **Sys. dm_os_host_info** .  
  
```  
SELECT host_platform, host_distribution, host_release, 
    host_service_pack_level, host_sku, os_language_version  
FROM sys.dm_os_host_info;  
```  

Veja um exemplo de conjunto de resultados no Windows:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Windows   |Windows Server 2012 R2 Standard    |6.3    |   |7  |1046 |  

Veja um exemplo de conjunto de resultados no Linux:
 
 |host_platform |host_distribution |host_release |host_service_pack_level |host_sku |os_language_version |
 |----- |----- |----- |----- |----- |----- |
 |Linux |Ubuntu |16.04  |   |NULO   |1046 |  

  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_os_sys_info &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-sys-info-transact-sql.md)   
 [sys.dm_os_windows_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-windows-info-transact-sql.md)  
 

