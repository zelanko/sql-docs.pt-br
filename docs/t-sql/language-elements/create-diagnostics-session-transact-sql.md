---
title: CREATE DIAGNOSTICS SESSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 662d019e-f217-49df-9e2f-b5662fa0342d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0d4148e002ba84677e13e101a4830f0b6da10915
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68088969"
---
# <a name="create-diagnostics-session-transact-sql"></a>CREATE DIAGNOSTICS SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  As sessões de diagnóstico permitem que você salve as informações de diagnóstico detalhadas definidas pelo usuário sobre o desempenho do sistema ou da consulta.  
  
 As sessões de diagnóstico geralmente são usadas para depurar o desempenho de uma consulta específica ou para monitorar o comportamento de um componente do dispositivo específico durante a operação do dispositivo.  
  
> [!NOTE]  
>  Você deve estar familiarizado com XML para usar sessões de diagnóstico.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
Creating a new diagnostics session:  
CREATE DIAGNOSTICS SESSION diagnostics_name AS N'{<session_xml>}';  
  
<session_xml>::  
<Session>  
   [ <MaxItemCount>max_item_count_num</MaxItemCount> ]  
   <Filter>  
      { \<Event Name="event_name"/>  
         [ <Where>\<filter_property_name Name="value" ComparisonType="comp_type"/></Where> ] [ ,...n ]  
      } [ ,...n ]  
   </Filter> ]   
   <Capture>  
      \<Property Name="property_name"/> [ ,...n ]  
   </Capture>  
<Session>  
  
Retrieving results for a diagnostics session:  
SELECT * FROM master.sysdiag.diagnostics_name ;  
  
Removing results for a diagnostics session:  
DROP DIAGNOSTICS SESSION diagnostics_name ;  
```  
  
## <a name="arguments"></a>Argumentos  
 *diagnostics_name*  
 O nome da sessão de diagnóstico. os nomes de sessão de diagnóstico podem incluir somente caracteres a-z, A-Z e 0-9. Além disso, os nomes de sessão de diagnóstico precisam começar com um caractere. *diagnostics_name* é limitado a 127 caracteres.  
  
 *max_item_count_num*  
 O número de eventos a serem persistidos em uma exibição. Por exemplo, se 100 for especificado, os 100 eventos mais recentes que corresponderem aos critérios de filtro serão persistidos na sessão de diagnóstico. Se menos de 100 eventos correspondentes forem encontrados, a sessão de diagnóstico conterá menos de 100 eventos. *max_item_count_num* precisa ser pelo menos 100 e menor ou igual a 100.000.  
  
 *event_name*  
 Define os eventos reais a serem coletados na sessão de diagnóstico.  *event_name* é um dos eventos listados em [sys.pdw_diag_events](../../relational-databases/system-catalog-views/sys-pdw-diag-events-transact-sql.md) em que `sys.pdw_diag_events.is_enabled='True'`.  
  
 *filter_property_name*  
 O nome da propriedade na qual os resultados devem ser restringidos. Por exemplo, se você desejar limitar com base na ID de sessão, *filter_property_name* deverá ser *SessionId*. Consulte *property_name* abaixo para obter uma lista de valores possíveis para *filter_property_name*.  
  
 *value*  
 Um valor a ser avaliado em relação a *filter_property_name*. O tipo de valor precisa corresponder ao tipo de propriedade. Por exemplo, se o tipo de propriedade for decimal, o tipo de *valor* precisará ser um decimal.  
  
 *comp_type*  
 O tipo de comparação. Os valores possíveis são: Equals, EqualsOrGreaterThan, EqualsOrLessThan, GreaterThan, LessThan, NotEquals, Contains, RegEx  
  
 *property_name*  
 Uma propriedade relacionada ao evento.  Os nomes de propriedade podem fazer parte da marca de captura ou ser usados como parte dos critérios de filtragem.  
  
|Nome da propriedade|DESCRIÇÃO|  
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
 Cada usuário tem permissão para no máximo 10 sessões de diagnóstico simultâneas. Consulte [sys.pdw_diag_sessions](../../relational-databases/system-catalog-views/sys-pdw-diag-sessions-transact-sql.md) para obter uma lista das sessões atuais e descarte as sessões desnecessárias usando `DROP DIAGNOSTICS SESSION`.  
  
 As sessões de diagnóstico continuarão a coletar metadados até serem descartadas.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão **ALTER SERVER STATE**.  
  
## <a name="locking"></a>Bloqueio  
 Coloca um bloqueio compartilhado na tabela de sessões de diagnóstico.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-diagnostics-session"></a>a. Criando uma sessão de diagnóstico  
 Este exemplo cria uma sessão de diagnóstico para registrar as métricas de desempenho do mecanismo de banco de dados. O exemplo cria uma sessão de diagnóstico que escuta os eventos de execução/término da consulta do mecanismo e um evento de bloqueio do DMS. O que é retornado é o texto do comando, o nome do computador, a ID de solicitação (ID da consulta) e a sessão na qual o evento foi criado.  
  
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
  
 Exiba os resultados da sessão de diagnóstico selecionando no esquema sysdiag.  
  
```  
SELECT * FROM master.sysdiag.MYDIAGSESSION;  
```  
  
 Observe que o esquema sysdiag contém uma exibição com o mesmo nome da sua sessão de diagnóstico.  
  
 Para ver apenas a atividade da sua conexão, adicione a propriedade `Session.SPID` e adicione `WHERE [Session.SPID] = @@spid;` à consulta.  
  
 Ao terminar de usar a sessão de diagnóstico, descarte-a usando o comando **DROP DIAGNOSTICS**.  
  
```  
DROP DIAGNOSTICS SESSION MYDIAGSESSION;  
```  
  
### <a name="b-alternative-diagnostic-session"></a>B. Sessão de diagnóstico alternativa  
 Um segundo exemplo com propriedades um pouco diferentes.  
  
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
  
 Execute uma consulta, como:  
  
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
  
 Ao terminar de usar a sessão de diagnóstico, descarte-a usando o comando **DROP DIAGNOSTICS**.  
  
```  
DROP DIAGNOSTICS SESSION PdwOptimizationDiagnostics;  
```  
  
  
