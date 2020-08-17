---
description: sys.fn_cdc_get_max_lsn (Transact-SQL)
title: sys.fn_cdc_get_max_lsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_get_max_lsn
- fn_cdc_get_max_lsn
- fn_cdc_get_max_lsn_TSQL
- sys.fn_cdc_get_max_lsn_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_max_lsn
- sys.fn_cdc_get_max_lsn
ms.assetid: 93f3a4c8-b91f-4ebb-8e96-9397bb3a1c43
author: rothja
ms.author: jroth
ms.openlocfilehash: 314fac004523b27d5766cca264535dcca6dd058e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88322132"
---
# <a name="sysfn_cdc_get_max_lsn-transact-sql"></a>sys.fn_cdc_get_max_lsn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna o LSN (número de sequência de log) máximo da coluna start_lsn na tabela do sistema [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) . É possível usar essa função para retornar o ponto de extremidade superior da linha do tempo de captura de dados de alteração para qualquer instância de captura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_cdc_get_max_lsn ()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **binary(10)**  
  
## <a name="remarks"></a>Comentários  
 Essa função retorna o LSN máximo na coluna start_lsn da tabela [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) . Como tal, ele é o último LSN processado pelo processo de captura quando as alterações são propagadas para as tabelas de alteração do banco de dados. Ele serve como ponto de extremidade superior de todas as linhas do tempo associadas às instâncias de captura definidas para o banco de dados.  
  
 A função é tipicamente usada para obter um ponto de extremidade superior apropriado para um intervalo de consulta.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função pública do banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-maximum-lsn-value"></a>a. Retornando o valor LSN máximo  
 O exemplo a seguir retorna o LSN máximo para todas as instâncias de captura no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT sys.fn_cdc_get_max_lsn()AS max_lsn;  
```  
  
### <a name="b-setting-the-high-endpoint-of-a-query-range"></a>B. Definindo o ponto de extremidade superior de um intervalo de consulta  
 O exemplo a seguir usa o LSN máximo retornado por `sys.fn_cdc_get_max_lsn` para definir o ponto de extremidade superior de um intervalo de consulta da instância de captura `HumanResources_Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn(N'HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee(@from_lsn, @to_lsn, 'all');  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. fn_cdc_get_min_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
