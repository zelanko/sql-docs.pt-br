---
title: "CRIAR sessão de diagnóstico (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: pdw
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 662d019e-f217-49df-9e2f-b5662fa0342d
caps.latest.revision: "9"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: bda2e9c6813e53bffeab974e5e01b475cdfebe26
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="create-diagnostics-session-transact-sql"></a>CRIAR sessão de diagnóstico (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Sessões de diagnóstico permitem que você salve as informações de diagnóstico detalhadas, definidas pelo usuário no desempenho do sistema ou de consulta.  
  
 Sessões de diagnóstico são normalmente usadas para depurar o desempenho de uma consulta específica, ou para monitorar o comportamento de um componente específico do dispositivo durante a operação do dispositivo.  
  
> [!NOTE]  
>  Você deve estar familiarizado com o XML para usar sessões de diagnóstico.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Creating a new diagnostics session:  
CREATE DIAGNOSTICS SESSION diagnostics_name AS N’{<session_xml>}’;  
  
<session_xml>::  
<Session>  
   [ <MaxItemCount>max_item_count_num</MaxItemCount> ]  
   <Filter>  
      { \<Event Name=”event_name”/>  
         [ <Where>\<filter_property_name Name=”value” ComparisonType="comp_type"/></Where> ] [ ,...n ]  
      } [ ,...n ]  
   </Filter> ]   
   <Capture>  
      \<Property Name=”property_name”/> [ ,...n ]  
   </Capture>  
<Session>  
  
Retrieving results for a diagnostics session:  
SELECT * FROM master.sysdiag.diagnostics_name ;  
  
Removing results for a diagnostics session:  
DROP DIAGNOSTICS SESSION diagnostics_name ;  
```  
  
## <a name="arguments"></a>Argumentos  
 *diagnostics_name*  
 O nome da sessão de diagnóstico. Nomes de sessão de diagnóstico podem incluir caracteres a-z, A-Z e 0-9. Além disso, os nomes de sessão de diagnóstico devem começar com um caractere. *diagnostics_name* é limitada a 127 caracteres.  
  
 *max_item_count_num*  
 O número de eventos sejam mantidas em um modo de exibição. Por exemplo, se 100 for especificado, os 100 eventos mais recentes que correspondem aos critérios de filtro serão mantidos para a sessão de diagnóstico. Se menos de 100 eventos de correspondência for encontrada, a sessão de diagnóstico irá conter menos de 100 eventos. *max_item_count_num* deve ser pelo menos 100 e menor ou igual a 100.000.  
  
 *event_name*  
 Define os eventos reais a serem coletadas em que a sessão de diagnóstico.  *event_name* é um dos eventos listados em [sys.pdw_diag_events](http://msdn.microsoft.com/en-us/d813aac0-cea1-4f53-b8e8-d26824bc2587) onde `sys.pdw_diag_events.is_enabled='True'`.  
  
 *filter_property_name*  
 O nome da propriedade na qual restringir os resultados. Por exemplo, se você quiser limitar com base na id de sessão, *filter_property_name* devem ser *SessionId*. Consulte *property_name* abaixo para obter uma lista de valores possíveis para *filter_property_name*.  
  
 *value*  
 Um valor a ser avaliado em relação a *filter_property_name*. O tipo de valor deve corresponder ao tipo de propriedade. Por exemplo, se o tipo de propriedade é decimal, o tipo de *valor* deve ser um decimal.  
  
 *comp_type*  
 O tipo de comparação. Possíveis valores são: igual a, EqualsOrGreaterThan, EqualsOrLessThan, GreaterThan, LessThan, NotEquals, Contains, RegEx  
  
 *Property_Name*  
 Uma propriedade relacionada ao evento.  Nomes de propriedade podem fazer parte da marca de captura ou usado como parte dos critérios de filtragem.  
  
|Nome da propriedade|Description|  
|-------------------|-----------------|  
|UserName|Um nome de usuário (logon).|  
|SessionId|Uma ID de sessão.|  
|QueryId|Uma ID de consulta.|  
|CommandType|Um tipo de comando.|  
|CommandText|Texto dentro de um comando processado.|  
|OperationType|O tipo de operação para o evento.|  
|Duration|A duração do evento.|  
|SPID|A ID de processo do serviço.|  
  
## <a name="remarks"></a>Comentários  
 Cada usuário é permitido um máximo de 10 sessões simultâneas de diagnóstico. Consulte [sys.pdw_diag_sessions](http://msdn.microsoft.com/en-us/ca111ddc-2787-4205-baf0-1a242c0257a9) para obter uma lista de sessões atuais e soltar os desnecessários sessões usando `DROP DIAGNOSTICS SESSION`.  
  
 Sessões de diagnóstico continuará coletar metadados até descartado.  
  
## <a name="permissions"></a>Permissões  
 Requer o **ALTER SERVER STATE** permissão.  
  
## <a name="locking"></a>Bloqueio  
 Leva um bloqueio compartilhado na tabela de sessões de diagnóstico.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-diagnostics-session"></a>A. Criar uma sessão de diagnóstico  
 Este exemplo cria uma sessão de diagnóstico para registrar as métricas de desempenho do mecanismo de banco de dados. O exemplo cria uma sessão de diagnóstico que escuta para eventos de execução/término do mecanismo de consulta e um evento DMS bloqueio. O que é retornado é o texto do comando, nome da máquina, id de solicitação (id de consulta) e a sessão que o evento foi criado.  
  
```  
CREATE DIAGNOSTICS SESSION MYDIAGSESSION AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:EngineQueryRunningEvent" />  
      <Event Name="DmsCoreInstrumentation:DmsBlockingQueueEnqueueBeginEvent" />  
      <Where>  
         <SessionId Value="381" ComparisonType="NotEquals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Query.CommandText" />  
      <Property Name="MachineName" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Alias" />  
      <Property Name="Duration" />  
      <Property Name="Session.SessionId" />  
   </Capture>  
