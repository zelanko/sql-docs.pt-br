---
title: sys.DM os_loaded_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_os_loaded_modules
- dm_os_loaded_modules
- sys.dm_os_loaded_modules_TSQL
- dm_os_loaded_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_loaded_modules dynamic management view
ms.assetid: 56c7743a-b568-4943-bd3b-73c57d9d641c
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1888f39f6024a0b299834217c2f8b69052761b65
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmosloadedmodules-transact-sql"></a>sys.dm_os_loaded_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada módulo carregado no espaço de endereçamento de servidor.  
  
> [!NOTE]  
>  Para chamar essa de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_loaded_modules**.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**base_address**|**varbinary(8)**|Endereço do módulo no processo.|  
|**file_version**|**varchar(23)**|Versão do arquivo Aparece no seguinte formato:<br /><br /> x.x:x.x|  
|**product_version**|**varchar(23)**|Versão do produto. Aparece no seguinte formato:<br /><br /> x.x:x.x|  
|**Depurar**|**bit**|1 = O módulo é uma versão de depuração do módulo carregado.|  
|**corrigido**|**bit**|1 = O módulo foi corrigido.|  
|**prerelease**|**bit**|1 = O módulo é uma versão de pré-lançamento do módulo carregado.|  
|**private_build**|**bit**|1 = O módulo é uma compilação privada do módulo carregado.|  
|**special_build**|**bit**|1 = módulo é uma versão especial do módulo carregado.|  
|**language**|**Int**|Idioma das informações de versão do módulo.|  
|**Empresa**|**nvarchar(256)**|Nome da empresa que criou o módulo.|  
|**Descrição**|**nvarchar(256)**|Descrição do módulo.|  
|**name**|**nvarchar(255)**|Nome do módulo. Inclui o caminho completo do módulo.|  
|**pdw_node_id**|**Int**|**Aplica-se ao**: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sistema operacional SQL Server relacionadas exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
