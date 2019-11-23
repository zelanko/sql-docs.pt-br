---
title: sys. dm_io_backup_tapes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 98902f096bb960436d764416e2563af5056f00dd
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874151"
---
# <a name="sysdm_io_backup_tapes-transact-sql"></a>sys.dm_io_backup_tapes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna a lista de dispositivos de fita e o estado de solicitações de montagem para backups.   
 
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**physical_device_name**|**nvarchar(520)**|Nome do dispositivo físico atual no qual um backup pode ser realizado. Não permite valor nulo.|  
|**logical_device_name**|**nvarchar(256)**|Nome especificado pelo usuário para a unidade (a partir de **Sys. backup_devices**). NULL se nenhum nome especificado pelo usuário estiver disponível. Permite valor nulo.|  
|**status**|**int**|Status da fita.<br /><br /> 1 = Aberta, disponível para uso<br /><br /> 2 = Montagem pendente<br /><br /> 3 = Em uso<br /><br /> 4 = Carregando<br /><br /> **Observação:** Enquanto uma fita está sendo carregada (**status = 4**), o rótulo de mídia ainda não é lido. Colunas que copiam valores de rótulo de mídia, como **media_sequence_number**, mostram valores previstos, que podem ser diferentes dos valores reais na fita. Depois que o rótulo tiver sido lido, o **status** será alterado para **3** (em uso) e as colunas de rótulo de mídia refletirão a fita real que é carregada.<br /><br /> Não permite valor nulo.|  
|**status_desc**|**nvarchar(520)**|Descrição do status da fita:<br /><br /> AVAILABLE<br /><br /> MOUNT PENDING<br /><br /> IN USE<br /><br /> LOADING MEDIA<br /><br /> Não permite valor nulo.|  
|**mount_request_time**|**datetime**|Hora em que a montagem foi solicitada. NULL se nenhuma montagem estiver pendente (**status! = 2**). Permite valor nulo.|  
|**mount_expiration_time**|**datetime**|Hora em que o pedido de montagem expirará (tempo limite). NULL se nenhuma montagem estiver pendente (**status! = 2**). Permite valor nulo.|  
|**database_name**|**nvarchar(256)**|Banco de dados do qual será feito o backup neste dispositivo. Permite valor nulo.|  
|**spid**|**int**|ID da sessão. Identificação do usuário da fita. Permite valor nulo.|  
|**command**|**int**|Comando que executa o backup. Permite valor nulo.|  
|**command_desc**|**nvarchar(120)**|Descrição do comando. Permite valor nulo.|  
|**media_family_id**|**int**|Índice da família de mídias (1... *n*), *n* é o número de famílias de mídia no conjunto de mídias. Permite valor nulo.|  
|**media_set_name**|**nvarchar(256)**|Nome do conjunto de mídias (caso haja) como especificado pela opção de MEDIANAME, quando o conjunto de mídias foi criado. Permite valor nulo.|  
|**media_set_guid**|**uniqueidentifier**|Identificador que identifica exclusivamente o conjunto de mídias. Permite valor nulo.|  
|**media_sequence_number**|**int**|Índice de volume em uma família de mídia (1. *.. n*). Permite valor nulo.|  
|**tape_operation**|**int**|Operação de fita que está sendo executada:<br /><br /> 1 = Leitura<br /><br /> 2 = Formato<br /><br /> 3 = Inicialização<br /><br /> 4 = Acréscimo<br /><br /> Permite valor nulo.|  
|**tape_operation_desc**|**nvarchar(120)**|Operação de fita que está sendo executada:<br /><br /> READ<br /><br /> FORMAT<br /><br /> INIT<br /><br /> APPEND<br /><br /> Permite valor nulo.|  
|**mount_request_type**|**int**|Tipo de pedido de montagem:<br /><br /> 1 = Fita específica. A fita identificada pelo **media_\*** campos é necessário.<br /><br /> 2 = Próxima família de mídias. A família de mídia seguinte ainda não restaurada é solicitada. Isso é usado ao restaurar com um número menor de dispositivos do que há de famílias de mídia.<br /><br /> 3 = Fita de continuação. A família de mídia está sendo estendida, e uma fita de continuação é solicitada.<br /><br /> Permite valor nulo.|  
|**mount_request_type_desc**|**nvarchar(120)**|Tipo de pedido de montagem:<br /><br /> SPECIFIC TAPE<br /><br /> NEXT MEDIA FAMILY<br /><br /> CONTINUATION VOLUME<br /><br /> Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão VIEW SERVER STATE, no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições e funções &#40;de gerenciamento dinâmico relacionadas a e/s do TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

