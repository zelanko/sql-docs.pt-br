---
title: sys.dm_exec_input_buffer (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/14/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_input_buffer
- sys.dm_exec_input_buffer _tsql
- dm_exec_input_buffer
- dm_exec_input_buffer_tsql
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_input_buffer dynamic management function
ms.assetid: fb34a560-bde9-4ad9-aa96-0d4baa4fc104
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4e18f635b7bbdd8fa96a565fef6aef5be5bde87f
ms.sourcegitcommit: 0c40843c13f67ba7d975f4fedb9d20d70747f66d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/15/2019
ms.locfileid: "74097876"
---
# <a name="sysdm_exec_input_buffer-transact-sql"></a>sys.dm_exec_input_buffer (Transact-SQL)

[!INCLUDE[tsql-appliesto-2014sp2-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-2014sp2-asdb-xxxx-xxx-md.md)]

Retorna informações sobre as instruções enviadas a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="syntax"></a>Sintaxe

```
sys.dm_exec_input_buffer ( session_id , request_id )
```

## <a name="arguments"></a>Argumentos

*session_id* É a ID da sessão que executa o lote a ser pesquisado. *session_id* é **smallint**. *session_id* pode ser obtido dos seguintes objetos de gerenciamento dinâmico:

- [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
- [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)
- [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)

*request_id* O request_id de [Sys. dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md). *request_id* é **int**.

## <a name="table-returned"></a>Tabela retornada

|Nome da coluna|Data type|Descrição|
|-----------------|---------------|-----------------|
|**event_type**|**nvarchar(256)**|O tipo de evento no buffer de entrada para o SPID especificado.|
|**parameters**|**smallint**|Todos os parâmetros fornecidos para a instrução.|
|**event_info**|**nvarchar(max)**|O texto da instrução no buffer de entrada para o SPID especificado.|

## <a name="permissions"></a>Permissões

Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o usuário tiver a permissão VIEW SERVER STATE, o usuário verá todas as sessões em execução na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; caso contrário, o usuário verá apenas a sessão atual.

> [!IMPORTANT]
> A execução dessa DMV fora de SQL Server Management Studio contra SQL Server sem exibir permissões de estado do servidor (como em um gatilho, procedimento armazenado ou função) gera um erro de permissão no banco de dados mestre.

Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)], se o usuário for o proprietário do banco de dados, o usuário verá todas as sessões em execução no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]; caso contrário, o usuário verá apenas a sessão atual.

> [!IMPORTANT]
> A execução dessa DMV fora do SQL Server Management Studio no banco de dados SQL do Azure sem permissões de proprietário (como em um gatilho, procedimento armazenado ou função) gera um erro de permissão no banco de dados mestre.

## <a name="remarks"></a>Remarks

Essa função de gerenciamento dinâmico pode ser usada em conjunto com sys. dm_exec_sessions ou sys. dm_exec_requests fazendo a **aplicação cruzada**.

## <a name="examples"></a>Exemplos

### <a name="a-simple-example"></a>A. Exemplo simples

O exemplo a seguir demonstra a passagem de uma ID de sessão (SPID) e uma ID de solicitação para a função.

```sql
SELECT * FROM sys.dm_exec_input_buffer (52, 0);
GO
```

### <a name="b-using-cross-apply-to-additional-information"></a>b. Usando Cross aplicar a informações adicionais

O exemplo a seguir lista o buffer de entrada para sessões com ID de sessão maior que 50.

```sql
SELECT es.session_id, ib.event_info
FROM sys.dm_exec_sessions AS es
CROSS APPLY sys.dm_exec_input_buffer(es.session_id, NULL) AS ib
WHERE es.session_id > 50;
GO
```

## <a name="see-also"></a>Consulte também

- [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)
- [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)
- [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
- [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)
