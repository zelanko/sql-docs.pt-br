---
description: DBCC INPUTBUFFER (Transact-SQL)
title: DBCC INPUTBUFFER (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC INPUTBUFFER
- INPUTBUFFER
- DBCC_INPUTBUFFER_TSQL
- INPUTBUFFER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- input buffers [SQL Server]
- last statement from client
- displaying last statement sent
- statements [SQL Server], last statement
- DBCC INPUTBUFFER statement
ms.assetid: a44d702b-b3fb-4950-8c8f-1adcf3f514ba
author: pmasl
ms.author: umajay
ms.openlocfilehash: a76fab0c7e0b7e15beb0eb094de4aa66e1644b2e
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115001"
---
# <a name="dbcc-inputbuffer-transact-sql"></a>DBCC INPUTBUFFER (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Exibe a última instrução enviada de um cliente para uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DBCC INPUTBUFFER ( session_id [ , request_id ])  
[WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*session_id*  
É a ID da sessão associada a cada conexão primária ativa.  
  
*request_id*  
É a solicitação exata (lote) para pesquisar na sessão atual.  

A seguinte consulta retorna *request_id*:  
```sql
SELECT request_id   
FROM sys.dm_exec_requests   
WHERE session_id = @@spid;  
```  
WITH  
Permite que opções sejam especificadas.  
  
NO_INFOMSGS  
Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC INPUTBUFFER retorna um conjunto de linhas com as seguintes colunas.
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**EventType**|**nvarchar(30)**|Tipo de evento. Pode ser **Evento de RPC** ou **Evento de Linguagem**. A saída será **Nenhum Evento** quando não for detectado nenhum último evento.|  
|**Parâmetros**|**smallint**|0 = Texto<br /><br /> 1- *n* = Parâmetros|  
|**EventInfo**|**nvarchar(4000)**|Para um **EventType** de RPC, **EventInfo** contém apenas o nome do procedimento. Para um **EventType** de Language, são exibidos apenas os primeiros 4.000 caracteres do evento.|  
  
Por exemplo, DBCC INPUTBUFFER retorna o conjunto de resultados a seguir quando o último evento no buffer é DBCC INPUTBUFFER(11).
  
```
EventType      Parameters EventInfo               
-------------- ---------- ---------------------   
Language Event 0          DBCC INPUTBUFFER (11)  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  

> [!NOTE]
> Começando pelo [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2, use [sys.dm_exec_input_buffer](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md) para retornar informações sobre as instruções enviadas a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="permissions"></a>Permissões  
No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é necessário um dos seguintes:
-   O usuário deve ser membro da função de servidor fixa **sysadmin**.  
-   O usuário deve ter a permissão VIEW SERVER STATE.  
-   *session_id* deve ser igual à ID de sessão na qual o comando está sendo executado. Para determinar a ID de sessão, execute a seguinte consulta:  
  
```sql
SELECT @@spid;  
```
  
No [!INCLUDE[ssSDS](../../includes/sssds-md.md)], as camadas Premium e Comercialmente Críticas requerem a permissão VIEW DATABASE STATE no banco de dados. No [!INCLUDE[ssSDS](../../includes/sssds-md.md)], as camadas Standard, Básica e de Uso Geral requerem a conta do administrador [!INCLUDE[ssSDS](../../includes/sssds-md.md)].
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir executa `DBCC INPUTBUFFER` em uma segunda conexão enquanto uma transação longa é executada em uma conexão anterior.
  
```sql
CREATE TABLE dbo.T1 (Col1 INT, Col2 CHAR(3));  
GO  
DECLARE @i INT = 0;  
BEGIN TRAN  
SET @i = 0;  
WHILE (@i < 100000)  
BEGIN  
INSERT INTO dbo.T1 VALUES (@i, CAST(@i AS CHAR(3)));  
SET @i += 1;  
END;  
COMMIT TRAN;  
--Start new connection #2.  
DBCC INPUTBUFFER (52);  
```  

## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[sys.dm_exec_input_buffer &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)
  
  
