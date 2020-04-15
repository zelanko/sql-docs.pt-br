---
title: Matrizes de vinculação de parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binding parameter arrays [ODBC]
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 037afe23-052d-4f3a-8aa7-45302b199ad0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 73cfcde89e89edb87a4955cf0854c66a01d81e6f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283396"
---
# <a name="binding-arrays-of-parameters"></a>Associar matrizes de parâmetros
Aplicações que usam matrizes de parâmetros ligam os arrays aos parâmetros da declaração SQL. Existem dois estilos de ligação:  
  
-   Ligue uma matriz a cada parâmetro. Cada estrutura de dados (array) contém todos os dados para um único parâmetro. Isso é chamado *de vinculação em termos de coluna* porque vincula uma coluna de valores para um único parâmetro.  
  
-   Defina uma estrutura para reter os dados dos parâmetros para um conjunto inteiro de parâmetros e vincular uma matriz dessas estruturas. Cada estrutura de dados contém os dados de uma única declaração SQL. Isso é chamado *de vinculação em termos de linha* porque liga uma linha de parâmetros.  
  
 Como quando o aplicativo vincula variáveis únicas a parâmetros, ele chama **SQLBindParameter** para vincular matrizes a parâmetros. A única diferença é que os endereços aprovados são endereços de matriz, não endereços de variável única. O aplicativo define o atributo de declaração SQL_ATTR_PARAM_BIND_TYPE para especificar se ele está usando a vinculação em termos de coluna (o padrão) ou em termos de linha. Se usar a vinculação em termos de coluna ou de linha é em grande parte uma questão de preferência de aplicativo. Dependendo de como o processador acessa a memória, a vinculação em termos de linha pode ser mais rápida. No entanto, é provável que a diferença seja insignificante, exceto por um número muito grande de linhas de parâmetros.  
  
## <a name="column-wise-binding"></a>Associação de coluna  
 Ao usar a vinculação em termos de coluna, um aplicativo vincula uma ou duas matrizes a cada parâmetro para o qual os dados devem ser fornecidos. O primeiro array contém os valores de dados, e o segundo array mantém buffers de comprimento/indicador. Cada matriz contém tantos elementos quanto há valores para o parâmetro.  
  
 A vinculação em termos de coluna é o padrão. O aplicativo também pode mudar de vinculação em termos de linha para vinculação em termos de coluna, definindo o atributo de declaração SQL_ATTR_PARAM_BIND_TYPE. A ilustração a seguir mostra como funciona a vinculação em termos de coluna.  
  
 ![Mostra como a coluna&#45;a vinculação sábia funciona](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 Por exemplo, o código a seguir liga as matrizes de 10 elementos a parâmetros para as colunas PartID, Description e Price e executa uma instrução para inserir 10 linhas. Ele usa a vinculação em termos de coluna.  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  Price) "  
                                                "VALUES (?, ?, ?)";  
SQLUINTEGER    PartIDArray[ARRAY_SIZE];  
SQLCHAR        DescArray[ARRAY_SIZE][DESC_LEN];  
SQLREAL        PriceArray[ARRAY_SIZE];  
SQLINTEGER     PartIDIndArray[ARRAY_SIZE], DescLenOrIndArray[ARRAY_SIZE],  
               PriceIndArray[ARRAY_SIZE];  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
memset(DescLenOrIndArray, 0, sizeof(DescLenOrIndArray));  
memset(PartIDIndArray, 0, sizeof(PartIDIndArray));  
memset(PriceIndArray, 0, sizeof(PriceIndArray));  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, SQL_PARAM_BIND_BY_COLUMN, 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in column-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  PartIDArray, 0, PartIDIndArray);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  DescArray, DESC_LEN, DescLenOrIndArray);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  PriceArray, 0, PriceIndArray);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartIDArray[i], DescArray[i], &PriceArray[i]);  
   PartIDIndArray[i] = 0;  
   DescLenOrIndArray[i] = SQL_NTS;  
   PriceIndArray[i] = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
}  
```  
  
## <a name="row-wise-binding"></a>Associação de linha  
 Ao usar a vinculação em termos de linha, um aplicativo define uma estrutura para cada conjunto de parâmetros. A estrutura contém um ou dois elementos para cada parâmetro. O primeiro elemento contém o valor do parâmetro, e o segundo elemento contém o buffer de comprimento/indicador. A aplicação então aloca uma matriz dessas estruturas, que contém tantos elementos quanto há valores para cada parâmetro.  
  
 O aplicativo declara o tamanho da estrutura ao motorista com o atributo de declaração SQL_ATTR_PARAM_BIND_TYPE. O aplicativo vincula os endereços dos parâmetros na primeira estrutura da matriz. Assim, o motorista pode calcular o endereço dos dados para uma determinada linha e coluna como  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 onde as linhas são numeradas de 1 para o tamanho do conjunto de parâmetros. A compensação, se definida, é o valor apontado pelo atributo de declaração SQL_ATTR_PARAM_BIND_OFFSET_PTR. A ilustração a seguir mostra como funciona a vinculação em termos de linha. Os parâmetros podem ser colocados na estrutura em qualquer ordem, mas são mostrados em ordem seqüencial para clareza.  
  
 ![Mostra como a linha&#45;a ligação sábia funciona](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 O código a seguir cria uma estrutura com elementos para os valores a armazenar nas colunas PartID, Description e Price. Em seguida, ele aloca uma matriz de 10 elementos dessas estruturas e vincula-as a parâmetros para as colunas PartID, Description e Price, usando a vinculação em termos de linha. Em seguida, executa uma instrução para inserir 10 linhas.  
  
```  
#define DESC_LEN 51  
#define ARRAY_SIZE 10  
  
