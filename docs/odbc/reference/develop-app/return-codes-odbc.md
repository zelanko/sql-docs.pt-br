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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304307"
---
# <a name="return-codes-odbc"></a>Códigos de retorno ODBC
Cada função no ODBC retorna um código, conhecido como seu *código de retorno,* que indica o sucesso geral ou falha da função. Em geral, a lógica de programação se baseia em códigos de retorno.  
  
 Por exemplo, o código a seguir chama **SQLFetch** para recuperar as linhas em um conjunto de resultados. Ele verifica o código de devolução da função para determinar se o fim do conjunto de resultados foi atingido (SQL_NO_DATA), se alguma informação de aviso foi devolvida (SQL_SUCCESS_WITH_INFO) ou se ocorreu um erro (SQL_ERROR).  
  
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
|SQL_SUCCESS|Função concluída com sucesso. O aplicativo chama **o SQLGetDiagField** para recuperar informações adicionais do registro de cabeçalho.|  
|Sql_success_with_info|Função concluída com sucesso, possivelmente com um erro não fatal (aviso). O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais.|  
|SQL_ERROR|Falha na função. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais. O conteúdo de quaisquer argumentos de saída para a função é indefinido.|  
|SQL_INVALID_HANDLE|A função falhou devido a um ambiente inválido, conexão, declaração ou alça descritor. Isso indica um erro de programação. Nenhuma informação adicional está disponível no **SQLGetDiagRec** ou **no SQLGetDiagField**. Esse código é retornado somente quando o cabo é um ponteiro nulo ou é o tipo errado, como quando uma alça de declaração é passada para um argumento que requer uma alça de conexão.|  
|SQL_NO_DATA|Não havia mais dados disponíveis. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais. Um ou mais registros de status definidos pelo driver na classe 02xxx podem ser devolvidos. **Nota:**  Em ODBC 2. *x*, este código de retorno foi nomeado SQL_NO_DATA_FOUND.|  
|Sql_need_data|Mais dados são necessários, como quando os dados de parâmetros são enviados no momento da execução ou informações adicionais de conexão são necessárias. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais, se houver.|  
|Sql_still_executing|Uma função que foi iniciada assíncronamente ainda está sendo executada. O aplicativo chama **SQLGetDiagRec** ou **SQLGetDiagField** para recuperar informações adicionais, se houver.|
