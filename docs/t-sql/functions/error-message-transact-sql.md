---
title: ERROR_MESSAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ERROR_MESSAGE_TSQL
- ERROR_MESSAGE
dev_langs:
- TSQL
helpviewer_keywords:
- ERROR_MESSAGE function
- errors [SQL Server], text of
- messages [SQL Server], text of
- TRY...CATCH [SQL Server]
- CATCH block
ms.assetid: f32877a6-5f17-418c-a32c-5a1a344b3c45
caps.latest.revision: 53
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a49d8e24a71b43ba2f400abfbb71f26fe51386a8
ms.sourcegitcommit: 6e55a0a7b7eb6d455006916bc63f93ed2218eae1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2018
ms.locfileid: "35239216"
---
# <a name="errormessage-transact-sql"></a>ERROR_MESSAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Essa função retorna o texto da mensagem do erro que fez com que o bloco CATCH de um constructo TRY…CATCH fosse executado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ERROR_MESSAGE ( )   
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar(4000)**  
  
## <a name="return-value"></a>Valor retornado  
Quando chamado em um bloco CATCH, `ERROR_MESSAGE` retorna o texto completo da mensagem do erro que fez com que o bloco `CATCH` fosse executado. O texto inclui os valores fornecidos para qualquer parâmetro substituível, assim como comprimentos, nomes de objeto ou horas.  
  
`ERROR_MESSAGE` retorna NULL quando chamado fora do escopo de um bloco CATCH.  
  
## <a name="remarks"></a>Remarks  
`ERROR_MESSAGE` dá suporte a chamadas em qualquer lugar dentro do escopo de um bloco CATCH.  
  
`ERROR_MESSAGE` retorna uma mensagem de erro relevante, independentemente de quantas vezes ou de em que local ele é executado dentro do escopo do bloco `CATCH`. É diferente de uma função como @@ERROR, que retorna apenas um número de erro na instrução imediatamente após àquela que causa um erro.  
  
Em blocos `CATCH` aninhados, `ERROR_MESSAGE` retorna a mensagem de erro específica do escopo do bloco `CATCH` que referenciou esse bloco `CATCH`. Por exemplo, o bloco `CATCH` de um constructo TRY...CATCH externo poderia ter um constructo `TRY...CATCH` interno. Dentro desse bloco `CATCH` interno, `ERROR_MESSAGE` retorna a mensagem do erro que invocou o bloco `CATCH` interno. Se `ERROR_MESSAGE` é executado no bloco `CATCH` externo, ele retorna a mensagem do erro que invocou esse bloco `CATCH` externo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-errormessage-in-a-catch-block"></a>A. Usando ERROR_MESSAGE em um bloco CATCH  
Este exemplo a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. O bloco `CATCH` retorna a mensagem de erro.  
  
```  
  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  

-----------

(0 row(s) affected)

ErrorMessage
----------------------------------
Divide by zero error encountered.

(1 row(s) affected)

```  
  
### <a name="b-using-errormessage-in-a-catch-block-with-other-error-handling-tools"></a>B. Usando ERROR_MESSAGE em um bloco CATCH com outras ferramentas de tratamento de erros  
Este exemplo a seguir mostra uma instrução `SELECT` que gera um erro de divisão por zero. Juntamente com a mensagem de erro, o bloco `CATCH` retorna informações sobre esse erro.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  

-----------

(0 row(s) affected)

ErrorNumber ErrorSeverity ErrorState  ErrorProcedure  ErrorLine  ErrorMessage
----------- ------------- ----------- --------------- ---------- ----------------------------------
8134        16            1           NULL            4          Divide by zero error encountered.

(1 row(s) affected)

```
  

