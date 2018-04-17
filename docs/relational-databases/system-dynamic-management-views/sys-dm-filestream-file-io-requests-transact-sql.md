---
title: sys.DM filestream_file_io_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_filestream_file_io_requests
- dm_filestream_file_io_requests
- sys.dm_filestream_file_io_requests_TSQL
- dm_filestream_file_io_requests_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_file_io_requests catalog view
ms.assetid: d41e39a5-14d5-4f3d-a2e3-a822b454c1ed
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0e2115473a557df341cb1e1244d4b6378a69c15b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmfilestreamfileiorequests-transact-sql"></a>sys.dm_filestream_file_io_requests (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe uma lista de solicitações de E/S sendo processadas NSO (proprietário do namespace) no momento determinado.  
  
|Coluna|Tipo|Description|  
|------------|----------|-----------------|  
|**request_context_address**|**varbinary(8)**|Mostra o endereço interno do bloco memória NSO que contém a solicitação de E/S do driver. Não permite valor nulo.|  
|**current_spid**|**smallint**|Mostra a SPID (ID de processo) da conexão atual do SQL Server. Não permite valor nulo.|  
|**request_type**|**nvarchar(60)**|Mostra o tipo de IRP (pacote de solicitação de E/S). Os possíveis tipos de solicitação são: REQ_PRE_CREATE, REQ_POST_CREATE, REQ_RESOLVE_VOLUME, REQ_GET_VOLUME_INFO, REQ_GET_LOGICAL_NAME, REQ_GET_PHYSICAL_NAME, REQ_PRE_CLEANUP, REQ_POST_CLEANUP, REQ_CLOSE, REQ_FSCTL, REQ_QUERY_INFO, REQ_SET_INFO, REQ_ENUM_DIRECTORY, REQ_QUERY_SECURITY e REQ_SET_SECURITY. Não permite valor nulo|  
|**request_state**|**nvarchar(60)**|Mostra o estado da solicitação de E/S no NSO. Os valores possível são: REQ_STATE_RECEIVED, REQ_STATE_INITIALIZED, REQ_STATE_ENQUEUED, REQ_STATE_PROCESSING, REQ_STATE_FORMATTING_RESPONSE, REQ_STATE_SENDING_RESPONSE, REQ_STATE_COMPLETING e REQ_STATE_COMPLETED. Não permite valor nulo.|  
|**request_id**|**Int**|Mostra a ID de solicitação exclusiva atribuída pelo driver a esta solicitação. Não permite valor nulo.|  
|**irp_id**|**Int**|Mostra a ID de IRP exclusiva. Isso é útil para identificar todas as solicitações de E/S relacionadas ao IRP determinado. Não permite valor nulo.|  
|**handle_id**|**Int**|Indica a ID do identificador de namespace. Esse é o identificador específico ao NSO e é exclusivo em uma instância. Não permite valor nulo.|  
|**client_thread_id**|**varbinary(8)**|Mostra a ID de thread do aplicativo cliente que origina a solicitação.<br /><br /> **\*\* Aviso \* \***  isso só será útil se o aplicativo cliente está em execução no mesmo computador que o SQL Server. Quando o aplicativo cliente está em execução remotamente, o **client_thread_id** mostra a ID do thread de algum processo do sistema que funciona em nome do cliente remoto.<br /><br /> Permite valor nulo.|  
|**client_process_id**|**varbinary(8)**|Mostrará a ID de processo do aplicativo cliente se este for executado no mesmo computador que o SQL Server. Para um cliente remoto, isso mostra a ID de processo do sistema que está funcionando em nome do aplicativo cliente. Permite valor nulo.|  
|**handle_context_address**|**varbinary(8)**|Mostra o endereço da estrutura NSO interna associada ao identificador do cliente. Permite valor nulo.|  
|**filestream_transaction_id**|**varbinary(128)**|Mostra a ID da transação associada ao identificador específico e todas as solicitações associadas a esse identificador. É o valor retornado pelo **get_filestream_transaction_context** função. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [FileStream e exibições de gerenciamento dinâmico de FileTable &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)  
  
  
