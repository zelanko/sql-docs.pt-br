---
title: Conjunto de linhas DISCOVER_SESSIONS | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_SESSIONS rowset
ms.assetid: 47a79542-3142-4e62-a66f-6c4dbfe0f5c0
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e2a206d090df4b9ab2e498352892b2c3cbb55b35
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="discoversessions-rowset"></a>Conjunto de linhas DISCOVER_SESSIONS
  Oferece uso de recursos e de informações de atividade sobre as sessões atualmente abertas no servidor.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_SESSIONS** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**SESSION_COMMAND_COUNT**|**DBTYPE_I4**||O número de comandos que começaram a ser executados desde o início da sessão.|  
|**SESSION_CONNECTION_ID**|**DBTYPE_I4**||O identificador de conexão para a sessão.|  
|**SESSION_CPU_TIME_MS**|**DBTYPE_UI8**||O tempo de CPU, em milissegundos, consumido por todas as solicitações desde o início da sessão.|  
|**SESSION_CURRENT_DATABASE**|**DBTYPE_WSTR**||O nome do banco de dados usado pela execução atual de comando, ou o banco de dados usado pelo último comando executado.|  
|**SESSION_ELAPSED_TIME_MS**|**DBTYPE_UI8**||O tempo decorrido, em milissegundos, desde o início da sessão.|  
|**SESSION_ID**|**DBTYPE_WSTR**||O identificador exclusivo da sessão, como um GUID.|  
|**SESSION_IDLE_TIME_MS**|**DBTYPE_UI8**||O tempo ocioso, em milissegundos, desde o início da sessão.|  
|**SESSION_LAST_COMMAND**|**DBTYPE_WSTR**||O texto do comando atual em execução ou o último comando executado.|  
|**SESSION_LAST_COMMAND_CPU_TIME_MS**|**DBTYPE_UI8**||O tempo de CPU, em milissegundos, consumido por **SESSION_LAST_COMMAND**.|  
|**SESSION_LAST_COMMAND_ELAPSED_TIME_MS**|**DBTYPE_UI8**||O tempo decorrido, em milissegundos, desde o início de **SESSION_LAST_COMMAND**.|  
|**SESSION_LAST_COMMAND_END_TIME**|**DBTYPE_DBTIMESTAMP**||A hora do servidor UTC no momento da conclusão da execução do último comando.|  
|**SESSION_LAST_COMMAND_START_TIME**|**DBTYPE_DBTIMESTAMP**||A hora do servidor UTC no momento do início da execução do último comando.|  
|**SESSION_PROPERTIES**|**DBTYPE_WSTR**||Reservado para uso futuro.|  
|**SESSION_READ_KB**|**DBTYPE_UI8**||O valor acumulado de leitura de dados do disco, em quilobytes, desde o início da sessão.|  
|**SESSION_READS**|**DBTYPE_UI8**||O número acumulado de leituras de disco desde o início da sessão.|  
|**SESSION_SPID**|**DBTYPE_I4**||A ID da sessão.|  
|**SESSION_START_TIME**|**DBTYPE_DBTIMESTAMP**||A data e a hora em que a sessão foi iniciada como hora UTC para o servidor.|  
|**SESSION_STATUS**|**DBTYPE_I4**||O status de atividade da sessão.<br /><br /> 0 significa "Ocioso": Nenhuma atividade atual está em andamento.<br /><br /> 1 significa "Ativo": A sessão está executando alguma tarefa solicitada.<br /><br /> 2 significa "Bloqueado": A sessão está aguardando por algum recurso para continuar a executar a tarefa suspensa.<br /><br /> 3 significa "Cancelado": A sessão foi marcada como cancelada.|  
|**SESSION_USED_MEMORY**|**DBTYPE_I4**||O tamanho atual de memória usada pela sessão, em quilobytes. O valor relatado é o uso de RAM por SPID, sem distinção entre a memória reduzível e não reduzível. Ao contrário de outros DMVS que relatam o uso de memória, o DISCOVER_SESSIONS não divide o uso de memória por categoria.<br /><br /> Observe que SESSION_USED_MEMORY tende a relatar um uso de memória real menor pois ele exclui objetos compartilhados em várias sessões.  Apenas os objetos que são exclusivos da sessão são representados no cálculo de memória.|  
|**SESSION_USER_NAME**|**DBTYPE_WSTR**||O nome de usuário da sessão.|  
|**SESSION_WRITE_KB**|**DBTYPE_UI8**||O valor acumulado de gravação de dados no disco, em quilobytes, desde o início da sessão.|  
|**SESSION_WRITES**|**DBTYPE_UI8**||O número acumulado de gravações de disco desde o início da sessão.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_SESSIONS** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|SESSION_ID|DBTYPE_WSTR|Opcional.|  
|SESSION_SPID|DBTYPE_I4|Opcional.|  
|SESSION_CONNECTION_ID|DBTYPE_I4|Opcional.|  
|SESSION_USER_NAME|DBTYPE_WSTR|Opcional.|  
|SESSION_CURRENT_DATABASE|DBTYPE_WSTR|Opcional.|  
|SESSION_ELAPSED_TIME_MS|DBTYPE_UI8|Opcional.|  
|SESSION_CPU_TIME_MS|DBTYPE_UI8|Opcional.|  
|SESSION_IDLE_TIME_MS|DBTYPE_UI8|Opcional.|  
|SESSION_STATUS|DBTYPE_I4|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
