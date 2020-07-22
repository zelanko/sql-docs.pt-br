---
title: catalog.event_messages | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a31a654f-31e9-4da1-aabf-182b07848e36
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2e19ca7fac23979ecd691ed6cab45fa2cfec9564
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86912623"
---
# <a name="catalogevent_messages"></a>catalog.event_messages 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe informações sobre mensagens que foram registradas em log durante operações.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|Event_message_ID|BIGINT|A ID exclusiva da mensagem de evento.|  
|Operation_id|BIGINT|O tipo de operação.<br /><br /> Para ver uma lista completa dos tipos de operação, consulte [catalog.operations &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md).|  
|Message_time|datetimeoffset(7)|A hora em que a mensagem foi criada.|  
|Message_type|SMALLINT|O tipo da mensagem exibida. Para obter mais informações sobre tipos de mensagem, consulte [catalog.operation_messages &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-operation-messages-ssisdb-database.md).|  
|Message_source_type|SMALLINT|A origem da mensagem.|  
|message|nvarchar(max)|O texto da mensagem.|  
|Extended_info_id|BIGINT|A ID de informações adicionais relacionadas à mensagem da operação, localizada na exibição [catalog.extended_operation_info &#40;Banco de dados SSISDB&#41;](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md).|  
|Package_name|nvarchar(260)|O nome do arquivo do pacote.|  
|Event_name|nvarchar(1024)|O evento em tempo de execução associado ao tipo de mensagem.|  
|Message_source_name|nvarchar(4000)|O componente de pacote que é a origem da mensagem.|  
|Message_source_id|nvarchar(38)|A ID exclusiva da origem da mensagem.|  
|Subcomponent_name|nvarchar(4000)|O componente do fluxo de dados que é a origem da mensagem.<br /><br /> Quando as mensagens são retornadas pelo mecanismo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], SSIS.Pipeline aparece nesta coluna.|  
|Package_path|nvarchar(max)|O caminho exclusivo do componente no pacote.|  
|Execution_path|nvarchar(max)|O caminho completo do pacote pai para o ponto no qual o componente é executado.<br /><br /> Esse caminho também captura iterações de um componente.|  
|threadID|INT|ID do thread que está executando quando a mensagem é registrada em log.|  
|Message_code|INT|O código associado à mensagem.|  
  
## <a name="remarks"></a>Comentários  
 Esta exibição exibe os tipos de origem de mensagem a seguir.  
  
|**message_source_type**|DESCRIÇÃO|  
|-------------------------------|-----------------|  
|10|APIs de entrada, como os procedimentos armazenados T-SQL e CLR|  
|20|O processo externo usado para executar pacote (ISServerExec.exe)|  
|30|Objetos de nível de pacote|  
|40|Tarefas de fluxo de controle|  
|50|Contêineres de fluxo de controle|  
|60|Tarefa de Fluxo de Dados|  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na operação  
  
-   Associação à função de banco de dados **ssis_admin**.  
  
-   Associação à função de servidor **sysadmin**.  
  
## <a name="see-also"></a>Consulte Também  
 [catalog.event_message_context](../../integration-services/system-views/catalog-event-message-context.md)  
  
  
