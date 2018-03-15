---
title: SET FMTONLY (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FMTONLY_TSQL
- FMTONLY
- SET FMTONLY
- SET_FMTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server], only metadata returned
- SET FMTONLY statement
- FMTONLY option
ms.assetid: 02a1d9ac-2e58-433c-9a07-2c5a4a2214e1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 38625e3079956032513bb0e26c5d37b9a7071fea
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="set-fmtonly-transact-sql"></a>SET FMTONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna apenas metadados ao cliente. Pode ser usado para testar o formato da resposta sem realmente executar a consulta.  
  
> [!NOTE]  
>  Não use este recurso. Esse recurso foi substituído por [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md), [sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md), [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md) e [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SET FMTONLY { ON | OFF }   
```  
  
## <a name="remarks"></a>Remarks  
 Nenhuma linha é processada ou enviada ao cliente devido à solicitação quando SET FMTONLY está ON.  
  
 A configuração de SET FMTONLY é definida no momento da execução e não no momento da análise.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função public.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>A: Exibir as informações de cabeçalho de coluna para uma consulta sem realmente executar a consulta.  
 O exemplo a seguir altera a configuração de `SET FMTONLY` para `ON` e executa uma instrução `SELECT`. A configuração faz com que a instrução retorne apenas a informações de coluna; nenhuma linha de dados é retornada.  
  
```  
USE AdventureWorks2012;  
GO  
SET FMTONLY ON;  
GO  
SELECT *   
FROM HumanResources.Employee;  
GO  
SET FMTONLY OFF;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>B. Exiba as informações de cabeçalho de coluna para uma consulta sem realmente executar a consulta.  
 O exemplo a seguir mostra como retornar apenas as informações de cabeçalho (metadados) de coluna para uma consulta. O lote começa com FMTONLY definido como OFF e alterações FMTONLY ON antes da instrução SELECT. Isso faz com que a instrução SELECT retorne somente os cabeçalhos de coluna; nenhuma linha de dados é retornada.  
  
```  
-- Uses AdventureWorks  
  
BEGIN  
    SET FMTONLY OFF;  
    SET DATEFORMAT mdy;  
    SET FMTONLY ON;  
    SELECT * FROM dbo.DimCustomer;  
    SET FMTONLY OFF;  
END  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

