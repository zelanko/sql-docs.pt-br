---
title: "Matrizes de parâmetros de associação | Microsoft Docs"
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
- binding parameter arrays [ODBC]
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 037afe23-052d-4f3a-8aa7-45302b199ad0
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 049414080c3594a873f17c3e8eed8fdc876fedf0
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="binding-arrays-of-parameters"></a>Matrizes de parâmetros de associação
Aplicativos que usam matrizes de parâmetros de associar as matrizes de parâmetros na instrução SQL. Há dois estilos de associação:  
  
-   Associe uma matriz para cada parâmetro. Cada estrutura de dados (matriz) contém todos os dados para um único parâmetro. Isso é chamado de *a associação* porque ele associa uma coluna de valores para um único parâmetro.  
  
-   Defina uma estrutura para armazenar os dados de parâmetro para um conjunto de parâmetros e associar uma matriz dessas estruturas. Cada estrutura de dados contém os dados para uma única instrução SQL. Isso é chamado de *a associação* porque ele associa uma linha de parâmetros.  
  
 Como quando o aplicativo associa único variáveis para parâmetros, ele chama **SQLBindParameter** para associar as matrizes de parâmetros. A única diferença é que os endereços passados são endereços de matriz, endereços de variável não único. O aplicativo define o atributo de instrução SQL_ATTR_PARAM_BIND_TYPE para especificar se está usando a (o padrão) ou a associação. Se deseja usar a associação de coluna ou linha de associação é principalmente uma questão de preferência de aplicativo. Dependendo de como o processador de acessa a memória, a associação pode ser mais rápida. No entanto, a diferença é provavelmente insignificante, exceto um grande número de linhas de parâmetros.  
  
## <a name="column-wise-binding"></a>A associação  
 Ao usar a associação, um aplicativo associar uma ou duas matrizes para cada parâmetro para o qual os dados são a ser fornecido. A primeira matriz contém os valores de dados, e a segunda matriz contém buffers de comprimento/indicador. Cada matriz contém elementos existem valores para o parâmetro.  
  
 A associação é o padrão. O aplicativo também pode mudar da associação para a associação, definindo o atributo de instrução SQL_ATTR_PARAM_BIND_TYPE. A ilustração a seguir mostra como a associação funciona.  
  
 ![Mostra como coluna &#45; ligação aconselhável funciona](../../../odbc/reference/develop-app/media/pr31.gif "pr31")  
  
 Por exemplo, o código a seguir associa o elemento 10 matrizes aos parâmetros para as colunas PartID, a descrição e o preço e executa uma instrução para inserir 10 linhas. Ele usa a associação.  
  
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
  
memset(DescLenOrIndArray, 0, sizeof(DescLenOrIndArray);  
memset(PartIDIndArray, 0, sizeof(PartIDIndArray);  
memset(PriceIndArray, 0, sizeof(PriceIndArray);  
  
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
  
## <a name="row-wise-binding"></a>A associação  
 Ao usar a associação, um aplicativo define uma estrutura para cada conjunto de parâmetros. A estrutura contém um ou dois elementos para cada parâmetro. O primeiro elemento contém o valor do parâmetro e o segundo elemento contém o buffer de comprimento/indicador. O aplicativo, em seguida, aloca uma matriz dessas estruturas, que contém elementos existem valores para cada parâmetro.  
  
 O aplicativo declara o tamanho da estrutura para o driver com o atributo de instrução SQL_ATTR_PARAM_BIND_TYPE. O aplicativo associa os endereços dos parâmetros na primeira estrutura da matriz. Portanto, o driver pode calcular o endereço dos dados para uma determinada linha e coluna como  
  
```  
Address = Bound Address + ((Row Number - 1) * Structure Size) + Offset  
```  
  
 em que as linhas são numeradas de 1 para o tamanho do conjunto de parâmetros. O deslocamento, se definida, é o valor apontado pelo atributo de instrução SQL_ATTR_PARAM_BIND_OFFSET_PTR. A ilustração a seguir mostra como a associação funciona. Os parâmetros podem ser colocados na estrutura em qualquer ordem, mas são mostrados em ordem sequencial para maior clareza.  
  
 ![Mostra como a linha &#45; ligação aconselhável funciona](../../../odbc/reference/develop-app/media/pr32.gif "pr32")  
  
 O código a seguir cria uma estrutura com elementos para os valores a serem armazenados nas colunas PartID, descrição e preço. Em seguida, ele aloca uma matriz de elementos de 10 dessas estruturas e o associa a parâmetros para as colunas PartID, descrição e preço, usando a associação. Em seguida, ele executa uma instrução para inserir 10 linhas.  
  
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

