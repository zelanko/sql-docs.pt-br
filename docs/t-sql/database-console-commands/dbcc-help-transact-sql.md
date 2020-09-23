---
description: DBCC HELP (Transact-SQL)
title: DBCC HELP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC HELP
- DBCC_HELP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC statement syntax information
- DBCC HELP statement
ms.assetid: 306092c6-4354-4e47-928b-606124fbdc6e
author: pmasl
ms.author: umajay
ms.openlocfilehash: 5a609cd126f131e59ac2ed09ef91df70021c1ca6
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116887"
---
# <a name="dbcc-help-transact-sql"></a>DBCC HELP (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

Retorna informações de sintaxe para o comando especificado DBCC.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DBCC HELP ( 'dbcc_statement' | @dbcc_statement_var | '?' )  
[ WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *dbcc_statement* |  *\@dbcc_statement_var*  
 É o nome do comando DBCC para o qual receber informações de sintaxe. Forneça somente a parte do comando DBCC que segue DBCC, por exemplo, CHECKDB em vez de DBCC CHECKDB.  
  
 ?  
 Retorna todos os comandos DBCC para os quais a Ajuda está disponível.  
  
 WITH NO_INFOMSGS  
 Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
DBCC HELP retorna um conjunto de resultados que exibe a sintaxe para o comando DBCC especificado.
  
## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** .
  
## <a name="examples"></a>Exemplos  
### <a name="a-using-dbcc-help-with-a-variable"></a>a. Usando DBCC HELP com uma variável  
O exemplo a seguir retorna informações de sintaxe para o DBCC `CHECKDB`.
  
```sql  
DECLARE @dbcc_stmt sysname;  
SET @dbcc_stmt = 'CHECKDB';  
DBCC HELP (@dbcc_stmt);  
GO  
```  
  
### <a name="b-using-dbcc-help-with-the--option"></a>B. Usando DBCC HELP com a opção Opção  
O exemplo seguinte retorna todas as instruções DBCC para as quais a Ajuda está disponível.
  
```sql  
DBCC HELP ('?');  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
