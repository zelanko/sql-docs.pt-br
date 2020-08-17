---
description: sys.fn_cdc_is_bit_set (Transact-SQL)
title: sys.fn_cdc_is_bit_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_cdc_is_bit_set
- sys.fn_cdc_is_bit_set_TSQL
- sys.fn_cdc_is_bit_set
- fn_cdc_is_bit_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_cdc_is_bit_set
- fn_cdc_is_bit_set
ms.assetid: 792fe7cf-b3b8-4f25-8329-78d63f0e6921
author: rothja
ms.author: jroth
ms.openlocfilehash: ab93830bd9e2b164f5b76412b2b412dc095c6c9c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88321612"
---
# <a name="sysfn_cdc_is_bit_set-transact-sql"></a>sys.fn_cdc_is_bit_set (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Indica se uma coluna capturada foi atualizada verificando se sua posição ordinal está definida em um bitmask fornecido.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_cdc_is_bit_set ( position , update_mask )  
```  
  
## <a name="arguments"></a>Argumentos  
 *propostas*  
 É a posição ordinal na máscara a ser verificada. a *posição* é **int**.  
  
 *update_mask*  
 É a máscara que identifica colunas atualizadas. *update_mask* é **varbinary (128)**.  
  
## <a name="return-type"></a>Tipo de retorno  
 **bit**  
  
## <a name="remarks"></a>Comentários  
 Esta função é geralmente usada como parte de uma consulta de dados de alteração, a fim de indicar se a coluna foi alterada. Nesse cenário, a função [Sys. fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) é usada antes da consulta para obter o ordinal de coluna necessário. **Sys. fn_cdc_is_bit_set** é então aplicado a cada linha de dados de alteração que é retornada, fornecendo as informações específicas de coluna como parte do conjunto de resultados retornado.  
  
 É recomendável usar essa função em vez da função [Sys. fn_cdc_has_column_changed](../../relational-databases/system-functions/sys-fn-cdc-has-column-changed-transact-sql.md) ao determinar se as colunas foram alteradas para todas as linhas de um conjunto de resultados retornado.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `sys.fn_cdc_is_bit_set` para preceder ao conjunto de resultados gerado pela função de consulta `cdc.fn_cdc_get_all_changes_HR_Department` a coluna '`IsGroupNmUpdated`' usando o ordinal da coluna pré-computada e o valor de `__$update_mask` como argumentos para a chamada.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10), @GroupNm_ordinal int;  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HR_Department');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SET @GroupNm_ordinal = sys.fn_cdc_get_column_ordinal('HR_Department','GroupName');  
  
SELECT sys.fn_cdc_is_bit_set(@GroupNm_ordinal,__$update_mask) as 'IsGroupNmUpdated', *  
FROM cdc.fn_cdc_get_all_changes_HR_Department( @from_lsn, @to_lsn, 'all')  
WHERE __$operation = 4;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções da captura de dados de alterações &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)   
 [sys. fn_cdc_get_column_ordinal &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md)   
 [sys. fn_cdc_has_column_changed &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-has-column-changed-transact-sql.md)   
 [CDC. fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [CDC. fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
