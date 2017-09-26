---
title: Catalog.event_messages | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: a31a654f-31e9-4da1-aabf-182b07848e36
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a0db5ace2a95bea93189cb48378b01a4ba599942
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="catalogeventmessages"></a>catalog.event_messages
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Exibe informações sobre mensagens que foram registradas em log durante operações.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|Event_message_ID|bigint|A ID exclusiva da mensagem de evento.|  
|Operation_id|bigint|O tipo de operação.<br /><br /> Para obter uma lista dos tipos de operação, consulte [Catalog. Operations &#40; Banco de dados SSISDB &#41; ](../../integration-services/system-views/catalog-operations-ssisdb-database.md).|  
|Message_time|datetimeoffset(7)|A hora em que a mensagem foi criada.|  
|Message_type|smallint|O tipo da mensagem exibida. Para obter mais informações sobre tipos de mensagem, consulte [Catalog. operation_messages &#40; Banco de dados SSISDB &#41; ](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md).|  
|Message_source_type|smallint|A origem da mensagem.|  
|message|nvarchar(max)|O texto da mensagem.|  
|Extended_info_id|bigint|A ID de informações adicionais relacionadas à mensagem de operação, localizada no [Catalog. extended_operation_info &#40; Banco de dados SSISDB &#41; ](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md) exibição.|  
|Package_name|nvarchar(260)|O nome do arquivo do pacote.|  
|Event_name|nvarchar (1024)|O evento em tempo de execução associado ao tipo de mensagem.|  
|Message_source_name|nvarchar(4000)|O componente de pacote que é a origem da mensagem.|  
|Message_source_id|Nvarchar(38)|A ID exclusiva da origem da mensagem.|  
|Subcomponent_name|nvarchar(4000)|O componente do fluxo de dados que é a origem da mensagem.<br /><br /> Quando as mensagens são retornadas pelo mecanismo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], SSIS.Pipeline aparece nesta coluna.|  
|Package_path|nvarchar(max)|O caminho exclusivo do componente no pacote.|  
|Execution_path|nvarchar(max)|O caminho completo do pacote pai para o ponto no qual o componente é executado.<br /><br /> Esse caminho também captura iterações de um componente.|  
|threadID|int|ID do thread que está executando quando a mensagem é registrada em log.|  
|Message_code|int|O código associado à mensagem.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição exibe os tipos de origem de mensagem a seguir.  
  
|**message_source_type**|Description|  
|-------------------------------|-----------------|  
|10|APIs de entrada, como os procedimentos armazenados T-SQL e CLR|  
|20|O processo externo usado para executar pacote (ISServerExec.exe)|  
|30|Objetos de nível de pacote|  
|40|Tarefas de fluxo de controle|  
|50|Contêineres de fluxo de controle|  
|60|Tarefa de fluxo de dados|  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na operação  
  
-   Associação de **ssis_admin** função de banco de dados.  
  
-   Associação de **sysadmin** função de servidor.  
  
## <a name="see-also"></a>Consulte também  
 [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
  
