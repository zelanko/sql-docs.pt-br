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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3a0b54617d55033addabc729adbd078680022fc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67902466"
---
# <a name="using-length-and-indicator-values"></a>Usar valores de indicador e de comprimento
O buffer de comprimento/indicador é usado para passar o comprimento de bytes dos dados no buffer de dados ou um indicador especial, como SQL_NULL_DATA, o que indica que os dados são nulos. Dependendo da função na qual ela é usada, um buffer de comprimento/indicador é definido como um sqlinteiro ou um SQLSMALLINT. Portanto, um único argumento é necessário para descrevê-lo. Se o buffer de dados for um buffer de entrada nondeferred, esse argumento conterá o comprimento de bytes dos próprios dados ou um valor de indicador. Geralmente, ele é denominado *StrLen_or_Ind* ou um nome semelhante. Por exemplo, o código a seguir chama **SQLPutData** para passar um buffer cheio de dados; o comprimento do byte (*ValueLen*) é passado diretamente porque o buffer de dados (*ValuePtr*) é um buffer de entrada.  
  
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
  
 Se o buffer de dados for um buffer de entrada adiado, um buffer de saída nondeferred ou um buffer de saída, o argumento conterá o endereço do buffer de comprimento/indicador. Geralmente, ele é denominado *StrLen_or_IndPtr* ou um nome semelhante. Por exemplo, o código a seguir chama **SQLGetData** para recuperar um buffer cheio de dados; o comprimento do byte é retornado para o aplicativo no buffer de comprimento/indicador (*ValueLenOrInd*), cujo endereço é passado para **SQLGetData** porque o buffer de dados correspondente (*ValuePtr*) é um buffer de saída nondeferred.  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLGetData(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 A menos que seja especificamente proibido, um argumento de buffer de comprimento/indicador pode ser 0 (se a entrada nondeferred) ou um ponteiro nulo (se a saída ou a entrada adiada). Para buffers de entrada, isso faz com que o driver ignore o comprimento de bytes dos dados. Isso retorna um erro ao passar dados de comprimento variável, mas é comum ao passar dados não nulos de comprimento fixo, pois nenhum valor de comprimento nem de indicador é necessário. Para buffers de saída, isso faz com que o driver não retorne o comprimento de bytes dos dados ou um valor de indicador. Isso é um erro se os dados retornados pelo driver forem nulos, mas forem comuns ao recuperar dados de comprimento fixo e não anuláveis, pois nenhum valor de comprimento nem de indicador é necessário.  
  
 Como quando o endereço de um buffer de dados adiado é passado para o driver, o endereço de um buffer de comprimento/indicador adiado deve permanecer válido até que o buffer seja desassociado.  
  
 Os seguintes comprimentos são válidos como valores de comprimento/indicador:  
  
-   *n*, onde *n* > 0.  
  
-   0.  
  
-   SQL_NTS. Uma cadeia de caracteres enviada ao driver no buffer de dados correspondente é terminada em nulo; Essa é uma maneira conveniente para que os programadores de C passem cadeias de caracteres sem precisar calcular o comprimento do byte. Esse valor é válido somente quando o aplicativo envia dados para o driver. Quando o driver retorna dados para o aplicativo, ele sempre retorna o comprimento de bytes real dos dados.  
  
 Os valores a seguir são válidos como valores de comprimento/indicador. SQL_NULL_DATA é armazenado no campo descritor de SQL_DESC_INDICATOR_PTR; todos os outros valores são armazenados no campo descritor de SQL_DESC_OCTET_LENGTH_PTR.  
  
-   SQL_NULL_DATA. Os dados são um valor de dados nulo e o valor no buffer de dados correspondente é ignorado. Esse valor é válido somente para dados do SQL enviados ou recuperados do driver.  
  
-   SQL_DATA_AT_EXEC. O buffer de dados não contém nenhum dado. Em vez disso, os dados serão enviados com **SQLPutData** quando a instrução for executada ou quando **SQLBulkOperations** ou **SQLSetPos** for chamado. Esse valor é válido somente para dados SQL enviados ao driver. Para obter mais informações, consulte [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md), [SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)e [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
-   Resultado da macro SQL_LEN_DATA_AT_EXEC (*comprimento*). Esse valor é semelhante a SQL_DATA_AT_EXEC. Para obter mais informações, consulte [enviando dados longos](../../../odbc/reference/develop-app/sending-long-data.md).  
  
-   SQL_NO_TOTAL. O driver não pode determinar o número de bytes de dados longos que ainda estão disponíveis para retornar em um buffer de saída. Esse valor é válido somente para dados SQL recuperados do driver.  
  
-   SQL_DEFAULT_PARAM. Um procedimento é usar o valor padrão de um parâmetro de entrada em um procedimento em vez do valor no buffer de dados correspondente.  
  
-   SQL_COLUMN_IGNORE. **SQLBulkOperations** ou **SQLSetPos** é ignorar o valor no buffer de dados. Ao atualizar uma linha de dados por uma chamada para **SQLBulkOperations** ou **SQLSetPos,** o valor da coluna não é alterado. Ao inserir uma nova linha de dados por uma chamada para **SQLBulkOperations**, o valor da coluna é definido como seu padrão ou, se a coluna não tiver um padrão, para NULL.
