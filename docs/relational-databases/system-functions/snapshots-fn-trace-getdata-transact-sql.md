---
title: snapshots.fn_trace_getdata (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- snapshots.fn_trace_getdata
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots.fn_trace_getdata function
ms.assetid: ac28ef48-f4f4-4bf2-ba22-d44e1be88172
author: rothja
ms.author: jroth
ms.openlocfilehash: 8f342fd9dcf89b5d9862a2ed51718b09aae2e991
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771524"
---
# <a name="snapshotsfn_trace_getdata-transact-sql"></a>snapshots.fn_trace_getdata (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Essa função retorna todos os eventos capturados para o rastreamento especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
snapshots.fn_trace_gettable ( trace_info_id, start_time, end_time )  
```  
  
## <a name="arguments"></a>Argumentos  
 *trace_info_id*  
 O identificador exclusivo para a chave primária na tabela de instantâneos. trace_info no banco de dados de data warehouse de gerenciamento. *trace_info_id* é **int**.  
  
 *start_time*  
 A hora em que o rastreamento foi iniciado. *start_time* é **DateTime**.  
  
 *end_time*  
 A hora em que o rastreamento foi terminado. *end_time* é **DateTime**.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|\<All trace columns>|\<Varies>|Os dados de rastreamento da tabela snapshots.trace_data no banco de dados de data warehouse de gerenciamento.<br /><br /> Uma lista das colunas do rastreamento especificado pode ser obtida usando a seguinte consulta:<br /><br /> `SELECT * FROM sys.trace_columns`<br /><br /> **Observação:** As colunas retornadas pela função instantâneos. fn_trace_gettable correspondem aos valores na coluna nome na exibição do sistema sys. trace_columns. A única diferença é que a coluna GroupID não é retornada pela função.|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão SELECT para mdw_reader.  
  
## <a name="see-also"></a>Consulte Também  
 [Coleta de dados](../../relational-databases/data-collection/data-collection.md)  
  
  
