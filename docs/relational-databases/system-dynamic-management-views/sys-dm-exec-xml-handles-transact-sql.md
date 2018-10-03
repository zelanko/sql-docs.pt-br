---
title: sys.dm_exec_xml_handles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_exec_xml_handles
- dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles_TSQL
- sys.dm_exec_xml_handles
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_xml_handles dynamic management function
ms.assetid: a873ce0f-6955-417a-96a1-b2ef11a83633
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 959e43a965a3a64eaa39bd20cd9147d074e73296
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47799694"
---
# <a name="sysdmexecxmlhandles-transact-sql"></a>sys.dm_exec_xml_handles (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Retorna informações sobre identificadores ativos que foram abertos por **sp_xml_preparedocument**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dm_exec_xml_handles (session_id | 0 )  
```  
  
## <a name="arguments"></a>Argumentos  
 *session_id* | 0,  
 ID da sessão. Se *session_id* for especificado, essa função retorna informações sobre identificadores XML na sessão especificada.  
  
 Se 0 for especificado, a função retornará as informações sobre todos os identificadores XML em todas as sessões.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID de sessão da sessão que contém o identificador de documento XML.|  
|**document_id**|**int**|ID do identificador de documento XML retornado por **sp_xml_preparedocument**.|  
|**namespace_document_id**|**int**|ID do identificador interno usado para o documento de namespace associado que foi passado como o terceiro parâmetro para **sp_xml_preparedocument**. NULL se não houver nenhum documento de namespace.|  
|**sql_handle**|**varbinary(64)**|Identificador para o texto do código SQL em que o identificador foi definido.|  
|**statement_start_offset**|**int**|Número de caracteres em execução no momento, lote ou procedimento armazenado no qual o **sp_xml_preparedocument** chamada ocorre. Pode ser usada junto com o **sql_handle**, o **statement_end_offset**e o **DM exec_sql_text** a função de gerenciamento dinâmico para recuperar o atualmente executar a instrução para a solicitação.|  
|**statement_end_offset**|**int**|Número de caracteres em execução no momento, lote ou procedimento armazenado no qual o **sp_xml_preparedocument** chamada ocorre. Pode ser usada junto com o **sql_handle**, o **statement_start_offset**e o **DM exec_sql_text** a função de gerenciamento dinâmico para recuperar o atualmente executar a instrução para a solicitação.|  
|**creation_time**|**datetime**|Carimbo de hora quando **sp_xml_preparedocument** foi chamado.|  
|**original_document_size_bytes**|**bigint**|Tamanho do documento XML não analisado em bytes.|  
|**original_namespace_document_size_bytes**|**bigint**|Tamanho do documento XML de namespace não analisado, em bytes. NULL se não houver nenhum documento de namespace.|  
|**num_openxml_calls**|**bigint**|Número de chamadas de OPENXML com esse identificador de documento.|  
|**row_count**|**bigint**|Número de linhas retornadas por todas as chamadas de OPENXML anteriores para esse identificador de documento.|  
|**dormant_duration_ms**|**bigint**|Milissegundos desde a última chamada de OPENXML. Se OPENXML não foi chamado, retornará milissegundos desde o **sp_xml_preparedocument**chamada t.|  
  
## <a name="remarks"></a>Comentários  
 O tempo de vida dos **sql_handles** usado para recuperar o texto SQL que executou uma chamada a **sp_xml_preparedocument** dura mais do que o plano armazenado em cache usado para executar a consulta. Se o texto de consulta não estiver disponível no cache, os dados não poderão ser recuperados usando as informações fornecidas no resultado de função. Isso poderá ocorrer se você estiver executando muitos lotes grandes.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão VIEW SERVER STATE no servidor para ver todas as sessões ou IDs de sessões que não pertencem ao chamador. Um chamador sempre pode ver os dados para sua própria ID de sessão atual.      
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir seleciona todos os identificadores ativos.  
  
```  
SELECT * FROM sys.dm_exec_xml_handles(0);  
```  
  
## <a name="see-also"></a>Consulte também  
 <br>[Exibições de gerenciamento dinâmico e funções (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
 <br>[Funções (Transact-SQL) e exibições de gerenciamento dinâmico relacionadas à execução](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)
 <br>[sp_xml_preparedocument (Transact-SQL)](../system-stored-procedures/sp-xml-preparedocument-transact-sql.md)
 <br>[sp_xml_removedocument (Transact-SQL)](../system-stored-procedures/sp-xml-removedocument-transact-sql.md)


 
  
  