typedef tagPartStruct {  
   SQLREAL       Price;  
   SQLUINTEGER   PartID;  
   SQLCHAR       Desc[DESC_LEN];  
   SQLINTEGER    PriceInd;  
   SQLINTEGER    PartIDInd;  
   SQLINTEGER    DescLenOrInd;  
} PartStruct;  
  
PartStruct PartArray[ARRAY_SIZE];  
SQLCHAR *      Statement = "INSERT INTO Parts (PartID, Description,  
                Price) "  
               "VALUES (?, ?, ?)";  
SQLUSMALLINT   i, ParamStatusArray[ARRAY_SIZE];  
SQLULEN ParamsProcessed;  
  
// Set the SQL_ATTR_PARAM_BIND_TYPE statement attribute to use  
// column-wise binding.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_BIND_TYPE, sizeof(PartStruct), 0);  
  
// Specify the number of elements in each parameter array.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMSET_SIZE, ARRAY_SIZE, 0);  
  
// Specify an array in which to return the status of each set of  
// parameters.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAM_STATUS_PTR, ParamStatusArray, 0);  
  
// Specify an SQLUINTEGER value in which to return the number of sets of  
// parameters processed.  
SQLSetStmtAttr(hstmt, SQL_ATTR_PARAMS_PROCESSED_PTR, &ParamsProcessed, 0);  
  
// Bind the parameters in row-wise fashion.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &PartArray[0].PartID, 0, &PartArray[0].PartIDInd);  
SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, DESC_LEN - 1, 0,  
                  PartArray[0].Desc, DESC_LEN, &PartArray[0].DescLenOrInd);  
SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_FLOAT, SQL_REAL, 7, 0,  
                  &PartArray[0].Price, 0, &PartArray[0].PriceInd);  
  
// Set part ID, description, and price.  
for (i = 0; i < ARRAY_SIZE; i++) {  
   GetNewValues(&PartArray[i].PartID, PartArray[i].Desc, &PartArray[i].Price);  
   PartArray[0].PartIDInd = 0;  
   PartArray[0].DescLenOrInd = SQL_NTS;  
   PartArray[0].PriceInd = 0;  
}  
  
// Execute the statement.  
SQLExecDirect(hstmt, Statement, SQL_NTS);  
  
// Check to see which sets of parameters were processed successfully.  
for (i = 0; i < ParamsProcessed; i++) {  
   printf("Parameter Set  Status\n");  
   printf("-------------  -------------\n");  
   switch (ParamStatusArray[i]) {  
      case SQL_PARAM_SUCCESS:  
      case SQL_PARAM_SUCCESS_WITH_INFO:  
         printf("%13d  Success\n", i);  
         break;  
  
      case SQL_PARAM_ERROR:  
         printf("%13d  Error\n", i);  
         break;  
  
      case SQL_PARAM_UNUSED:  
         printf("%13d  Not processed\n", i);  
         break;  
  
      case SQL_PARAM_DIAG_UNAVAILABLE:  
         printf("%13d  Unknown\n", i);  
         break;  
  
   }  
```
