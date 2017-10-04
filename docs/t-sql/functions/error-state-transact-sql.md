---
title: ERROR_STATE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ERROR_STATE_TSQL
- ERROR_STATE
dev_langs:
- TSQL
helpviewer_keywords:
- messages [SQL Server], state
- ERROR_STATE function
- errors [SQL Server], state
- TRY...CATCH [SQL Server]
- CATCH block
- states [SQL Server], error numbers
ms.assetid: 6059af00-83fe-409f-ab7c-daad111bc671
caps.latest.revision: 39
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 98b5a1ecfbfd9efd84f8a5cc55454aaaec6f8423
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="errorstate-transact-sql"></a>ERROR_STATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Retorna o número de estado do erro que fez o bloco CATCH de uma construção TRY…CATCH ser executado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ERROR_STATE ( )  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="return-value"></a>Valor de retorno  
 Quando chamado em um bloco CATCH, retorna o número de estado de mensagem de erro que fez o bloco CATCH ser executado.  
  
 Retorna NULL se for chamado fora do escopo de um bloco CATCH.  
  
## <a name="remarks"></a>Comentários  
 Algumas mensagens de erro podem ser geradas em vários pontos no código para o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Por exemplo, um erro "1105" pode ser gerado para várias condições diferentes. Cada condição específica que gera o erro atribui um código de estado exclusivo.  
  
 Ao exibir bancos de dados de problemas conhecidos, como a Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)], é possível usar o número de estado para determinar se o problema registrado é o mesmo do erro que você encontrou. Por exemplo, se um Artigo da Base de Dados de Conhecimento descreve uma mensagem de erro 1105 com um estado 2, e a mensagem de erro 1105 que você recebeu tinha um estado 3, o erro provavelmente tem uma causa diferente daquela informada no artigo.  
  
 Um engenheiro de suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também pode usar o código de estado de um erro para encontrar o local no código de origem em que aquele código de erro está sendo gerado, o que pode fornecer outras ideias sobre como diagnosticar o problema.  
  
 ERROR_STATE pode ser chamado em qualquer lugar dentro do escopo de um bloco CATCH.  
  
 ERROR_STATE retorna o estado de erro, independentemente do número de vezes que ele é executado ou se é executado dentro do escopo do bloco CATCH. Isso é diferente de funções como @@ERROR, que retorna somente o número do erro na instrução imediatamente posterior àquela que causa um erro ou na primeira instrução de um bloco CATCH.  
  
 Em blocos CATCH aninhados, ERROR_STATE retorna o estado de erro específico do escopo do bloco CATCH no qual é referenciado. Por exemplo, o bloco CATCH de uma construção TRY...CATCH externa poderia ter uma construção TRY...CATCH aninhada. Dentro do bloco CATCH aninhado, ERROR_STATE retorna o estado do erro que invocou o bloco CATCH aninhado. Se ERROR_STATE for executado em um bloco CATCH externo, retornará o estado do erro que invocou aquele bloco CATCH.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-errorstate-in-a-catch-block"></a>A. Usando ERROR_STATE em um bloco CATCH  
 A exemplo a seguir mostra um `SELECT` instrução que gera um erro de divisão por zero. O estado do erro é retornado.  
  
```  
BEGIN TRY  
    -- Generate a divide by zero error  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_STATE() AS ErrorState;  
END CATCH;  
GO  
```  
  
### <a name="b-using-errorstate-in-a-catch-block-with-other-error-handling-tools"></a>B. Usando ERROR_STATE em um bloco CATCH com outras ferramentas de tratamento de erros  
 A exemplo a seguir mostra um `SELECT` instrução que gera um erro de divisão por zero. Junto com o estado de erro, são retornadas as informações relacionadas ao erro.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_LINE() AS ErrorLine,  
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-using-errorstate-in-a-catch-block"></a>C. Usando ERROR_STATE em um bloco CATCH  
 A exemplo a seguir mostra um `SELECT` instrução que gera um erro de divisão por zero. O estado do erro é retornado.  
  
```  
BEGIN TRY  
    -- Generate a divide by zero error  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT ERROR_STATE() AS ErrorState;  
END CATCH;  
GO  
```  
  
### <a name="d-using-errorstate-in-a-catch-block-with-other-error-handling-tools"></a>D. Usando ERROR_STATE em um bloco CATCH com outras ferramentas de tratamento de erros  
 A exemplo a seguir mostra um `SELECT` instrução que gera um erro de divisão por zero. Junto com o estado de erro, são retornadas as informações relacionadas ao erro.  
  
```  
BEGIN TRY  
    -- Generate a divide-by-zero error.  
    SELECT 1/0;  
END TRY  
BEGIN CATCH  
    SELECT  
        ERROR_NUMBER() AS ErrorNumber,  
        ERROR_SEVERITY() AS ErrorSeverity,  
        ERROR_STATE() AS ErrorState,  
        ERROR_PROCEDURE() AS ErrorProcedure,  
        ERROR_MESSAGE() AS ErrorMessage;  
END CATCH;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md)   
 [TRY...CATCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/try-catch-transact-sql.md)   
 [ERROR_LINE &#40;Transact-SQL&#41;](../../t-sql/functions/error-line-transact-sql.md)   
 [ERROR_MESSAGE &#40;Transact-SQL&#41;](../../t-sql/functions/error-message-transact-sql.md)   
 [ERROR_NUMBER &#40;Transact-SQL&#41;](../../t-sql/functions/error-number-transact-sql.md)   
 [ERROR_PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/functions/error-procedure-transact-sql.md)   
 [ERROR_SEVERITY &#40;Transact-SQL&#41;](../../t-sql/functions/error-severity-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)   
 [@@ERROR &#40;Transact-SQL&#41;](../../t-sql/functions/error-transact-sql.md)  
  
  


