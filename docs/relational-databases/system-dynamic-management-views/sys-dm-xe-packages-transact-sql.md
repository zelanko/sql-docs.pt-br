---
title: sys.dm_xe_packages (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- dm_xe_packages_TSQL
- sys.dm_xe_packages_TSQL
- dm_xe_packages
- sys.dm_xe_packages
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_packages dynamic management view
- extended events [SQL Server], views
ms.assetid: 2e5ecbe9-3ea8-45e6-a161-e31671a03e1d
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d33b1703f517fbedb746d1a0185e960764603ff5
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmxepackages-transact-sql"></a>sys.dm_xe_packages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista todos os pacotes registrados com o mecanismo de eventos estendido.  
  
 
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(60)**|O nome do pacote. A descrição é exposta no próprio pacote. Não permite valor nulo.|  
|guid|**uniqueidentifier**|O GUID que identifica o pacote. Não permite valor nulo.|  
|descrição|**nvarchar(256)**|A descrição do pacote. descriptionis definido pelo autor do pacote e não é anulável.|  
|funcionalidades|**Int**|Bitmap que descreve os recursos deste pacote. Permite valor nulo.|  
|capabilities_desc|**nvarchar(256)**|Uma lista de todas as funcionalidades possíveis para este pacote. Permite valor nulo.|  
|module_guid|**uniqueidentifier**|O GUID do módulo que expõe este pacote. Não permite valor nulo.|  
|module_address|**varbinary(8)**|O endereço básico onde o módulo que contém o pacote é carregado. Um único módulo pode expor vários pacotes. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="remarks"></a>Remarks  
 Os pacotes registrados com o mecanismo de eventos estendido expõem eventos, as ações que podem ser realizadas na hora do acionamento do evento, e destinos para processamento síncrono e assíncrono de dados de evento.  
  
 Estes pacotes podem ser carregados dinamicamente em um espaço de endereçamento de processo. No momento em que o pacote é carregado, ele registra todos os objetos que expõe, com o mecanismo de eventos estendido.  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
||||  
|-|-|-|  
|De|Para|Relação|  
|sys.dm_xe_packages.module_address|sys.dm_os_loaded_modules.base_address|Muitos para um|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

