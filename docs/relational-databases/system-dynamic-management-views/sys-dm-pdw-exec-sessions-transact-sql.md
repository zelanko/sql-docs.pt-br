---
description: sys.dm_pdw_exec_sessions (Transact-SQL)
title: sys.dm_pdw_exec_sessions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/22/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 31c262b3-7e4d-44c4-af71-aaef0fd1a980
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: 1e5fc3af931460de84dde4467b803226dcd6d431
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482562"
---
# <a name="sysdm_pdw_exec_sessions-transact-sql"></a>sys.dm_pdw_exec_sessions (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contém informações sobre todas as sessões no momento ou recentemente abertas no dispositivo. Ele lista uma linha por sessão.  
  
|Nome da coluna|Tipo de Dados|DESCRIÇÃO|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**|A ID da consulta atual ou a última execução de consulta (se a sessão for ENCERRAda e a consulta estiver sendo executada no momento do encerramento). Chave para esta exibição.|Exclusivo em todas as sessões no sistema.|  
|status|**nvarchar (10)**|Para sessões atuais, identifica se a sessão está ativa ou ociosa no momento. Para as sessões anteriores, o status da sessão pode mostrar fechado ou encerrado (se a sessão foi fechada de modo forçado).|' ATIVO ', ' FECHADO ', ' OCIOSO ', ' ENCERRADO '|  
|request_id|**nvarchar(32)**|A ID da consulta atual ou da última execução de consulta.|Exclusivo em todas as solicitações no sistema. NULL se nenhum tiver sido executado.|  
|security_id|**varbinary(85)**|A ID de segurança do principal que está executando a sessão.||  
|login_name|**nvarchar(128)**|O nome de logon da entidade de segurança que está executando a sessão.|Qualquer cadeia de caracteres que esteja de acordo com as convenções de nomenclatura de usuário.|  
|login_time|**datetime**|Data e hora em que o usuário fez logon e esta sessão foi criada.|**Data** e hora válidas antes da hora atual.|  
|query_count|**int**|Captura o número de consultas/a sessão requeststhis foi executada desde a criação.|Maior ou igual a 0.|  
|is_transactional|**bit**|Captura se uma sessão está atualmente dentro de uma transação ou não.|0 para confirmação automática, 1 para transacional.|  
|client_id|**nvarchar(255)**|Captura informações do cliente para a sessão.|Qualquer cadeia de caracteres válida.|  
|app_name|**nvarchar(255)**|Captura as informações de nome do aplicativo como opção definidas como parte do processo de conexão.|Qualquer cadeia de caracteres válida.|  
|sql_spid|**int**|O número de identificação do SPID. Use `session_id` esta sessão. Use a `sql_spid` coluna para ingressar no **Sys.dm_pdw_nodes_exec_sessions**.<br /><br /> Aviso esta coluna contém SPIDs fechados. **\* \* \* \***||  
  
 Para obter informações sobre o máximo de linhas retidas por essa exibição, consulte a seção de metadados no tópico [limites de capacidade](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) .  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW SERVER STATE`.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico do Azure Synapse Analytics e Parallel data warehouse &#40;&#41;de Transact-SQL ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
