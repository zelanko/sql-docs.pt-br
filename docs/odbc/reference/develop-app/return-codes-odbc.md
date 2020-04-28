---
title: Códigos de retorno ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- return codes [ODBC]
- diagnostic information [ODBC], return codes
ms.assetid: e893b719-4392-476f-911a-5ed6da6f7e94
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 15e434025ed1201ca61371c2fb88e70143e131a5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304307"
---
# <a name="return-codes-odbc"></a>Códigos de retorno ODBC
Cada função no ODBC retorna um código, conhecido como seu *código de retorno,* que indica o êxito geral ou a falha da função. Em geral, a lógica de programação se baseia em códigos de retorno.  
  
 Por exemplo, o código a seguir chama **SQLFetch** para recuperar as linhas em um conjunto de resultados. Ele verifica o código de retorno da função para determinar se o final do conjunto de resultados foi atingido (SQL_NO_DATA), se alguma informação de aviso foi retornada (SQL_SUCCESS_WITH_INFO) ou se ocorreu um erro (SQL_ERROR).  
  
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
  
|Código de retorno|Descrição|  
|-----------------|-----------------|  
|SQL_SUCCESS|A função foi concluída com êxito. O aplicativo chama **SQLGetDiagField** para recuperar informações adicionais do registro de cabeçalho.|  
|SQL_SUCCESS_WITH_INFO|A função foi concluída com êxito, possivelmente com um erro não fatal (aviso). O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais.|  
|SQL_ERROR|Falha na função. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais. O conteúdo de qualquer argumento de saída para a função é indefinido.|  
|SQL_INVALID_HANDLE|A função falhou devido a um ambiente, uma conexão, uma instrução ou um identificador de descritor inválido. Isso indica um erro de programação. Não há informações adicionais disponíveis em **SQLGetDiagRec** ou **SQLGetDiagField**. Esse código é retornado somente quando o identificador é um ponteiro nulo ou é do tipo errado, como quando um identificador de instrução é passado para um argumento que requer um identificador de conexão.|  
|SQL_NO_DATA|Não há mais dados disponíveis. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais. Um ou mais registros de status definidos pelo driver na classe 02xxx podem ser retornados. **Observação:**  No ODBC 2. *x*, esse código de retorno foi nomeado SQL_NO_DATA_FOUND.|  
|SQL_NEED_DATA|Mais dados são necessários, como quando os dados de parâmetro são enviados em tempo de execução ou informações de conexão adicionais são necessárias. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais, se houver.|  
|SQL_STILL_EXECUTING|Uma função que foi iniciada assincronamente ainda está em execução. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais, se houver.|
