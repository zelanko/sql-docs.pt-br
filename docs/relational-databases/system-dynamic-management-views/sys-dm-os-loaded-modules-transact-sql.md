---
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 58f0258843995acc82e84d69a4d2d101594fc313
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820796"
---
# <a name="sysdm_os_loaded_modules-transact-sql"></a>sys.dm_os_loaded_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
|**idioma**|**int**|Idioma das informações de versão do módulo.|  
|**corporativa**|**nvarchar(256)**|Nome da empresa que criou o módulo.|  
|**ndescrição**|**nvarchar(256)**|Descrição do módulo.|  
|**name**|**nvarchar (255)**|Nome do módulo. Inclui o caminho completo do módulo.|  
|**pdw_node_id**|**int**|**Aplica-se ao**: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [SQL Server exibições de gerenciamento dinâmico relacionadas ao sistema operacional &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  
