---
title: sys.fn_cdc_map_time_to_lsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
applies_to:
- SQL Server (starting with 2008)
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
caps.latest.revision: 23
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f463c01205b574334dd52263cb056f3a2daea62f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysfncdcmaptimetolsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o valor LSN (número) de sequência de log da **start_lsn** coluna o [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabela do sistema para o tempo especificado. Você pode usar essa função para mapear sistematicamente intervalos de data e hora para o intervalo de LSN necessário para as funções de enumeração do change data capture [CDC. fn_cdc_get_all_changes_ < instância_de_captura >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) e [cdc.fn _cdc_get_net_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) para retornar as alterações de dados dentro do intervalo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 **'**< relational_operator >**'** {maior menor que | maior menor que ou igual | menor maior que | menor maior que ou igual}  
 É usado para identificar um valor do LSN distinto dentro de **CDC. lsn_time_mapping** tabela com um tipo de **tran_end_time** que satisfaz a relação quando comparado com o *tracking_time*  valor.  
  
 *relational_operator* é **nvarchar (30)**.  
  
 *tracking_time*  
 É o valor de data e hora ao qual corresponder. *tracking_time* é **datetime**.  
  
## <a name="return-type"></a>Tipo de retorno  
 **binary(10)**  
  
## <a name="remarks"></a>Remarks  
 Para entender como o **fn_cdc_map_time_lsn** pode ser usado para mapear os intervalos de data e hora para intervalos LSN, considere o cenário a seguir. Presuma que um consumidor queira extrair dados de alteração diariamente. Ou seja, o consumidor deseja apenas as alterações de um determinado dia até a meia-noite. O limite inferior do intervalo de tempo deve ir até, mas não incluir, a meia-noite do dia anterior. O limite superior deve ir até e incluir a meia-noite do dia determinado. A exemplo a seguir mostra como a função **fn_cdc_map_time_to_lsn** pode ser usado para mapear sistematicamente esse intervalo de tempo para o intervalo de LSN que as funções de enumeração do change data capture para retornar todos os alterações dentro desse intervalo.  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 O operador relacional '`smallest greater than`' é usado para restringir mudanças àquelas que ocorrem após a meia-noite do dia anterior. Se várias entradas com diferente valores LSN compartilhamento o **tran_end_time** valor identificado como o limite inferior no [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabela, a função retornará o menor LSN assegurando que todas as entradas são incluídas. Para o limite superior, o operador relacional '`largest less than or equal to`' é usado para garantir que o intervalo inclui todas as entradas para o dia, incluindo aquelas que tem meia-noite como seu **tran_end_time** valor. Se várias entradas com diferente valores LSN compartilhamento o **tran_end_time** valor identificado como o limite superior, a função retornará o maior LSN assegurando que todas as entradas foram incluídas.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa o `sys.fn_cdc_map_time_lsn` função para determinar se há quaisquer linhas no [CDC. lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) de tabela com um **tran_end_time** valor que é maior que ou igual a meia-noite. Essa consulta pode ser usada para determinar, por exemplo, se o processo de captura já processou as alterações confirmadas desde meia-noite do dia anterior, de forma que a extração de dados de alteração para esse dia possa prosseguir.  
  
```  
DECLARE @extraction_time datetime, @lsn binary(10);  
SET @extraction_time = '2007-01-01 12:00:00.000';  
SELECT @lsn = sys.fn_cdc_map_time_to_lsn ('smallest greater than or equal', @extraction_time);  
IF @lsn IS NOT NULL  
BEGIN  
<some action>  
END  
```  
  
## <a name="see-also"></a>Consulte também  
 [cdc.lsn_time_mapping &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [sys.fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
