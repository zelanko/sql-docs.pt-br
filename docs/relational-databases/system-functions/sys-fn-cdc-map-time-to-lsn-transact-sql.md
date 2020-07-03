---
title: sys.fn_cdc_map_time_to_lsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_map_time_to_lsn
- fn_cdc_map_time_to_lsn_TSQL
- sys.fn_cdc_map_time_to_lsn_TSQL
- fn_cdc_map_time_to_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_map_time_to_lsn
- sys.fn_cdc_map_time_to_lsn
ms.assetid: 6feb051d-77ae-4c93-818a-849fe518d1d4
author: rothja
ms.author: jroth
ms.openlocfilehash: a3cd283f09263d4f36f0f4e2cfd4a18767dd614e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898361"
---
# <a name="sysfn_cdc_map_time_to_lsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna o valor do LSN (número de sequência de log) da coluna **start_lsn** na tabela do sistema [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) para o tempo especificado. Você pode usar essa função para mapear sistematicamente os intervalos de DateTime para o intervalo baseado em LSN necessário para as funções de enumeração de captura de dados de alteração [CDC. fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) e [cdc. fn_cdc_get_net_changes_<](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) capture_instance a>para retornar alterações de dados dentro desse intervalo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_cdc_map_time_to_lsn ( '<relational_operator>', tracking_time )  
  
<relational_operator> ::=  
{  largest less than  
 | largest less than or equal  
 | smallest greater than  
 | smallest greater than or equal  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 **'**<relational_operator>**'** {maior menor que | maior que ou igual a | menor que | menor que ou igual a}  
 É usado para identificar um valor LSN distinto dentro da tabela **CDC. lsn_time_mapping** com um **tran_end_time** associado que satisfaça a relação em comparação com o valor de *tracking_time* .  
  
 *relational_operator* é **nvarchar (30)**.  
  
 *tracking_time*  
 É o valor de data e hora ao qual corresponder. *tracking_time* é **DateTime**.  
  
## <a name="return-type"></a>Tipo de retorno  
 **binary(10)**  
  
## <a name="remarks"></a>Comentários  
 Para entender como o **Sys. fn_cdc_map_time_lsn** pode ser usado para mapear intervalos de DateTime para intervalos LSN, considere o cenário a seguir. Presuma que um consumidor queira extrair dados de alteração diariamente. Ou seja, o consumidor deseja apenas as alterações de um determinado dia até a meia-noite. O limite inferior do intervalo de tempo deve ir até, mas não incluir, a meia-noite do dia anterior. O limite superior deve ir até e incluir a meia-noite do dia determinado. O exemplo a seguir mostra como a função **Sys. fn_cdc_map_time_to_lsn** pode ser usada para mapear sistematicamente esse intervalo com base no tempo para o intervalo baseado em LSN necessário para as funções de enumeração de captura de dados de alteração para retornar todas as alterações dentro desse intervalo.  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 O operador relacional '`smallest greater than`' é usado para restringir mudanças àquelas que ocorrem após a meia-noite do dia anterior. Se várias entradas com valores LSN diferentes compartilharem o valor de **tran_end_time** identificado como o limite inferior na tabela [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) , a função retornará o menor LSN, garantindo que todas as entradas sejam incluídas. Para o limite superior, o operador relacional ' `largest less than or equal to` ' é usado para garantir que o intervalo inclua todas as entradas para o dia, incluindo aquelas que têm meia-noite como seu valor **tran_end_time** . Se várias entradas com valores LSN diferentes compartilharem o valor de **tran_end_time** identificado como o limite superior, a função retornará o maior LSN, garantindo que todas as entradas sejam incluídas.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa a `sys.fn_cdc_map_time_lsn` função para determinar se há alguma linha na tabela [cdc. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) com um valor de **tran_end_time** maior ou igual à meia-noite. Essa consulta pode ser usada para determinar, por exemplo, se o processo de captura já processou as alterações confirmadas desde meia-noite do dia anterior, de forma que a extração de dados de alteração para esse dia possa prosseguir.  
  
```  
DECLARE @extraction_time datetime, @lsn binary(10);  
SET @extraction_time = '2007-01-01 12:00:00.000';  
SELECT @lsn = sys.fn_cdc_map_time_to_lsn ('smallest greater than or equal', @extraction_time);  
IF @lsn IS NOT NULL  
BEGIN  
<some action>  
END  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CDC. lsn_time_mapping &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [sys. fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [CDC. fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
