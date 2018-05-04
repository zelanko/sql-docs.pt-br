---
title: sys.dm_pdw_network_credentials (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.service: ''
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2f3456427ef31af27d6edf64077b2a485c585f01
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
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
  
  
