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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f56def542b71906d1e9432d724fdab8143ccb346
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279584"
---
# <a name="sqlcompleteasync-function"></a>Função SQLCompleteAsync
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,8: nenhuma  
  
 **Resumo**  
 **SQLCompleteAsync** pode ser usado para determinar quando uma função assíncrona é concluída usando o processamento baseado em notificação ou sondagem. Para obter mais informações sobre operações assíncronas, consulte [execução assíncrona](../../../odbc/reference/develop-app/asynchronous-execution.md).  
  
 **SQLCompleteAsync** é implementado apenas no Gerenciador de driver ODBC.  
  
 No modo de processamento assíncrono baseado em notificação, **SQLCompleteAsync** deve ser chamado depois que o Gerenciador de driver gerar o objeto de evento usado para notificação. **SQLCompleteAsync** conclui o processamento assíncrono e a função assíncrona irá gerar um código de retorno.  
  
 No modo de processamento assíncrono baseado em sondagem, **SQLCompleteAsync** é uma alternativa para chamar a função assíncrona original, sem a necessidade de especificar os argumentos na chamada de função assíncrona original. **SQLCompleteAsync** pode ser usado independentemente se a biblioteca de cursores ODBC está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 Entrada O tipo do identificador no qual concluir o processamento assíncrono. Os valores válidos são SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
 *Handle*  
 Entrada O identificador no qual concluir o processamento assíncrono. Se o *identificador* não for um identificador válido do tipo especificado por *HandleType*, **SQLCompleteAsync** retornará SQL_INVALID_HANDLE.  
  
 Se o *identificador* não for um identificador válido do tipo especificado por *HandleType*, **SQLCompleteAsync** retornará SQL_INVALID_HANDLE.  
  
 *AsyncRetCodePtr*  
 Der Ponteiro para um buffer que conterá o código de retorno da API assíncrona. Se *AsyncRetCodePtr* for nulo, **SQLCompleteAsync** retornará SQL_ERROR.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Se **SQLCompleteAsync** retornar SQL_SUCCESS, um aplicativo deverá obter o código de retorno da função assíncrona do buffer apontado por *AsyncRetCodePtr*. O SQLSTATE associado, se houver, pode ser obtido chamando **SQLGetDiagRec** com um *handletype* de SQL_HANDLE_STMT e um identificador de instrução ou um *HandleType* de SQL_HANDLE_DBC e um identificador de conexão. Esses registros de diagnóstico são associados à função assíncrona, não esta função **SQLCompleteAsync** .  
  
 **SQLCompleteAsync** retorna um código diferente de SQL_SUCCESS para indicar que **SQLCompleteAsync** não é chamado corretamente. O **SQLCompleteAsync** não publicará nenhum registro de diagnóstico nesse caso. Os códigos de retorno possíveis são:  
  
-   SQL_INVALID_HANDLE: o identificador indicado por *HandleType* e *identificador* não é um identificador válido.  
  
-   SQL_ERROR: *AsyncRetCodePtr* é nulo ou o processamento assíncrono não está habilitado no identificador.  
  
-   SQL_NO_DATA: no modo de notificação, uma operação assíncrona não está em andamento ou o Gerenciador de driver não notificou o aplicativo. No modo de sondagem, uma operação assíncrona não está em andamento.  
  
## <a name="comments"></a>Comentários  
 No modo de processamento assíncrono baseado em sondagem, *AsyncRetCodePtr* pode ser SQL_STILL_EXECUTING quando **SQLCompleteAsync** retorna SQL_SUCCESS. O aplicativo deve continuar sondando até que *AsyncRetCodePtr* não seja SQL_STILL_EXECUTING. No modo de processamento assíncrono baseado em notificação, o *AsyncRetCodePtr* nunca será SQL_STILL_EXECUTING.  
  
## <a name="see-also"></a>Consulte Também  
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
