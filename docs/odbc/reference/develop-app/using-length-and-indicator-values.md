---
title: Usando valores de comprimento e indicador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- length/indicator buffers [ODBC]
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 849792f1-cb1e-4bc2-b568-c0aff0b66199
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a0c878c9038b26aa996ed206c6b8adfe8d6c21e5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306757"
---
# <a name="using-length-and-indicator-values"></a>Usar valores de indicador e de comprimento
O buffer de comprimento/indicador é usado para passar o comprimento do byte dos dados no buffer de dados ou um indicador especial como SQL_NULL_DATA, o que indica que os dados são NULAS. Dependendo da função em que é usado, um buffer de comprimento/indicador é definido como um SQLINTEGER ou um SQLSMALLINT. Portanto, um único argumento é necessário para descrevê-lo. Se o buffer de dados for um buffer de entrada não diferido, este argumento contém o comprimento do byte dos dados em si ou um valor indicador. Muitas vezes é chamado *StrLen_or_Ind* ou um nome semelhante. Por exemplo, o código a seguir chama **SQLPutData** para passar um buffer cheio de dados; o comprimento do byte *(ValueLen)* é passado diretamente porque o buffer de dados *(ValuePtr)* é um buffer de entrada.  
  
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
  
 Se o buffer de dados for um buffer de entrada diferido, um buffer de saída não diferido ou um buffer de saída, o argumento contém o endereço do buffer de comprimento/indicador. Muitas vezes é chamado *StrLen_or_IndPtr* ou um nome semelhante. Por exemplo, o código a seguir chama **SQLGetData** para recuperar um buffer cheio de dados; o comprimento do byte é devolvido ao aplicativo no buffer de comprimento/indicador *(ValueLenOrInd),* cujo endereço é passado para **SQLGetData** porque o buffer de dados correspondente *(ValuePtr)* é um buffer de saída não diferido.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 A menos que seja especificamente proibido, um argumento de buffer de comprimento/indicador pode ser 0 (se entrada não diferida) ou um ponteiro nulo (se saída ou entrada diferida). Para buffers de entrada, isso faz com que o driver ignore o comprimento do byte dos dados. Isso retorna um erro ao passar dados de comprimento variável, mas é comum ao passar dados não nulos de comprimento fixo, porque nem um comprimento nem um valor indicador são necessários. Para buffers de saída, isso faz com que o driver não retorne o comprimento do byte dos dados ou um valor indicador. Este é um erro se os dados retornados pelo driver forem NULOS, mas é comum ao recuperar dados fixos e não anulados, porque nem um comprimento nem um valor indicador são necessários.  
  
 Como quando o endereço de um buffer de dados diferido é passado para o driver, o endereço de um buffer de comprimento/indicador diferido deve permanecer válido até que o buffer seja desvinculado.  
  
 Os seguintes comprimentos são válidos como valores de comprimento/indicador:  
  
-   *n*, onde *n* > 0.  
  
-   0.  
  
-   SQL_NTS. Uma seqüência enviada ao driver no buffer de dados correspondente é anulada por nulidade; esta é uma maneira conveniente para os programadores C passarem as cordas sem ter que calcular seu comprimento de byte. Esse valor só é legal quando o aplicativo envia dados para o motorista. Quando o driver retorna os dados para o aplicativo, ele sempre retorna o comprimento real do byte dos dados.  
  
 Os seguintes valores são válidos como valores de comprimento/indicador. SQL_NULL_DATA é armazenado no campo descritor SQL_DESC_INDICATOR_PTR; todos os outros valores são armazenados no campo descritor SQL_DESC_OCTET_LENGTH_PTR.  
  
-   Sql_null_data. Os dados são um valor de dados NULL, e o valor no buffer de dados correspondente é ignorado. Esse valor é legal apenas para dados SQL enviados ou recuperados do driver.  
  
-   SQL_DATA_AT_EXEC. O buffer de dados não contém nenhum dado. Em vez disso, os dados serão enviados com **SQLPutData** quando a declaração for executada ou quando **sQLBulkOperations** ou **SQLSetPos** forem chamados. Esse valor é legal apenas para dados SQL enviados ao motorista. Para obter mais informações, consulte [SQLBindParameter,](../../../odbc/reference/syntax/sqlbindparameter-function.md) [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
-   Resultado da macro SQL_LEN_DATA_AT_EXEC *(comprimento).* Este valor é semelhante ao SQL_DATA_AT_EXEC. Para obter mais informações, consulte [O envio de dados longos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
-   SQL_NO_TOTAL. O driver não pode determinar o número de bytes de dados longos ainda disponíveis para retornar em um buffer de saída. Esse valor é legal apenas para dados SQL recuperados do driver.  
  
-   Sql_default_param. Um procedimento é usar o valor padrão de um parâmetro de entrada em um procedimento em vez do valor no buffer de dados correspondente.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** ou **SQLSetPos** é ignorar o valor no buffer de dados. Ao atualizar uma linha de dados por uma chamada para **SQLBulkOperations** ou **SQLSetPos,** o valor da coluna não é alterado. Ao inserir uma nova linha de dados por uma chamada para **SQLBulkOperations,** o valor da coluna é definido como padrão ou, se a coluna não tiver um padrão, para NULL.
