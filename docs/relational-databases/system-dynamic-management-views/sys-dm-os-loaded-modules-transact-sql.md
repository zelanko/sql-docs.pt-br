---
title: sys.dm_os_loaded_modules (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3967e3f8548a7b8ef804d054cf746243a8fb5b96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63047183"
---
# <a name="sysdmosloadedmodules-transact-sql"></a>sys.dm_os_loaded_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha para cada módulo carregado no espaço de endereçamento de servidor.  
  
> [!NOTE]  
>  Chamá-lo partir [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use o nome **sys.dm_pdw_nodes_os_loaded_modules**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**base_address**|**varbinary(8)**|Endereço do módulo no processo.|  
|**file_version**|**varchar(23)**|Versão do arquivo Aparece no seguinte formato:<br /><br /> x.x:x.x|  
|**product_version**|**varchar(23)**|Versão do produto. Aparece no seguinte formato:<br /><br /> x.x:x.x|  
|**debug**|**bit**|1 = O módulo é uma versão de depuração do módulo carregado.|  
|**patched**|**bit**|1 = O módulo foi corrigido.|  
|**prerelease**|**bit**|1 = O módulo é uma versão de pré-lançamento do módulo carregado.|  
|**private_build**|**bit**|1 = O módulo é uma compilação privada do módulo carregado.|  
|**special_build**|**bit**|1 = módulo é uma versão especial do módulo carregado.|  
|**language**|**int**|Idioma das informações de versão do módulo.|  
|**Empresa**|**nvarchar(256)**|Nome da empresa que criou o módulo.|  
|**description**|**nvarchar(256)**|Descrição do módulo.|  
|**name**|**nvarchar(255)**|Nome do módulo. Inclui o caminho completo do módulo.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador para o nó que essa distribuição é no.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Sistema operacional SQL Server relacionados exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
