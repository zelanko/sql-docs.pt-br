---
title: fn_syscollector_get_execution_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_syscollector_get_execution_details_TSQL
- fn_syscollector_get_execution_details
dev_langs:
- TSQL
helpviewer_keywords:
- fn_syscollector_get_execution_details function
ms.assetid: d59ddf0c-72c0-4c57-bc83-aef260e4e105
author: rothja
ms.author: jroth
ms.openlocfilehash: b2ed385026d2bd47912a1a95d237b2adedafa26d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68042825"
---
# <a name="fn_syscollector_get_execution_details-transact-sql"></a>fn_syscollector_get_execution_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma parte do log [!INCLUDE[ssIS](../../includes/ssis-md.md)] (sysssislog) que corresponde ao package_execution_id do pacote fornecido. A tabela contém uma linha para cada entrada de log gerada em tempo de execução por pacotes, trabalhos e contêineres.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_syscollector_get_execution_details ( log_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *log_id*  
 O identificador exclusivo local do log de execução. *log_id* é **int**.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|id|**int**|O identificador exclusivo da entrada do log.|  
|event|**sysname**|O nome do evento que gerou a entrada do log.|  
|computer|**nvarchar**|O computador no qual o pacote foi executado quando a entrada do log foi gerada.|  
|operador|**nvarchar**|O nome de usuário da pessoa ou agente que executou o pacote que gerou a entrada do log.|  
|source|**nvarchar**|O nome do executável que gerou a entrada do log.|  
|sourceid|**uniqueidentifier**|A GUID do executável que gerou a entrada do log.|  
|executionid|**uniqueidentifier**|A GUID da instância de execução do executável que gerou a entrada do log.|  
|starttime|**datetime**|A hora em que o pacote começou a ser executado.|  
|endtime|**datetime**|A hora em que o pacote foi concluído.|  
|datacode|**int**|Um valor inteiro que identifica o evento associado à entrada do log. "0" indica que o evento não forneceu nenhum identificador.|  
|databytes|**imagem**|Uma matriz de bytes que identifica um valor de retorno.|  
|mensagem|**nvarchar**|Uma descrição do evento e as informações associadas a ele.|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão SELECT para **dc_operator**.  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar log de pacote no SQL Server Data Tools](../../integration-services/performance/integration-services-ssis-logging.md#server_logging)   
 [Coleta de dados](../../relational-databases/data-collection/data-collection.md)  
  
  
