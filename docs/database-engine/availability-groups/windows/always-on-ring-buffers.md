---
title: Buffers de anéis de Grupos de Disponibilidade Always On (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 47bb7a1a-c0a5-473c-a7db-d9f4bf3ee650
caps.latest.revision: 7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f7cca7af1978aae48099e30fe85b96d1226d7876
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="always-on-availability-groups-ring-buffers"></a>Buffers de anéis de Grupos de Disponibilidade Always On
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Algumas informações de diagnóstico de Grupos de Disponibilidade Always On podem ser obtidas nos buffers de anéis do SQL Server ou na DMV (exibição de gerenciamento dinâmico) sys.dm_os_ring_buffers. Os buffers de anéis são criados durante a inicialização do SQL Server e registram alertas no sistema do SQL Server para diagnósticos internos. Não há suporte para eles, mas você ainda pode extrair informações valiosas deles ao solucionar problemas. Esses buffers de anéis fornecem outra fonte de diagnóstico quando o SQL Server para de responder ou falha.  
  
 A consulta T-SQL (Transact-SQL) a seguir recupera todos os registros de eventos dos buffers de anéis dos grupos de disponibilidade.  
  
```sql  
SELECT * FROM sys.dm_os_ring_buffers WHERE ring_buffer_type LIKE '%HADR%'  
```  
  
 Para que os dados sejam mais gerenciáveis, filtre-os por data e, em seguida, por tipo de buffer de anéis. A consulta a seguir recupera os registros do buffer de anel especificado que ocorreu hoje.  
  
```sql  
DECLARE @runtime datetime  
SET @runtime = GETDATE()  
SELECT CONVERT (varchar(30), @runtime, 121) as data_collection_runtime,   
DATEADD (ms, -1 * (inf.ms_ticks - ring.[timestamp]), GETDATE()) AS ring_buffer_record_time,   
ring.[timestamp] AS record_timestamp, inf.ms_ticks AS cur_timestamp, ring.*   
FROM sys.dm_os_ring_buffers ring  
CROSS JOIN sys.dm_os_sys_info inf where ring_buffer_type='<RING_BUFFER_TYPE>'  
```  
  
 A coluna Registro de cada registro contém dados de diagnóstico em formato XML. Os dados XML são diferentes entre os tipos de buffer de anel. Para obter mais informações sobre cada tipo de buffer de anel, veja [Tipos de buffer de anel de grupos de disponibilidade](#BKMK_RingBufferTypes). Para que os dados XML sejam mais legíveis, você precisa personalizar a consulta T-SQL para extrair os elementos XML desejados. Por exemplo, a consulta a seguir recupera todos os eventos do buffer de anel RING_BUFFER_HADRDBMGR_API e formata os dados XML em colunas de tabela separadas.  
  
```sql  
WITH hadr(ts, type, record) AS  
(  
  SELECT timestamp AS ts, ring_buffer_type AS type, CAST(record AS XML) AS record   
  FROM sys.dm_os_ring_buffers WHERE ring_buffer_type = 'RING_BUFFER_HADRDBMGR_API'  
)  
SELECT   
  ts,  
  type,  
  record.value('(./Record/@id)[1]','bigint') AS [Record ID],  
  record.value('(./Record/@time)[1]','bigint') AS [Time],  
  record.value('(./Record/HadrDbMgrAPI/dbId)[1]', 'bigint') AS [DBID],  
  record.value('(/Record/HadrDbMgrAPI/API)[1]', 'varchar(50)') AS [API],  
  record.value('(/Record/HadrDbMgrAPI/Action)[1]', 'varchar(50)') AS [Action],  
  record.value('(/Record/HadrDbMgrAPI/role)[1]', 'int') AS [Role],  
  record.value('(/Record/Stack)[1]', 'varchar(100)') AS [Call Stack]  
FROM hadr  
ORDER BY record.value('(./Record/@time)[1]','bigint') DESC  
GO  
```  
  
##  <a name="BKMK_RingBufferTypes"></a> Tipos de buffer de anel de grupos de disponibilidade  
 Há quatro buffers de anel de grupos de disponibilidade em sys.dm_os_ring_buffers. A tabela a seguir descreve os tipos de buffer de anel e um exemplo do conteúdo da coluna Registro para cada tipo de buffer de anel.  
  
 **RING_BUFFER_HADRDBMGR_API**  
  
 Registra transições de estado que foram ou estão ocorrendo. Ao observar as transições de estado preste bastante atenção aos valores objectType.  
  
```xml  
<Record id="11" type="RING_BUFFER_HADRDBMGR_STATE" time="860243">  
  <HadrDbMgrState>  
    <objectType>HadrUsers</objectType>  
    <currentState>HDbMState_Starting</currentState>  
    <proposedState>HDbMState_Started</proposedState>  
    <targetState>HDbMState_Started</targetState>  
    <legalTransition>Y</legalTransition>  
    <role>1</role>  
  </HadrDbMgrState>  
</Record>  
```  
  
 **RING_BUFFER_HADRDBMGR_STATE**  
  
 Registra o método interno ou as chamadas de função feitas pela atividade do Always On. Ela pode mostrar informações tais como suspensão, retomada ou alterações de função, incluindo pontos de entrada e saída.  
  
```xml  
<Record id="45" type="RING_BUFFER_HADRDBMGR_STATE" time="1723487912">  
  <HadrDbMgrState>  
    <dbId>5</dbId>  
    <objectType>HadrDbMgr</objectType>  
    <currentState>HDbMState_Starting</currentState>  
    <proposedState>HDbMState_Started</proposedState>  
    <targetState>HDbMState_Started</targetState>  
    <legalTransition>Y</legalTransition>  
    <role>2</role>  
  </HadrDbMgrState>  
</Record>  
```  
  
 **RING_BUFFER_HADRDBMGR_COMMIT**  
  
```xml  
<Record id="0" type="RING_BUFFER_HADRDBMGR_COMMIT" time="1723475368">  
  <HadrDbMgrCommitPolicy>  
    <dbId>5</dbId>  
    <replicaId>883a18f5-97d5-450f-8f8f-9983a4fa5299</replicaId>  
    <dbHardenPolicy>KillAll</dbHardenPolicy>  
    <dbSyncConfig>0x0</dbSyncConfig>  
    <syncPartnerCount>0</syncPartnerCount>  
    <minSyncPartnerConfig>0</minSyncPartnerConfig>  
    <partnerHardenPolicy>KillAll</partnerHardenPolicy>  
    <partnerSyncConfig>0x0</partnerSyncConfig>  
    <logBlock>0x0000000000000000</logBlock>  
    <leaseExpired>Y</leaseExpired>  
    <partnerChange>N</partnerChange>  
    <role>2</role>  
  </HadrDbMgrCommitPolicy>  
</Record>  
```  
  
 **RING_BUFFER_HADR_TRANSPORT_STATE**  
  
```xml  
<Record id="3" type="RING_BUFFER_HADR_TRANSPORT_STATE" time="1723485399">  
  <HadrTransportState>  
    <agId>08264B79-D10B-412F-B38D-CA07B08E9BD8</agId>  
    <localArId>883A18F5-97D5-450F-8F8F-9983A4FA5299</localArId>  
    <targetArId>628D6349-72DD-4D18-A6E1-1272645660BA</targetArId>  
    <currentState>HadrSession_Configuring</currentState>  
    <targetState>HadrSession_Connected</targetState>  
    <legalTransition>Y</legalTransition>  
  </HadrTransportState>  
</Record>  
```  
  
## <a name="parse-xml-data-from-a-ring-buffer"></a>Analisa dados XML de um buffer de anel  
 Você pode analisar o campo Registro do buffer de anel que está inspecionando usando [value&#40;&#41; Method &#40;xml Data Type&#41;](~/t-sql/xml/value-method-xml-data-type.md) em sua consulta. Para usar esse método, primeiro é preciso [CONVERTER](~/t-sql/functions/cast-and-convert-transact-sql.md) a coluna de registro do buffer de anel em XML. Por exemplo, a consulta abaixo demonstra como analisar RING_BUFFER_HADRDBMGR_API em formato legível usando esse método.  
  
```sql 
WITH hadr(ts, type, record) AS  
   (SELECT timestamp AS ts, ring_buffer_type AS type, CAST(record AS XML) AS record   
FROM sys.dm_os_ring_buffers   
WHERE ring_buffer_type = 'RING_BUFFER_HADRDBMGR_API')  
SELECT ts,  
type,  
record.value('(./Record/@id)[1]','bigint') AS [Record id],  
record.value('(./Record/@time)[1]','bigint') AS [Time],  
record.value('(./Record/HadrDbMgrAPI/dbId)[1]', 'bigint') AS [dbid],  
record.value('(/Record/HadrDbMgrAPI/API)[1]', 'varchar(50)') AS [API],  
record.value('(/Record/HadrDbMgrAPI/Action)[1]', 'varchar(50)') AS [Action],  
record.value('(/Record/HadrDbMgrAPI/role)[1]', 'int') AS [Role],  
record.value('(/Record/Stack)[1]', 'varchar(100)') AS [Call Stack]  
FROM hadr  
ORDER BY record.value('(./Record/@time)[1]','bigint') DESC  
GO  
```  
  
  