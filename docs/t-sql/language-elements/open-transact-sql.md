---
title: Abrir (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPEN_TSQL
- OPEN
dev_langs: TSQL
helpviewer_keywords:
- opening cursors
- cursors [SQL Server], opening
- populating cursors [SQL Server]
- OPEN statement
- Transact-SQL cursors, opening
ms.assetid: fd1c5e3b-6045-4a42-b646-3fca76e874c1
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: aec83ff9ef56b4d4ae02867d4055d0b1e38f41ec
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="open-transact-sql"></a>OPEN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Abre uma [!INCLUDE[tsql](../../includes/tsql-md.md)] cursor de servidor e popula o cursor executando o [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução especificada no DECLARE CURSOR ou conjunto *cursor_variable* instrução.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
OPEN { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
## <a name="arguments"></a>Argumentos  
 GLOBAL  
 Especifica que *cursor_name* refere-se a um cursor global.  
  
 *cursor_name*  
 É o nome do cursor declarado. Se uma global e um cursor local existirem com *cursor_name* como seu nome, *cursor_name* refere-se ao cursor global se GLOBAL for especificado; caso contrário, *cursor_name* refere-se ao cursor local.  
  
 *cursor_variable_name*  
 É o nome de uma variável de cursor que faz referência a um cursor.  
  
## <a name="remarks"></a>Comentários  
 Se o cursor for declarado com a opção INSENSITIVE ou STATIC, OPEN criará uma tabela temporária para manter o conjunto de resultados. OPEN falha quando o tamanho de qualquer linha no conjunto de resultados excede o tamanho máximo de linha para tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o cursor for declarado com a opção KEYSET, OPEN criará uma tabela temporária para manter o conjunto de chaves. As tabelas temporárias são armazenadas em tempdb.  
  
 Depois que um cursor foi aberto, use o @@CURSOR_ROWS linhas de função a receber o número de qualificação no último cursor aberto.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte à geração de cursores [!INCLUDE[tsql](../../includes/tsql-md.md)] controlados por conjunto de chaves ou estáticos de forma assíncrona. [!INCLUDE[tsql](../../includes/tsql-md.md)] , como OPEN ou FETCH, são em lote, de modo que não é preciso gerar cursores [!INCLUDE[tsql](../../includes/tsql-md.md)] assincronamente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] continua a dar suporte a cursores de servidor de API (interface de programação de aplicativo) estáticos ou controlados por conjunto de chaves assíncronos nos quais OPEN de baixa latência é uma preocupação devido às viagens de ida e volta do cliente para cada operação de cursor.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir abre um cursor e busca todas as linhas.  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT LastName, FirstName  
FROM AdventureWorks2012.HumanResources.vEmployee  
WHERE LastName like 'B%';  
  
OPEN Employee_Cursor;  
  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    FETCH NEXT FROM Employee_Cursor  
END;  
  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Fechar &#40; Transact-SQL &#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [@@CURSOR_ROWS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-rows-transact-sql.md)   
 [DESALOCAR &#40; Transact-SQL &#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)   
 [Busca &#40; Transact-SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
