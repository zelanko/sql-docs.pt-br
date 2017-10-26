---
title: Usando valores de indicador de comprimento e | Microsoft Docs
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
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f615aa92da79c391e84539fdf5cf402d523ab690
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-length-and-indicator-values"></a>Usando valores de indicador de comprimento e
O buffer de comprimento/indicador é usado para passar o comprimento de bytes dos dados no buffer de dados ou um indicador especial, como SQL_NULL_DATA, que indica que os dados são NULL. Dependendo da função na qual ele é usado, um buffer de comprimento/indicador é definido para ser um sqlinteger que contém ou um SQLSMALLINT. Portanto, um único argumento é necessário para descrevê-lo. Se o buffer de dados é um buffer de entrada nondeferred, esse argumento contém o comprimento em bytes de dados em si ou um valor de indicador. Ele é geralmente chamado de *StrLen_or_Ind* ou um nome semelhante. Por exemplo, o código a seguir chama **SQLPutData** para passar um buffer completo dos dados; o comprimento de bytes (*ValueLen*) é passada diretamente porque o buffer de dados (*ValuePtr*) é um buffer de entrada.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLen;  
  
// Call local function to place data in ValuePtr. In ValueLen, return the  
// number of bytes of data placed in ValuePtr. If there is not enough  
// data, this will be less than 50.  
FillBuffer(ValuePtr, sizeof(ValuePtr), &ValueLen);  
  
// Call SQLPutData to send the data to the driver.  
SQLPutData(hstmt, ValuePtr, ValueLen);  
```  
  
 Se o buffer de dados é um buffer de entrada adiado, um buffer de saída nondeferred ou um buffer de saída, o argumento contém o endereço do buffer de comprimento/indicador. Ele é geralmente chamado de *StrLen_or_IndPtr* ou um nome semelhante. Por exemplo, o código a seguir chama **SQLGetData** para recuperar um buffer de dados; o comprimento em bytes é retornado para o aplicativo no buffer de comprimento/indicador (*ValueLenOrInd*), cujo endereço é passado para **SQLGetData** porque o buffer de dados correspondente (*ValuePtr*) é um buffer de saída nondeferred.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 A menos que especificamente é proibido, um argumento de buffer de comprimento/indicador pode ser 0 (se a entrada nondeferred) ou um ponteiro nulo (se adiada de entrada ou saída). Para os buffers de entrada, isso faz com que o driver ignorar o comprimento de bytes dos dados. Isso retornará um erro ao transmitir dados de comprimento variável, mas é comum quando passar dados não nulo ou de comprimento fixo, porque é necessário um comprimento nem um valor de indicador. Para os buffers de saída, isso faz com que o driver não retornar o comprimento de bytes de dados ou um valor de indicador. Este é um erro se os dados retornados pelo driver for NULL, mas são comuns ao recuperar dados de comprimento fixo, não permite valor nulo, porque é necessário um comprimento nem um valor de indicador.  
  
 Como quando o endereço de um buffer de dados adiada é passado para o driver, o endereço de um buffer de comprimento/indicador adiada deve permanecer válido até que o buffer é desassociado.  
  
 Os seguintes tamanhos são válidos como valores de comprimento/indicador:  
  
-   *n*, onde * n * > 0.  
  
-   0.  
  
-   SQL_NTS. Uma cadeia de caracteres enviada para o driver no buffer de dados correspondente é terminada em nulo; Essa é uma maneira conveniente para programadores de C passar cadeias de caracteres sem a necessidade de calcular o comprimento em bytes. Esse valor é válido somente quando o aplicativo envia dados para o driver. Quando o driver retorna dados para o aplicativo, ele sempre retorna o tamanho real de bytes dos dados.  
  
 Os seguintes valores são válidos como valores de comprimento/indicador. SQL_NULL_DATA é armazenado no campo de descritor SQL_DESC_INDICATOR_PTR; todos os outros valores são armazenados no campo de descritor SQL_DESC_OCTET_LENGTH_PTR.  
  
-   SQL_NULL_DATA. Os dados são um valor de dados NULL, e o valor no buffer de dados correspondente é ignorado. Esse valor é válido somente para dados SQL enviados para ou recuperados do driver.  
  
-   SQL_DATA_AT_EXEC. O buffer de dados não contém nenhum dado. Em vez disso, os dados serão enviados com **SQLPutData** quando a instrução é executada ou quando **SQLBulkOperations** ou **SQLSetPos** é chamado. Esse valor é válido somente para dados SQL enviados para o driver. Para obter mais informações, consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
-   Resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro. Esse valor é semelhante a SQL_DATA_AT_EXEC. Para obter mais informações, consulte [enviar dados longos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
-   SQL_NO_TOTAL. O driver não pode determinar o número de bytes de dados longos ainda está disponíveis para retornar em um buffer de saída. Esse valor é válido somente para dados SQL recuperados do driver.  
  
-   SQL_DEFAULT_PARAM. Um procedimento é usar o valor padrão de um parâmetro de entrada em um procedimento em vez do valor no buffer de dados correspondente.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** ou **SQLSetPos** deve ignorar o valor no buffer de dados. Ao atualizar uma linha de dados por uma chamada para **SQLBulkOperations** ou **SQLSetPos,** o valor da coluna não é alterado. Ao inserir uma nova linha de dados por uma chamada para **SQLBulkOperations**, o valor da coluna é definido como padrão ou, se a coluna não tiver um padrão, como NULL.

