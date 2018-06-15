---
title: sys.dm_filestream_file_io_handles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_filestream_file_io_handles
- sys.dm_filestream_file_io_handles
- dm_filestream_file_io_handles_TSQL
- sys.dm_filestream_file_io_handles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_filestream_file_io_handle catalog view
ms.assetid: e59632f4-3292-419f-9217-ca375749f1a5
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 87dc96a297933b6981e1e2ada432d355287b4ce2
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2018
ms.locfileid: "34463632"
---
# <a name="sysdmfilestreamfileiohandles-transact-sql"></a>sys.dm_filestream_file_io_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe os identificadores de arquivos que o NSO (proprietário do namespace) conhece. Identificadores de FileStream que um cliente adquiriu usando **OpenSqlFilestream** são exibidos por esta exibição.  
  
|Coluna|Tipo|Description|  
|------------|----------|-----------------|  
|**handle_context_address**|**varbinary(8)**|Mostra o endereço da estrutura NSO interna associada ao identificador do cliente. Permite valor nulo.|  
|**creation_request_id**|**Int**|Mostra um campo da solicitação de E/S REQ_PRE_CREATE usada para criar este identificador. Não permite valor nulo.|  
|**creation_irp_id**|**Int**|Mostra um campo da solicitação de E/S REQ_PRE_CREATE usada para criar este identificador. Não permite valor nulo|  
|**handle_id**|**Int**|Mostra a ID exclusiva deste identificador que é atribuída pelo driver. Não permite valor nulo.|  
|**creation_client_thread_id**|**varbinary(8)**|Mostra um campo da solicitação de E/S REQ_PRE_CREATE usada para criar este identificador. Permite valor nulo.|  
|**creation_client_process_id**|**varbinary(8)**|Mostra um campo da solicitação de E/S REQ_PRE_CREATE usada para criar este identificador. Permite valor nulo.|  
|**filestream_transaction_id**|**varbinary(128)**|Mostra a ID da transação associada ao identificador específico. Este é o valor retornado pelo **get_filestream_transaction_context** função. Use este campo para ingressar o **sys.DM filestream_file_io_requests** exibição. Permite valor nulo.|  
|**access_type**|**nvarchar(60)**|Não permite valor nulo.|  
|**logical_path**|**nvarchar(256)**|Mostra o nome de caminho lógico do arquivo que este identificador abriu. Este é o mesmo nome de caminho que é retornado pelo **. Nome de caminho** método **varbinary**(**max**) filestream. Permite valor nulo.|  
|**physical_path**|**nvarchar(256)**|Mostra o nome de caminho NTFS real do arquivo. Este é o mesmo nome de caminho retornado pelo **. PhysicalPathName** método o **varbinary**(**max**) filestream. Ele é habilitado pelo sinalizador de rastreamento 5556. Permite valor nulo.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte também  
 [FileStream e exibições de gerenciamento dinâmico de FileTable &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)  
  
  
