---
title: sys. dm_xe_packages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a70105791ed9c6dea0371bd941dcae185ab05b2d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898597"
---
# <a name="sysdm_xe_packages-transact-sql"></a>sys.dm_xe_packages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Lista todos os pacotes registrados com o mecanismo de eventos estendido.  
  
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|name|**nvarchar(256)**|O nome do pacote. A descrição é exposta no próprio pacote. Não permite valor nulo.|  
|guid|**uniqueidentifier**|O GUID que identifica o pacote. Não permite valor nulo.|  
|descrição|**nvarchar (3072)**|A descrição do pacote. a descrição é definida pelo autor do pacote e não permite valor nulo.|  
|funcionalidades|**int**|Bitmap que descreve os recursos deste pacote. Permite valor nulo.|  
|capabilities_desc|**nvarchar(256)**|Uma lista de todas as funcionalidades possíveis para este pacote. Permite valor nulo.|  
|module_guid|**nvarchar(60)**|O GUID do módulo que expõe este pacote. Não permite valor nulo.|  
|module_address|**varbinary (8)**|O endereço básico onde o módulo que contém o pacote é carregado. Um único módulo pode expor vários pacotes. Não permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="remarks"></a>Comentários  
 Os pacotes registrados com o mecanismo de eventos estendido expõem eventos, as ações que podem ser realizadas na hora do acionamento do evento, e destinos para processamento síncrono e assíncrono de dados de evento.  
  
 Estes pacotes podem ser carregados dinamicamente em um espaço de endereçamento de processo. No momento em que o pacote é carregado, ele registra todos os objetos que expõe, com o mecanismo de eventos estendido.  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relações  
  
||||  
|-|-|-|  
|De|Para|Relação|  
|sys.dm_xe_packages.module_address|sys.dm_os_loaded_modules.base_address|Muitos para um|  
  
## <a name="see-also"></a>Confira também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

