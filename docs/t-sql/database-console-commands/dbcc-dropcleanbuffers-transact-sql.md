---
description: DBCC DROPCLEANBUFFERS (Transact-SQL)
title: DBCC DROPCLEANBUFFERS (Transact-SQL)
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROPCLEANBUFFERS
- DBCC_DROPCLEANBUFFERS_TSQL
- DROPCLEANBUFFERS_TSQL
- DBCC DROPCLEANBUFFERS
dev_langs:
- TSQL
helpviewer_keywords:
- clean buffers
- cold buffer cache
- buffer pools [SQL Server]
- dropping buffers
- removing buffers
- DBCC DROPCLEANBUFFERS statement
ms.assetid: a4121927-f2ce-4926-aa2c-9b1519dac048
author: pmasl
ms.author: umajay
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0e3f496f123e237858772a4a5cab5c8631acd448
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116905"
---
# <a name="dbcc-dropcleanbuffers-transact-sql"></a>DBCC DROPCLEANBUFFERS (Transact-SQL)

[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

Remove todos os buffers limpos do pool de buffers e os objetos de columnstore do pool de objetos columnstore.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe
Sintaxe para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:

```syntaxsql
DBCC DROPCLEANBUFFERS [ WITH NO_INFOMSGS ]  
```  
Sintaxe para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]:

```syntaxsql  
DBCC DROPCLEANBUFFERS ( COMPUTE | ALL ) [ WITH NO_INFOMSGS ]  
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas. As mensagens informativas sempre são suprimidas no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] e no [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
 COMPUTE  
 Limpar o cache de dados na memória de cada nó de computação.  
  
 ALL  
 Limpar o cache de dados na memória de cada nó de computação e do nó de controle. Esse será o padrão se você não especificar um valor.  
  
## <a name="remarks"></a>Comentários  
Use DBCC DROPCLEANBUFFERS para testar consultas com um cache de buffer a frio sem desligar e reiniciar o servidor.
Para remover buffers limpos dos objetos de columnstore e do pool de buffers do pool de objetos columnstore, primeiro use CHECKPOINT para produzir um cache de buffer frio. Isso faz com que todas as páginas de alterações para o banco de dados atual sejam gravadas no disco e limpa os buffers. Depois de fazer isso, você pode emitir o comando DBCC DROPCLEANBUFFERS para remover todos os buffers do pool de buffers.
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC DROPCLEANBUFFERS no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna:
  
```
DBCC execution completed. If DBCC printed error messages, contact your system administrator.  
```  
  
## <a name="permissions"></a>Permissões  
Exige associação na função de servidor fixa `sysadmin` para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
Exige associação na função de servidor fixa `DB_OWNER` para [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  
  
  
