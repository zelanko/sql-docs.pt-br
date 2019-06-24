---
title: SET RESULT SET CACHING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 561e92512ded10b06926f5b23f0f5d40540e3d2d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66826869"
---
# <a name="set-result-set-caching-transact-sql-applies-to-azure-sql-data-warehouse-gen2-only-preview"></a>SET RESULT SET CACHING (Transact-SQL) Aplica-se somente ao SQL Data Warehouse do Azure Gen2 (versão prévia)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

Faz com que o SQL Data Warehouse do Azure armazene em cache os conjuntos de resultados de consulta.
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Remarks  

> [!Note]
> Embora esse recurso esteja sendo distribuído para todas as regiões, verifique a versão implantada em sua instância e as [notas sobre a versão mais recente do SQL DW do Azure](/azure/sql-data-warehouse/release-notes-10-0-10106-0) para obter a disponibilidade de recursos.
  
Este comando deve ser executado enquanto estiver conectado ao banco de dados mestre.  A alteração dessa configuração de banco de dados entra em vigor imediatamente.  Os custos de armazenamento são incorridos pelo armazenamento em cache dos conjuntos de resultados da consulta. Depois de desabilitar o armazenamento em cache de resultados de um banco de dados, o cache de resultados anteriormente persistente será excluído imediatamente do armazenamento do SQL Data Warehouse do Azure. Uma nova coluna chamada is_result_set_caching_on é introduzida no [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql?view=azure-sqldw-latest) para mostrar a configuração de armazenamento em cache de resultados de um banco de dados.  

**ON** Especifica que os conjuntos de resultados de consulta retornados desse banco de dados serão armazenados em cache no armazenamento do SQL Data Warehouse do Azure.

**OFF** Especifica que os conjuntos de resultados de consulta retornados desse banco de dados não serão armazenados em cache no armazenamento do SQL Data Warehouse do Azure.

Os usuários podem determinar se uma consulta foi executada com um acerto ou erro do cache de resultados, consultando [sys.pdw_request_steps](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql?view=azure-sqldw-latest) com um request_id específico. Se houver um acerto de cache, o resultado da consulta terá uma única etapa com os seguintes detalhes:

|**Nome da coluna**|**Operador**|**Value**|
|----|----|----|
|operation_type|=|ReturnOperation|
|step_index|=|0|
|location_type|=|Control|
|command|Como|%DWResultCacheDb%|
||||
  
## <a name="permissions"></a>Permissões

Requer estas permissões:

- Logon da entidade de segurança no nível do servidor (aquele criado pelo processo de provisionamento) ou
- Membro da função de banco de dados dbmanager.

O proprietário do banco de dados não pode alterar o banco de dados, a menos que ele seja membro da função dbmanager.
  
## <a name="examples"></a>Exemplos

### <a name="enable-result-set-caching-for-a-database"></a>Habilitar o armazenamento em cache do conjunto de resultados de um banco de dados

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING ON;
```

### <a name="disable-result-set-caching-for-a-database"></a>Desabilitar o armazenamento em cache do conjunto de resultados de um banco de dados

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING OFF;
```

### <a name="check-result-set-caching-setting-for-a-database"></a>Verificar a configuração do armazenamento em cache do conjunto de resultados para um banco de dados

```sql
SELECT name, is_result_set_caching_on  
FROM sys.databases
```

### <a name="check-for-number-of-queries-with-result-set-cache-hit-and-cache-miss"></a>Verificar o número de consultas com acerto e erro de cache do conjunto de resultados

```sql
SELECT  
Queries=CacheHits+CacheMisses,
CacheHits,
CacheMisses,
CacheHitPct=CacheHits*1.0/(CacheHits+CacheMisses)
FROM  
(SELECT  
CacheHits=count(distinct case when s.command like '%DWResultCacheDb%' and
r.resource_class IS NULL and s.operation_type = 'ReturnOperation' and  
s.step_index = 0 then s.request_id else null end) ,
CacheMisses=count(distinct case when r.resource_class IS NOT NULL then  
s.request_id else null end)
     FROM sys.dm_pdw_request_steps s  
     JOIN sys.dm_pdw_exec_requests r  
     ON s.request_id = r.request_id) A
```

### <a name="check-for-result-set-cache-hit-or-cache-miss-for-a-query"></a>Verificar se há acerto ou erro de cache do conjunto de resultados para uma consulta

```sql
If
(SELECT step_index  
FROM sys.dm_pdw_request_steps  
WHERE request_id = 'QID58286'
      and operation_type = 'ReturnOperation'
      and command like '%DWResultCacheDb%') = 0
SELECT 1 as is_cache_hit  
ELSE
SELECT 0 as is_cache_hit
```

### <a name="check-for-all-queries-with-result-set-cache-hits"></a>Verificar todas as consultas com acertos de cache do conjunto de resultados

```sql
SELECT *  
FROM sys.dm_pdw_request_steps  
WHERE command like '%DWResultCacheDb%' and step_index = 0
```

## <a name="see-also"></a>Confira também

[Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)</br>
[ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)