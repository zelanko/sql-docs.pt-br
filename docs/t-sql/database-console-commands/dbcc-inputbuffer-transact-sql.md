---
title: DBCC INPUTBUFFER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 10/13/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 51
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 54e4c8309c290255cb2885fab04bb394bc453046
ms.openlocfilehash: 3d9b6acfbfef3125d6ee715708492de1cae2b3a2
ms.contentlocale: pt-br
ms.lasthandoff: 10/16/2017

---
# <a name="dbcc-inputbuffer-transact-sql"></a>DBCC INPUTBUFFER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Exibe a última instrução enviada de um cliente para uma instância de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DBCC INPUTBUFFER ( session_id [ , request_id ])  
[WITH NO_INFOMSGS ]  
```  
  
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
com  
Permite que opções sejam especificadas.  
  
NO_INFOMSGS  
Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC INPUTBUFFER retorna um conjunto de linhas com as seguintes colunas.
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**EventType**|**nvarchar (30)**|Tipo de evento. Isso pode ser **evento RPC** ou **eventos de linguagem**. A saída será **nenhum evento** quando nenhum último evento foi detectado.|  
|**Parâmetros**|**smallint**|0 = Texto<br /><br /> 1 -  *n*  = parâmetros|  
|**EventInfo**|**nvarchar(4000)**|Para uma **EventType** de RPC, **EventInfo** contém apenas o nome do procedimento. Para uma **EventType** de idioma, somente os primeiros 4000 caracteres do evento são exibidos.|  
  
Por exemplo, DBCC INPUTBUFFER retorna o conjunto de resultados a seguir quando o último evento no buffer é DBCC INPUTBUFFER(11).
  
```
EventType      Parameters EventInfo               
-------------- ---------- ---------------------   
Language Event 0          DBCC INPUTBUFFER (11)  
  
(1 row(s) affected)  
  
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  

> [!NOTE]
> Começando com [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2, use [sys.DM exec_input_buffer](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md) para retornar informações sobre instruções enviadas a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="permissions"></a>Permissões  
Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer um dos seguintes:
-   Usuário deve ser um membro do **sysadmin** função de servidor fixa.  
-   O usuário deve ter a permissão VIEW SERVER STATE.  
-   *session_id* deve ser igual à ID de sessão na qual o comando está sendo executado. Para determinar a ID de sessão, execute a seguinte consulta:  
  
```sql
SELECT @@spid;  
```
  
Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] camadas Premium requer a permissão VIEW DATABASE STATE no banco de dados. Em [!INCLUDE[ssSDS](../../includes/sssds-md.md)] camadas Standard e Basic requer o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] conta de administrador.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir executa `DBCC INPUTBUFFER` em uma segunda conexão enquanto uma transação longa é executada em uma conexão anterior.
  
```sql
CREATE TABLE dbo.T1 (Col1 int, Col2 char(3));  
GO  
DECLARE @i int = 0;  
BEGIN TRAN  
SET @i = 0;  
WHILE (@i < 100000)  
BEGIN  
INSERT INTO dbo.T1 VALUES (@i, CAST(@i AS char(3)));  
SET @i += 1;  
END;  
COMMIT TRAN;  
--Start new connection #2.  
DBCC INPUTBUFFER (52);  
```  

## <a name="see-also"></a>Consulte também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)  
[sys.DM exec_input_buffer &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-input-buffer-transact-sql.md)
  
  

