---
title: Função SQLCompleteAsync | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 736867be33531a73c0ada66a3be0f1245f1c483a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537596"
---
# <a name="sqlcompleteasync-function"></a>Função SQLCompleteAsync
**Conformidade com**  
 Versão introduzida: ODBC 3.8  
  
 Conformidade com padrões: None  
  
 **Resumo**  
 **SQLCompleteAsync** pode ser usado para determinar quando uma função assíncrona é concluída usando qualquer processamento baseado em notificação ou sondagem. Para obter mais informações sobre as operações assíncronas, consulte [execução assíncrona](../../../odbc/reference/develop-app/asynchronous-execution.md).  
  
 **SQLCompleteAsync** é implementada somente no Gerenciador de Driver ODBC.  
  
 No modo de processamento assíncrono de notificação com base **SQLCompleteAsync** deve ser chamado depois que o Gerenciador de Driver gera o objeto de evento usado para notificação. **SQLCompleteAsync** conclusão assíncrona processamento e a função assíncrona irá gerar um código de retorno.  
  
 No modo de processamento assíncrono de sondagem com base **SQLCompleteAsync** é uma alternativa a chamar a função assíncrona original, sem a necessidade de especificar os argumentos na chamada de função assíncrona original. **SQLCompleteAsync** pode ser usado independentemente se a biblioteca de cursores ODBC está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] O tipo do identificador no qual concluir assíncrona de processamento. Os valores válidos são SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
 *Handle*  
 [Entrada] O identificador no qual concluir assíncrona de processamento. Se *manipular* não é um identificador válido do tipo especificado por *HandleType*, **SQLCompleteAsync** retorne SQL_INVALID_HANDLE.  
  
 Se *manipular* não é um identificador válido do tipo especificado por *HandleType*, **SQLCompleteAsync** retorne SQL_INVALID_HANDLE.  
  
 *AsyncRetCodePtr*  
 [Saída] Ponteiro para um buffer que conterá o código de retorno da API assíncrona. Se *AsyncRetCodePtr* for NULL, **SQLCompleteAsync** retornará SQL_ERROR.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Se **SQLCompleteAsync** retorna SQL_SUCCESS, um aplicativo deve obter o código de retorno da função assíncrona do buffer apontado por *AsyncRetCodePtr*. O SQLSTATE associado, se houver, pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um identificador de instrução ou uma *HandleType* de SQL _ HANDLE_DBC e um identificador de conexão. Esses registros de diagnóstico estão associados com a função assíncrona, não desta **SQLCompleteAsync** função.  
  
 **SQLCompleteAsync** retorna um código diferente de SQL_SUCCESS para indicar que **SQLCompleteAsync** não é chamado. **SQLCompleteAsync** não postará nesse caso, qualquer registro de diagnóstico. Códigos de retorno possíveis são:  
  
-   SQL_INVALID_HANDLE: O identificador é indicado por *HandleType* e *manipular* não é um identificador válido.  
  
-   SQL_ERROR: *AsyncRetCodePtr* é NULL ou processamento assíncrono não está habilitado no identificador.  
  
-   SQL_NO_DATA: No modo de notificação, uma operação assíncrona não está em andamento ou o Gerenciador de Driver não notificou o aplicativo. No modo de sondagem, uma operação assíncrona não está em andamento.  
  
## <a name="comments"></a>Comentários  
 No modo de processamento assíncrono de sondagem com base *AsyncRetCodePtr* pode ser SQL_STILL_EXECUTING quando **SQLCompleteAsync** retorna SQL_SUCCESS. Aplicativo deve manter sondagem até *AsyncRetCodePtr* não é SQL_STILL_EXECUTING. No modo de processamento assíncrono de notificação com base *AsyncRetCodePtr* nunca será SQL_STILL_EXECUTING.  
  
## <a name="see-also"></a>Consulte também  
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
