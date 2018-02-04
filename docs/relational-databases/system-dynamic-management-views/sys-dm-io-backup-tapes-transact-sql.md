---
title: sys.dm_io_backup_tapes (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
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
- sys.dm_io_backup_tapes
- dm_io_backup_tapes_TSQL
- sys.dm_io_backup_tapes_TSQL
- dm_io_backup_tapes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_io_backup_tapes dynamic management view
ms.assetid: 2e27489e-cf69-4a89-9036-77723ac3de66
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 80f1fdab524409956921aa9087177b2ef9d8ae7f
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmiobackuptapes-transact-sql"></a>sys.dm_io_backup_tapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna a lista de dispositivos de fita e o estado de solicitações de montagem para backups.   
 
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**physical_device_name**|**nvarchar(520)**|Nome do dispositivo físico atual no qual um backup pode ser realizado. Não permite valor nulo.|  
|**logical_device_name**|**nvarchar(256)**|Nome de usuário especificado para a unidade (de **backup_devices**). NULL se nenhum nome especificado pelo usuário estiver disponível. Permite valor nulo.|  
|**status**|**Int**|Status da fita.<br /><br /> 1 = Aberta, disponível para uso<br /><br /> 2 = Montagem pendente<br /><br /> 3 = Em uso<br /><br /> 4 = Carregando<br /><br /> **Observação:** enquanto uma fita está sendo carregada (**status = 4**), o rótulo de mídia não foi lido ainda. Colunas que copiam valores de rótulo de mídia, tais como **media_sequence_number**, exibem valores antecipados que podem ser diferentes dos valores atuais na fita. Depois que o rótulo foi lido, **status** alterações **3** (em uso), e as colunas de rótulo de mídia refletem a fita atual que é carregada.<br /><br /> Não permite valor nulo.|  
|**status_desc**|**nvarchar(520)**|Descrição do status da fita:<br /><br /> AVAILABLE<br /><br /> MOUNT PENDING<br /><br /> IN USE<br /><br /> LOADING MEDIA<br /><br /> Não permite valor nulo.|  
|**mount_request_time**|**datetime**|Hora em que a montagem foi solicitada. NULL se nenhuma montagem estiver pendente (**status! = 2**). Permite valor nulo.|  
|**mount_expiration_time**|**datetime**|Hora em que o pedido de montagem expirará (tempo limite). NULL se nenhuma montagem estiver pendente (**status! = 2**). Permite valor nulo.|  
|**database_name**|**nvarchar(256)**|Banco de dados do qual será feito o backup neste dispositivo. Permite valor nulo.|  
|**spid**|**Int**|ID da sessão. Identificação do usuário da fita. Permite valor nulo.|  
|**command**|**Int**|Comando que executa o backup. Permite valor nulo.|  
|**command_desc**|**nvarchar(120)**|Descrição do comando. Permite valor nulo.|  
|**media_family_id**|**Int**|Índice de família de mídia (1... *n* ),  *n*  é o número de famílias de mídia no conjunto de mídias. Permite valor nulo.|  
|**media_set_name**|**nvarchar(256)**|Nome do conjunto de mídias (caso haja) como especificado pela opção de MEDIANAME, quando o conjunto de mídias foi criado. Permite valor nulo.|  
|**media_set_guid**|**uniqueidentifier**|Identificador que identifica exclusivamente o conjunto de mídias. Permite valor nulo.|  
|**media_sequence_number**|**Int**|Índice de volume dentro de uma família de mídia (1... *n*). Permite valor nulo.|  
|**tape_operation**|**Int**|Operação de fita que está sendo executada:<br /><br /> 1 = Leitura<br /><br /> 2 = Formato<br /><br /> 3 = Inicialização<br /><br /> 4 = Acréscimo<br /><br /> Permite valor nulo.|  
|**tape_operation_desc**|**nvarchar(120)**|Operação de fita que está sendo executada:<br /><br /> READ<br /><br /> FORMAT<br /><br /> INIT<br /><br /> APPEND<br /><br /> Permite valor nulo.|  
|**mount_request_type**|**Int**|Tipo de pedido de montagem:<br /><br /> 1 = Fita específica. A fita identificada pelo **Media\***  campos é necessária.<br /><br /> 2 = Próxima família de mídias. A família de mídia seguinte ainda não restaurada é solicitada. Isso é usado ao restaurar com um número menor de dispositivos do que há de famílias de mídia.<br /><br /> 3 = Fita de continuação. A família de mídia está sendo estendida, e uma fita de continuação é solicitada.<br /><br /> Permite valor nulo.|  
|**mount_request_type_desc**|**nvarchar(120)**|Tipo de pedido de montagem:<br /><br /> SPECIFIC TAPE<br /><br /> NEXT MEDIA FAMILY<br /><br /> CONTINUATION VOLUME<br /><br /> Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão VIEW SERVER STATE, no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Eu O relacionados funções e exibições de gerenciamento dinâmico &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

