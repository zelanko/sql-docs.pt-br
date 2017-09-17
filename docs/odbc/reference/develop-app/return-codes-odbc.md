---
title: "Códigos de retorno ODBC | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b997bfd1cc338f9c7a9dbb4b1b5b1ce851e71072
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="return-codes-odbc"></a>Códigos de retorno ODBC
Cada função em ODBC retorna um código, conhecido como seu *retornam o código,* que indica o êxito ou falha da função geral. Em geral, a lógica de programação se baseia em códigos de retorno.  
  
 Por exemplo, o código a seguir chama **SQLFetch** para recuperar as linhas em um conjunto de resultados. Ele verifica o código de retorno da função para determinar se o final do conjunto de resultados foi atingido (SQL_NO_DATA), se qualquer informação de aviso foi retornada (SQL_SUCCESS_WITH_INFO) ou se um erro (SQL_ERROR).  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
while ((rc=SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (rc == SQL_SUCCESS_WITH_INFO) {  
      // Call function to display warning information.  
   } else if (rc == SQL_ERROR) {  
      // Call function to display error information.  
      break;  
   }  
   // Process row.  
}  
```  
  
 O código de retorno SQL_INVALID_HANDLE sempre indica um erro de programação e nunca deve ser encontrado em tempo de execução. Todos os outros códigos de retorno fornecem informações, embora SQL_ERROR possa indicar um erro de programação.  
  
 A tabela a seguir define os códigos de retorno.  
  
|Código de retorno|Description|  
|-----------------|-----------------|  
|SQL_SUCCESS|Função foi concluída com êxito. O aplicativo chama **SQLGetDiagField** para recuperar informações adicionais do registro de cabeçalho.|  
|SQL_SUCCESS_WITH_INFO|Função foi concluída com êxito, possivelmente com um erro não fatal (aviso). O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais.|  
|SQL_ERROR|Falha na função. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais. O conteúdo de quaisquer argumentos de saída para a função é indefinido.|  
|SQL_INVALID_HANDLE|Função falhou devido a um identificador de ambiente, conexão, instrução ou descritor inválido. Isso indica um erro de programação. Nenhuma informação adicional está disponível na **SQLGetDiagRec** ou **SQLGetDiagField**. Este código é retornado somente quando o identificador é um ponteiro nulo ou tem tipo errado, como quando um identificador de instrução é passado como um argumento que exige um identificador de conexão.|  
|SQL_NO_DATA|Não há mais dados estavam disponíveis. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais. Um ou mais registros de status definidos pelo driver de classe 02xxx podem ser retornados. **Observação:** no ODBC 2.* x*, isso retornará o código foi nomeado SQL_NO_DATA_FOUND.|  
|SQL_NEED_DATA|Mais dados são necessários, como quando os dados de parâmetro são enviados em tempo de execução ou informações de conexão adicionais são necessárias. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais, se houver.|  
|SQL_STILL_EXECUTING|Uma função que foi iniciada de forma assíncrona ainda estiver em execução. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais, se houver.|
