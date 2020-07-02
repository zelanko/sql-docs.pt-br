---
title: sys. fn_validate_plan_guide (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_validate_plan_guide
- sys.fn_validate_plan_guide_TSQL
- fn_validate_plan_guide
- fn_validate_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_validate_plan_guide function
- sys.fn_validate_plan_guide function
ms.assetid: 3af8b47a-936d-4411-91d1-d2d16dda5623
author: rothja
ms.author: jroth
ms.openlocfilehash: b7e0d440a453b0481a4440ec432669d3981b9da8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754006"
---
# <a name="sysfn_validate_plan_guide-transact-sql"></a>sys.fn_validate_plan_guide (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Verifica a validade do guia de plano especificado. A função sys.fn_validate_plan_guide retorna a primeira mensagem de erro encontrada quando o guia de plano é aplicado à consulta. Um conjunto de linhas vazio será retornado quando a guia de plano for válida. Guias de plano podem ficar inválidos depois que são feitas alterações ao design físico do banco de dados. Por exemplo, se um guia de plano especificar um determinado índice e esse índice depois for descartado, a consulta não poderá mais usar o guia de plano.  
  
 Validando um guia de plano, você pode determinar se o guia pode ser usado pelo otimizador sem modificação. Com base nos resultados da função, você pode optar por descartar o guia de plano e redefinir a consulta ou modificar o design do banco de dados, por exemplo, recriando o índice especificado no guia de plano.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.fn_validate_plan_guide ( plan_guide_id )  
```  
  
## <a name="arguments"></a>Argumentos  
 *plan_guide_id*  
 É a ID do guia de plano conforme relatado na exibição do catálogo [Sys. plan_guides](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md) . *plan_guide_id* é **int** sem padrão.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|msgnum|**int**|A identificação da mensagem de erro.|  
|severidade|**tinyint**|O nível de severidade da mensagem, entre 1 e 25.|  
|state|**smallint**|Número de estado do erro que indica o ponto no código no qual o erro ocorreu.|  
|message|**nvarchar(2048)**|Texto da mensagem do erro.|  
  
## <a name="permissions"></a>Permissões  
 Os guias de plano com escopo OBJECT exigem a permissão VIEW DEFINITION ou ALTER nas permissões e objetos mencionados para compilar a consulta ou o lote fornecido no guia de plano Por exemplo, se um lote contiver instruções SELECT, serão solicitadas permissões SELECT nos objetos mencionados.  
  
 Os guias de plano com escopo SQL ou TEMPLATE exigem a permissão ALTER nas permissões e no banco de dados para compilar a consulta ou o lote fornecido no guia de plano Por exemplo, se um lote contiver instruções SELECT, serão solicitadas permissões SELECT nos objetos mencionados.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-validating-all-plan-guides-in-a-database"></a>a. Validando todos os guias de plano em um banco de dados  
 O exemplo seguinte verifica a validade de todos os guias de plano no banco de dados atual. Se um conjunto de resultados vazio for retornado, todos os guias de plano serão válidos.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT plan_guide_id, msgnum, severity, state, message  
FROM sys.plan_guides  
CROSS APPLY fn_validate_plan_guide(plan_guide_id);  
GO  
```  
  
### <a name="b-testing-plan-guide-validation-before-implementing-a-change-to-the-database"></a>B. Testando a validação do guia de plano antes de implementar uma alteração no banco de dados  
 O exemplo seguinte usa uma transação explícita para descartar um índice. A `sys.fn_validate_plan_guide` função é executada para determinar se essa ação invalidará quaisquer guias de plano no banco de dados. Com base nos resultados da função, a instrução `DROP INDEX` será confirmada ou a transação será revertida, e o índice não será descartado.  
  
```sql  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DROP INDEX IX_SalesOrderHeader_CustomerID ON Sales.SalesOrderHeader;  
-- Check for invalid plan guides.  
IF EXISTS (SELECT plan_guide_id, msgnum, severity, state, message  
           FROM sys.plan_guides  
           CROSS APPLY sys.fn_validate_plan_guide(plan_guide_id))  
    ROLLBACK TRANSACTION;  
ELSE  
    COMMIT TRANSACTION;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Guias de plano](../../relational-databases/performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
  
