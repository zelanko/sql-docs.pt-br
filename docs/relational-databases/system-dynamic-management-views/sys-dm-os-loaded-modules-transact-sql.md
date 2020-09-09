---
description: sys.dm_os_loaded_modules (Transact-SQL)
title: sys. dm_os_loaded_modules (Transact-SQL) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: af93d167af59eb95b4a1edd83109eebbd12782c7
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542154"
---
# <a name="sysdm_os_loaded_modules-transact-sql"></a>sys.dm_os_loaded_modules (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada módulo carregado no espaço de endereçamento de servidor.  
  
> [!NOTE]  
>  Para chamá-lo de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , use o nome **sys. dm_pdw_nodes_os_loaded_modules**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**base_address**|**varbinary (8)**|Endereço do módulo no processo.|  
|**file_version**|**varchar (23)**|Versão do arquivo Aparece no seguinte formato:<br /><br /> x.x:x.x|  
|**product_version**|**varchar (23)**|Versão do produto. Aparece no seguinte formato:<br /><br /> x.x:x.x|  
|**verificação**|**bit**|1 = O módulo é uma versão de depuração do módulo carregado.|  
|**patched**|**bit**|1 = O módulo foi corrigido.|  
|**pré-lançamento**|**bit**|1 = O módulo é uma versão de pré-lançamento do módulo carregado.|  
|**private_build**|**bit**|1 = O módulo é uma compilação privada do módulo carregado.|  
|**special_build**|**bit**|1 = o módulo é uma compilação especial do módulo carregado.|  
|**linguagem**|**int**|Idioma das informações de versão do módulo.|  
|**corporativa**|**nvarchar(256)**|Nome da empresa que criou o módulo.|  
|**descrição**|**nvarchar(256)**|Descrição do módulo.|  
|**name**|**nvarchar(255)**|Nome do módulo. Inclui o caminho completo do módulo.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