</Session>';  
```  
  
 Após a criação da sessão de diagnóstico, execute uma consulta.  
  
```  
SELECT COUNT(EmployeeKey) FROM AdventureWorksPDW2012..FactSalesQuota;  
```  
  
 Exiba os resultados da sessão de diagnóstico, selecionando a partir do esquema sysdiag.  
  
```  
SELECT * FROM master.sysdiag.MYDIAGSESSION;  
```  
  
 Observe que o esquema sysdiag contém uma exibição que é chamada de seu nome de sessão de diagnóstico.  
  
 Para ver apenas a atividade para sua conexão, adicione o `Session.SPID` propriedade e adicionar `WHERE [Session.SPID] = @@spid;` à consulta.  
  
 Quando tiver terminado com a sessão de diagnóstico, descartá-la usando o **DROP diagnóstico** comando.  
  
```  
DROP DIAGNOSTICS SESSION MYDIAGSESSION;  
```  
  
### <a name="b-alternative-diagnostic-session"></a>B. Sessão de diagnóstico alternativo  
 Um segundo exemplo com propriedades ligeiramente diferentes.  
  
```  
-- Determine the session_id of your current session  
SELECT TOP 1 session_id();  
-- Replace \<*session_number*> in the code below with the numbers in your session_id  
CREATE DIAGNOSTICS SESSION PdwOptimizationDiagnostics AS N'  
<Session>  
   <MaxItemCount>100</MaxItemCount>  
   <Filter>  
      <Event Name="EngineInstrumentation:MemoGenerationBeginEvent" />  
      <Event Name="EngineInstrumentation:MemoGenerationEndEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationBeginEvent" />  
      <Event Name="DSQLInstrumentation:OptimizationEndEvent" />  
      <Event Name="DSQLInstrumentation:BuildRelOpContextTreeBeginEvent" />  
      <Event Name="DSQLInstrumentation:PostPlanGenModifiersEndEvent" />  
      <Where>  
         <SessionId Value="\<*session_number*>" ComparisonType="Equals" />  
      </Where>  
   </Filter>  
   <Capture>  
      <Property Name="Session.SessionId" />  
      <Property Name="Query.QueryId" />  
      <Property Name="Query.CommandText" />  
      <Property Name="Name" />  
      <Property Name="DateTimePublished" />  
      <Property Name="DateTimePublished.Ticks" />  
  </Capture>  
</Session>';  
```  
  
 Execute uma consulta, tais como:  
  
```  
USE ssawPDW;  
GO  
SELECT * FROM dbo.FactFinance;  
```  
  
 A consulta a seguir retorna o tempo de autorização:  
  
```  
SELECT *   
FROM master.sysdiag.PdwOptimizationDiagnostics   
ORDER BY DateTimePublished;  
```  
  
 Quando tiver terminado com a sessão de diagnóstico, descartá-la usando o **DROP diagnóstico** comando.  
  
```  
DROP DIAGNOSTICS SESSION PdwOptimizationDiagnostics;  
```  
  
  
