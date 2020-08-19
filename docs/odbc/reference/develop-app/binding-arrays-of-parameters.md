---
description: Associar matrizes de parâmetros
title: Associando matrizes de parâmetros | Microsoft Docs
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
ms.openlocfilehash: 529ea49d2697ffcf7b89217746420ab5cb298890
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429478"
---
# <a name="binding-arrays-of-parameters"></a>Associar matrizes de parâmetros
Os aplicativos que usam matrizes de parâmetros associam as matrizes aos parâmetros na instrução SQL. Há dois estilos de ligação:  
  
-   Associar uma matriz a cada parâmetro. Cada estrutura de dados (matriz) contém todos os dados para um único parâmetro. Isso é chamado de *Associação de coluna,* pois associa uma coluna de valores a um único parâmetro.  
  
-   Defina uma estrutura para conter os dados de parâmetro para um conjunto inteiro de parâmetros e associe uma matriz dessas estruturas. Cada estrutura de dados contém os dados para uma única instrução SQL. Isso é chamado de *associação por linha,* pois associa uma linha de parâmetros.  
  
 Como quando o aplicativo associa variáveis únicas a parâmetros, ele chama **SQLBindParameter** para associar matrizes a parâmetros. A única diferença é que os endereços passados são endereços de matriz, não endereços de variável única. O aplicativo define o atributo SQL_ATTR_PARAM_BIND_TYPE instrução para especificar se ele está usando a associação de coluna (padrão) ou de linha. A possibilidade de usar a associação de linha ou de coluna é basicamente uma questão de preferência de aplicativo. Dependendo de como o processador acessa a memória, a ligação de linha pode ser mais rápida. No entanto, a diferença provavelmente será insignificante, exceto por números muito grandes de linhas de parâmetros.  
  
## <a name="column-wise-binding"></a>Associação de coluna  
 Ao usar a associação de coluna, um aplicativo associa uma ou duas matrizes a cada parâmetro para o qual os dados serão fornecidos. A primeira matriz contém os valores de dados, e a segunda matriz contém buffers de comprimento/indicador. Cada matriz contém tantos elementos quantos forem valores para o parâmetro.  
  
 A associação de coluna é o padrão. O aplicativo também pode ser alterado de associação de linha para associação por coluna, definindo o atributo de instrução SQL_ATTR_PARAM_BIND_TYPE. A ilustração a seguir mostra como a associação por coluna funciona.  
  
 ![Mostra como funciona a&#45;Associação inteligente de coluna](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 Por exemplo, o código a seguir associa matrizes de 10 elementos a parâmetros para as colunas partid, descrição e preço e executa uma instrução para inserir 10 linhas. Ele usa associação de coluna.  
  
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
 Ao usar a associação de linha, um aplicativo define uma estrutura para cada conjunto de parâmetros. A estrutura contém um ou dois elementos para cada parâmetro. O primeiro elemento contém o valor do parâmetro e o segundo elemento contém o buffer de comprimento/indicador. Em seguida, o aplicativo aloca uma matriz dessas estruturas, que contém tantos elementos quantos forem os valores para cada parâmetro.  
  
 O aplicativo declara o tamanho da estrutura para o driver com o atributo de instrução SQL_ATTR_PARAM_BIND_TYPE. O aplicativo associa os endereços dos parâmetros na primeira estrutura da matriz. Assim, o driver pode calcular o endereço dos dados de uma linha e coluna específica como  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 em que as linhas são numeradas de 1 até o tamanho do conjunto de parâmetros. O deslocamento, se definido, é o valor apontado pelo atributo da instrução SQL_ATTR_PARAM_BIND_OFFSET_PTR. A ilustração a seguir mostra como funciona a associação de linha. Os parâmetros podem ser colocados na estrutura em qualquer ordem, mas são mostrados em ordem sequencial para fins de clareza.  
  
 ![Mostra como a linha&#45;Associação inteligente funciona](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 O código a seguir cria uma estrutura com elementos para os valores a serem armazenados nas colunas partid, descrição e preço. Em seguida, ele aloca uma matriz de 10 elementos dessas estruturas e a associa aos parâmetros para as colunas partid, descrição e preço, usando a associação de linha. Em seguida, ele executa uma instrução para inserir 10 linhas.  
  
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
