---
title: fn_syscollector_get_execution_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_details_TSQL
- fn_syscollector_get_execution_details
dev_langs:
- TSQL
helpviewer_keywords:
- fn_syscollector_get_execution_details function
ms.assetid: d59ddf0c-72c0-4c57-bc83-aef260e4e105
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a52ee5b314b2e0e94ebe48bc9405173f24b70d3b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="fnsyscollectorgetexecutiondetails-transact-sql"></a>fn_syscollector_get_execution_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma parte do log [!INCLUDE[ssIS](../../includes/ssis-md.md)] (sysssislog) que corresponde ao package_execution_id do pacote fornecido. A tabela contém uma linha para cada entrada de log gerada em tempo de execução por pacotes, trabalhos e contêineres.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_syscollector_get_execution_details ( log_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *log_id*  
 O identificador exclusivo local do log de execução. *log_id* é **int**.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|id|**Int**|O identificador exclusivo da entrada do log.|  
|event|**sysname**|O nome do evento que gerou a entrada do log.|  
|computer|**nvarchar**|O computador no qual o pacote foi executado quando a entrada do log foi gerada.|  
|operador|**nvarchar**|O nome de usuário da pessoa ou agente que executou o pacote que gerou a entrada do log.|  
|origem|**nvarchar**|O nome do executável que gerou a entrada do log.|  
|sourceid|**uniqueidentifier**|A GUID do executável que gerou a entrada do log.|  
|executionid|**uniqueidentifier**|A GUID da instância de execução do executável que gerou a entrada do log.|  
|starttime|**datetime**|A hora em que o pacote começou a ser executado.|  
|endtime|**datetime**|A hora em que o pacote foi concluído.|  
|datacode|**Int**|Um valor inteiro que identifica o evento associado à entrada do log. "0" indica que o evento não forneceu nenhum identificador.|  
|databytes|**image**|Uma matriz de bytes que identifica um valor de retorno.|  
|message|**nvarchar**|Uma descrição do evento e as informações associadas a ele.|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão SELECT para **dc_operator**.  
  
## <a name="see-also"></a>Consulte também  
 [Habilitar o log no SQL Server Data Tools de pacote](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
