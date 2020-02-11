---
title: sys.fn_cdc_get_column_ordinal (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_get_column_ordinal
- fn_cdc_get_column_ordinal_TSQL
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal
ms.assetid: 4bb21a57-2b94-4208-8bdf-6a3e2681d881
author: rothja
ms.author: jroth
ms.openlocfilehash: 893c7b0a4c7c88c0fdc7bf89b01b61bfaae6f2f4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68046501"
---
# <a name="sysfn_cdc_get_column_ordinal-transact-sql"></a>sys.fn_cdc_get_column_ordinal (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o ordinal de coluna da coluna especificada, como aparece na [tabela de alteração](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) associada à instância de captura especificada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_cdc_get_column_ordinal ( 'capture_instance','column_name')  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *capture_instance* **'**  
 É o nome da instância de captura na qual a coluna especificada é identificada como uma coluna capturada. *capture_instance* é **sysname**.  
  
 **'** *column_name* **'**  
 É a coluna na qual os dados serão reportados. *column_name* é **sysname**.  
  
## <a name="return-type"></a>Tipo de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 Esta função é usada para identificar a posição ordinal de uma coluna capturada dentro da máscara de atualização do Change Data Capture. Ele é usado principalmente em conjunto com a função [Sys. fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) para extrair informações da máscara de atualização ao consultar dados de alteração.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT em todas as colunas capturadas da tabela de origem. Se uma função de banco de dados do componente do Change Data Capture estiver especificada para uma instância de captura, a associação naquela função também será requerida.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir obtém a posição ordinal da coluna `VacationHours`, na máscara de atualização para a instância de captura `HumanResources_Employee`. Esse valor é usado, então, na chamada para `sys.fn_cdc_is_bit_set`, para extrair informações da máscara de atualização retornada.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10),  @VacationHoursOrdinal int;  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SET @VacationHoursOrdinal = sys.fn_cdc_get_column_ordinal   
    ( 'HumanResources_Employee','VacationHours');  
SELECT *, sys.fn_cdc_is_bit_set(@VacationHoursOrdinal,  
    __$update_mask) as 'VacationHours'  
FROM cdc.fn_cdc_get_net_changes_HumanResources_Employee  
    ( @from_lsn, @to_lsn, 'all with mask');  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções da captura de dados de alterações &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [sys. sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [sys. sp_cdc_get_captured_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sys. fn_cdc_is_bit_set &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md)  
  
  
