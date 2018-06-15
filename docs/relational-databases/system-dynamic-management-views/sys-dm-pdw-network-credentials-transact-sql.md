---
title: sys.dm_pdw_network_credentials (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: e7b4534410eabf1186b115c07fef8a8d79960938
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34466702"
---
# <a name="sysdmpdwnetworkcredentials-transact-sql"></a>sys.dm_pdw_network_credentials (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Retorna uma lista de todas as credenciais de rede armazenada no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] dispositivo para todos os servidores de destino. Resultados são listados para o nó de controle e cada nó de computação.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**Int**|Id numérico exclusivo associado ao nó.|  
|target_server_name|**nvarchar(32)**|Endereço IP do servidor de destino que [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] terão acesso usando as credenciais de usuário e senha.|  
|username|**nvarchar(32)**|O nome de usuário para o qual a senha é armazenada.|  
|LAST_MODIFIED|**datetime**|Data e hora da última operação que modificou a credencial.|  
  
## <a name="permissions"></a>Permissões  
 Requer VIEW SERVER STATE.  
  
## <a name="general-remarks"></a>Comentários gerais  
 A chave para este modo de exibição de gerenciamento dinâmico é *pdw_node_id* mais *target_server_name*.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Data Warehouse Parallel Data Warehouse e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
