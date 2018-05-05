---
title: Função SQLCompleteAsync | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b9c0780cd9d444cf872ae6781dae0a60e80e951
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcompleteasync-function"></a>Função SQLCompleteAsync
**Conformidade**  
 Versão introduzidas: ODBC 3.8  
  
 Conformidade com padrões: nenhum  
  
 **Resumo**  
 **SQLCompleteAsync** pode ser usado para determinar quando uma função assíncrona é concluída usando qualquer processamento ou sondagem-baseada em notificação. Para obter mais informações sobre as operações assíncronas, consulte [execução assíncrona](../../../odbc/reference/develop-app/asynchronous-execution.md).  
  
 **SQLCompleteAsync** é implementada somente no Gerenciador de Driver ODBC.  
  
 No modo de processamento assíncrono de notificação com base em **SQLCompleteAsync** deve ser chamado depois que o Gerenciador de Driver gera o objeto de evento usado para notificação. **SQLCompleteAsync** conclusão assíncrona processamento e a função assíncrona irá gerar um código de retorno.  
  
 No modo de processamento assíncrono de pesquisa com base em **SQLCompleteAsync** é uma alternativa ao chamar a função assíncrona original, sem a necessidade de especificar os argumentos na chamada de função assíncrona original. **SQLCompleteAsync** pode ser usado independentemente se a biblioteca de cursores ODBC está habilitada.  
  
## <a name="syntax"></a>Sintaxe  
  
```vb  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] O tipo do identificador no qual a conclusão assíncrona de processamento. Os valores válidos são SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
 *Handle*  
 [Entrada] O identificador no qual a conclusão assíncrona de processamento. Se *tratar* não é um identificador válido do tipo especificado pelo *HandleType*, **SQLCompleteAsync** retorne SQL_INVALID_HANDLE.  
  
 Se *tratar* não é um identificador válido do tipo especificado pelo *HandleType*, **SQLCompleteAsync** retorne SQL_INVALID_HANDLE.  
  
 *AsyncRetCodePtr*  
 [Saída] Ponteiro para um buffer que contém o código de retorno da API assíncrona. Se *AsyncRetCodePtr* for NULL, **SQLCompleteAsync** retornará SQL_ERROR.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 Se **SQLCompleteAsync** retorna SQL_SUCCESS, um aplicativo deve obter o código de retorno da função assíncrona do buffer apontado pelo *AsyncRetCodePtr*. O SQLSTATE associado, se houver, pode ser obtido chamando **SQLGetDiagRec** com um *HandleType* de SQL_HANDLE_STMT e um identificador de instrução ou um *HandleType* de SQL _ HANDLE_DBC e um identificador de conexão. Os registros de diagnósticos estão associados com a função assíncrona, não desta **SQLCompleteAsync** função.  
  
 **SQLCompleteAsync** retorna um código diferente de SQL_SUCCESS para indicar que **SQLCompleteAsync** não foi chamado corretamente. **SQLCompleteAsync** não publicará qualquer registro de diagnóstico nesse caso. Códigos de retorno possíveis são:  
  
-   SQL_INVALID_HANDLE: O identificador indicado por *HandleType* e *tratar* não é um identificador válido.  
  
-   SQL_ERROR: *AsyncRetCodePtr* é nulo ou o processamento assíncrono não está habilitado no identificador.  
  
-   SQL_NO_DATA: No modo de notificação, uma operação assíncrona não está em andamento ou o Gerenciador de Driver não notificou o aplicativo. No modo de sondagem, uma operação assíncrona não está em andamento.  
  
## <a name="comments"></a>Comentários  
 No modo de processamento assíncrono de pesquisa com base em *AsyncRetCodePtr* pode ser SQL_STILL_EXECUTING quando **SQLCompleteAsync** retorna SQL_SUCCESS. Aplicativo deve manter sondagem até *AsyncRetCodePtr* não é SQL_STILL_EXECUTING. No modo de processamento assíncrono de notificação com base em *AsyncRetCodePtr* nunca serão SQL_STILL_EXECUTING.  
  
## <a name="see-also"></a>Consulte também  
 [Execução assíncrona (método de sondagem)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
