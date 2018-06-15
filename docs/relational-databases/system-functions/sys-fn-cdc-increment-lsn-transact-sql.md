---
title: sys.fn_cdc_increment_lsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- fn_cdc_increment_lsn_TSQL
- sys.fn_cdc_increment_lsn_TSQL
- sys.fn_cdc_increment_lsn
- fn_cdc_increment_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_increment_lsn
- sys.fn_cdc_increment_lsn
ms.assetid: e53b6703-358b-4c9a-912a-8f7c7331069b
caps.latest.revision: 18
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9202afab2c6b0fca9c230a60b1448a3069232d58
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33234357"
---
# <a name="sysfncdcincrementlsn-transact-sql"></a>sys.fn_cdc_increment_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o próximo LSN (número de sequência de log) da sequência com base no LSN especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_cdc_increment_lsn ( lsn_value )  
```  
  
## <a name="arguments"></a>Argumentos  
 *lsn_value*  
 Valor do LSN. *lsn_value* é **binário (10)**.  
  
## <a name="return-type"></a>Tipo de retorno  
 **binary(10)**  
  
## <a name="remarks"></a>Remarks  
 O valor de LSN retornado pela função é sempre superior ao valor especificado e nenhum valor de LSN pode existir entre os dois valores.  
  
 Para consultar sistematicamente um fluxo de alteração de dados ao longo do tempo, você pode periodicamente repetir a função de chamada de consulta sempre especificando um novo intervalo de consulta para limitar as mudanças retornadas na consulta. Para garantir que nenhum dado seja perdido, o limite superior da consulta anterior é frequentemente usado para gerar o limite inferior da consulta subsequente. Como o intervalo de consulta é um intervalo fechado, o novo limite inferior deve ser maior do que o limite superior anterior, mas pequeno o suficiente para garantir que nenhuma alteração tenha valores de LSN que se enquadrem entre esse valor e o limite superior antigo. A função sys.fn_cdc_increment_lsn é usada para obter esse valor.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função pública do banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `sys.fn_cdc_increment_lsn` para gerar um novo valor de limite inferior para uma consulta Change Data Capture com base no limite superior salvo de uma consulta anterior e salvo na variável `@save_to_lsn`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10), @save_to_lsn binary(10);  
SET @save_to_lsn = <previous_upper_bound_value>;  
SET @from_lsn = sys.fn_cdc_increment_lsn(@save_to_lsn);  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SELECT * from cdc.fn_cdc_get_all_changes_HumanResources_Employee( @from_lsn, @to_lsn, 'all' );  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.fn_cdc_decrement_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
