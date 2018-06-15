---
title: sys.fn_cdc_get_min_lsn (Transact-SQL) | Microsoft Docs
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
- sys.fn_cdc_get_min_lsn
- fn_cdc_get_min_lsn
- fn_cdc_get_min_lsn_TSQL
- sys.fn_cdc_get_min_lsn_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_min_lsn
- sys.fn_cdc_get_min_lsn
ms.assetid: bd49e28a-128b-4f6b-8545-6a2ec3f4afb3
caps.latest.revision: 17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4c4c6a9bf83e83628891104f0c95a6baefa08234
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33230437"
---
# <a name="sysfncdcgetminlsn-transact-sql"></a>sys.fn_cdc_get_min_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o valor da coluna start_lsn para a instância de captura especificada no [change_tables](../../relational-databases/system-tables/cdc-change-tables-transact-sql.md) tabela do sistema. Esse valor representa o ponto de extremidade inferior do intervalo de validade da instância de captura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_cdc_get_min_lsn ( 'capture_instance_name' )  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *capture_instance_name* **'**  
 É o nome da instância de captura. *capture_instance_name* é **sysname**.  
  
## <a name="return-types"></a>Tipos de retorno  
 **binary(10)**  
  
## <a name="remarks"></a>Remarks  
 Retorna 0x00000000000000000000 quando a instância de captura não existe ou quando o chamador não está autorizado a acessar os dados de alteração associados a uma instância de captura.  
  
 Essa função é usada normalmente para identificar o ponto de extremidade inferior da linha do tempo do Change Data Capture associado à instância de captura. Você também pode usar essa função para validar os pontos de extremidade de um intervalo de consulta que estejam dentro da linha de tempo da instância de captura antes de solicitar dados de alteração. É importante executar essas verificações porque o ponto de extremidade inferior da instância de captura é alterado quando a limpeza é executada nas tabelas de alteração. Se o período entre as solicitações de dados de alteração for significativo, mesmo um ponto de extremidade inferior que seja definido para o ponto de extremidade superior da solicitação de dados de alteração anterior poderá ficar fora da linha do tempo atual.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin ou na função de banco de dados fixa db_owner. Para todos os outros usuários, requer a permissão SELECT em todas as colunas capturadas na tabela de origem e, se uma função associada para a instância de captura tiver sido definida, faça associação nessa função de banco de dados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-the-minimum-lsn-value-for-a-specified-capture-instance"></a>A. Retornando o valor LSN mínimo de uma instância de captura especificada  
 O exemplo a seguir retorna o valor LSN mínimo da instância de captura `HumanResources_Employee` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2-12;  
GO  
SELECT sys.fn_cdc_get_min_lsn ('HumanResources_Employee')AS min_lsn;  
  
```  
  
### <a name="b-verifying-the-low-endpoint-of-a-query-range"></a>B. Verificando o ponto de extremidade inferior de um intervalo de consultas  
 O exemplo a seguir usa o valor LSN mínimo retornado por `sys.fn_cdc_get_min_lsn` para verificar se o ponto de extremidade inferior proposto para uma consulta de dados de alteração é válido para a linha do tempo atual de `HumanResources_Employee` da instância de captura. Esse exemplo assume que o LSN do ponto de extremidade superior anterior da instância de captura foi salvo e está disponível para definir a variável `@save_to_lsn`. Para a finalidade desse exemplo, `@save_to_lsn` é definido como 0x000000000000000000 para forçar a execução da seção de tratamento de erros.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @min_lsn binary(10), @from_lsn binary(10),@save_to_lsn binary(10), @to_lsn binary(10);  
-- Sets @save_to_lsn to the previous high endpoint saved from the last change data request.  
SET @save_to_lsn = 0x000000000000000000;  
-- Sets the upper endpoint for the query range to the current maximum LSN.  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
-- Sets the @min_lsn parameter to the current minimum LSN for the capture instance.  
SET @min_lsn = sys.fn_cdc_get_min_lsn ('HumanResources_Employee');  
-- Sets the low endpoint for the query range to the LSN that follows the previous high endpoint.  
SET @from_lsn = sys.fn_cdc_increment_lsn(@save_to_lsn);  
-- Tests to verify the low endpoint is valid for the current capture instance.  
IF (@from_lsn < @min_lsn)  
    BEGIN  
        RAISERROR('Low endpoint of the request interval is invalid.', 16, -1);  
    END  
ELSE  
-- Return the changes occurring within the query range.  
    SELECT * FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee(@from_lsn, @to_lsn, 'all');  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.fn_cdc_get_max_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md)   
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
