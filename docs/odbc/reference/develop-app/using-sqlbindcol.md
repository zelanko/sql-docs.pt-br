---
title: Usando SQLBindCol | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
- SQLBindCol function [ODBC], using
ms.assetid: 17277ab3-33ad-44d3-a81c-a26b5e338512
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2e3329d1f5990edae9805538d6e9c5e4c563b028
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="using-sqlbindcol"></a>Usando SQLBindCol
O aplicativo associa colunas chamando **SQLBindCol**. Essa função associa uma coluna por vez. Com ele, o aplicativo especifica o seguinte:  
  
-   O número da coluna. A coluna 0 é a coluna de indicador; não é possível incluir essa coluna em alguns conjuntos de resultados. Todas as outras colunas são numeradas começando com o número 1. Erro ao vincular uma coluna de números maiores que o número de colunas no conjunto de resultados; Esse erro não pode ser detectado até que o conjunto de resultados tiver sido criado, para que ele é retornado por **SQLFetch**, não **SQLBindCol**.  
  
-   O comprimento C de bytes, o endereço e o tipo de dados da variável associada à coluna. É um erro para especificar um tipo de dados C para o qual o tipo de dados SQL da coluna não pode ser convertido; Esse erro talvez não seja detectado até que o conjunto de resultados tiver sido criado, para que ele é retornado por **SQLFetch**, não **SQLBindCol**. Para obter uma lista de conversões com suporte, consulte [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no Apêndice d: os tipos de dados. Para obter informações sobre o comprimento em bytes, consulte [comprimento do Buffer de dados](../../../odbc/reference/develop-app/data-buffer-length.md).  
  
-   O endereço de um buffer de comprimento/indicador. O buffer de comprimento/indicador é opcional. Ele é usado para retornar o comprimento de bytes de binário ou de dados de caractere ou retorno SQL_NULL_DATA se os dados são NULL. Para obter mais informações, consulte [usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Quando **SQLBindCol** é chamado, o driver associa essas informações com a instrução. Quando cada linha de dados for encontrada, ele usa as informações para colocar os dados para cada coluna nas variáveis associadas de aplicativo.  
  
 Por exemplo, o código a seguir associa variáveis para as colunas de vendedor e CustID. Dados para as colunas serão retornados no *vendedor* e *CustID*. Porque *vendedor* é um buffer de caractere, o aplicativo especifica o comprimento de byte (11) para que o driver pode determinar se deseja truncar os dados. O comprimento em bytes de retornado título ou, se for NULL, será retornado no *SalesPersonLenOrInd*.  
  
 Porque *CustID* é uma variável de inteiro e corrigiu comprimento, não há necessidade de especificar seu comprimento de byte; o driver pressupõe que ele seja **sizeof (**SQLUINTEGER**)**. O comprimento de bytes do cliente retornado a ID de dados, ou se for NULL, será retornado no *CustIDInd*. Observe que o aplicativo estiver interessado somente se o salário for NULL, porque o comprimento de bytes é sempre **sizeof (**SQLUINTEGER**)**.  
  
```  
SQLCHAR       SalesPerson[11];  
SQLUINTEGER   CustID;  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLRETURN     rc;  
SQLHSTMT      hstmt;  
  
// Bind SalesPerson to the SalesPerson column and CustID to the   
// CustID column.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, SalesPerson, sizeof(SalesPerson),  
            &SalesPersonLenOrInd);  
SQLBindCol(hstmt, 2, SQL_C_ULONG, &CustID, 0, &CustIDInd);  
  
// Execute a statement to get the sales person/customer of all orders.  
SQLExecDirect(hstmt, "SELECT SalesPerson, CustID FROM Orders ORDER BY SalesPerson",  
               SQL_NTS);  
  
// Fetch and print the data. Print "NULL" if the data is NULL. Code to   
// check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   if (SalesPersonLenOrInd == SQL_NULL_DATA)   
            printf("NULL                     ");  
   else   
            printf("%10s   ", SalesPerson);  
   if (CustIDInd == SQL_NULL_DATA)   
         printf("NULL\n");  
   else   
            printf("%d\n", CustID);  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```  
  
 O código a seguir executa um **selecione** instrução inserida pelo usuário e imprime a cada linha de dados no conjunto de resultados. Como o aplicativo não pode prever a forma do resultado definido criado pelo **selecione** instrução, ele não é possível associar variáveis embutido ao conjunto, como no exemplo anterior de resultados. Em vez disso, o aplicativo aloca um buffer de comprimento/indicador e um buffer que contém os dados para cada coluna na linha. Para cada coluna, ela calcula o deslocamento inicial da memória para a coluna e ajusta esse deslocamento para que os buffers de dados e comprimento/indicador para a coluna Iniciar em limites de alinhamento. Em seguida, vincular a memória que inicia no deslocamento para a coluna. Do ponto de vista do driver, o endereço da memória é possível distinguir do endereço de uma variável de associado no exemplo anterior. Para obter mais informações sobre o alinhamento, consulte [alinhamento](../../../odbc/reference/develop-app/alignment.md).  
  
```  
// This application allocates a buffer at run time. For each column, this   
// buffer contains memory for the column's data and length/indicator.   
// For example:  
//      column 1         column 2      column 3      column 4  
// <------------><---------------><-----><------------>  
//      db1   li1   db2   li2   db3   li3   db4   li4  
//      |      |      |      |      |      |      |         |  
//      _____V_____V________V_______V___V___V______V_____V_  
// |__________|__|_____________|__|___|__|__________|__|  
//  
// dbn = data buffer for column n  
// lin = length/indicator buffer for column n  
  
// Define a macro to increase the size of a buffer so that it is a   
// multiple of the alignment size. Thus, if a buffer starts on an   
// alignment boundary, it will end just before the next alignment   
// boundary. In this example, an alignment size of 4 is used because   
// this is the size of the largest data type used in the application's   
// buffer--the size of an SDWORD and of the largest default C data type   
// are both 4. If a larger data type (such as _int64) was used, it would   
// be necessary to align for that size.  
#define ALIGNSIZE 4  
#define ALIGNBUF(Length) Length % ALIGNSIZE ? \  
                  Length + ALIGNSIZE - (Length % ALIGNSIZE) : Length  
  
SQLCHAR        SelectStmt[100];  
SQLSMALLINT    NumCols, *CTypeArray, i;  
SQLINTEGER *   ColLenArray, *OffsetArray, SQLType, *DataPtr;  
SQLRETURN      rc;   
SQLHSTMT       hstmt;  
  
// Get a SELECT statement from the user and execute it.  
GetSelectStmt(SelectStmt, 100);  
SQLExecDirect(hstmt, SelectStmt, SQL_NTS);  
  
// Determine the number of result set columns. Allocate arrays to hold   
// the C type, byte length, and buffer offset to the data.  
SQLNumResultCols(hstmt, &NumCols);  
CTypeArray = (SQLSMALLINT *) malloc(NumCols * sizeof(SQLSMALLINT));  
ColLenArray = (SQLINTEGER *) malloc(NumCols * sizeof(SQLINTEGER));  
OffsetArray = (SQLINTEGER *) malloc(NumCols * sizeof(SQLINTEGER));  
  
OffsetArray[0] = 0;  
for (i = 0; i < NumCols; i++) {  
   // Determine the column's SQL type. GetDefaultCType contains a switch   
   // statement that returns the default C type for each SQL type.  
   SQLColAttribute(hstmt, ((SQLUSMALLINT) i) + 1, SQL_DESC_TYPE, NULL, 0, NULL, (SQLPOINTER) &SQLType);  
   CTypeArray[i] = GetDefaultCType(SQLType);  
  
   // Determine the column's byte length. Calculate the offset in the   
   // buffer to the data as the offset to the previous column, plus the   
   // byte length of the previous column, plus the byte length of the   
   // previous column's length/indicator buffer. Note that the byte   
   // length of the column and the length/indicator buffer are increased   
   // so that, assuming they start on an alignment boundary, they will  
   // end on the byte before the next alignment boundary. Although this   
   // might leave some holes in the buffer, it is a relatively   
   // inexpensive way to guarantee alignment.  
   SQLColAttribute(hstmt, ((SQLUSMALLINT) i)+1, SQL_DESC_OCTET_LENGTH, NULL, 0, NULL, &ColLenArray[i]);  
   ColLenArray[i] = ALIGNBUF(ColLenArray[i]);  
   if (i)  
      OffsetArray[i] = OffsetArray[i-1]+ColLenArray[i-1]+ALIGNBUF(sizeof(SQLINTEGER));  
}  
  
// Allocate the data buffer. The size of the buffer is equal to the   
// offset to the data buffer for the final column, plus the byte length   
// of the data buffer and length/indicator buffer for the last column.  
void *DataPtr = malloc(OffsetArray[NumCols - 1] +  
               ColLenArray[NumCols - 1] + ALIGNBUF(sizeof(SQLINTEGER)));  
  
// For each column, bind the address in the buffer at the start of the   
// memory allocated for that column's data and the address at the start   
// of the memory allocated for that column's length/indicator buffer.  
for (i = 0; i < NumCols; i++)  
   SQLBindCol(hstmt,  
            ((SQLUSMALLINT) i) + 1,  
            CTypeArray[i],  
            (SQLPOINTER)((SQLCHAR *)DataPtr + OffsetArray[i]),  
            ColLenArray[i],  
            (SQLINTEGER *)((SQLCHAR *)DataPtr + OffsetArray[i] + ColLenArray[i]));  
  
// Retrieve and print each row. PrintData accepts a pointer to the data,   
// its C type, and its byte length/indicator. It contains a switch   
// statement that casts and prints the data according to its type. Code   
// to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   for (i = 0; i < NumCols; i++) {  
      PrintData((SQLCHAR *)DataPtr[OffsetArray[i]], CTypeArray[i],  
               (SQLINTEGER *)((SQLCHAR *)DataPtr[OffsetArray[i] + ColLenArray[i]]));  
   }  
}  
  
// Close the cursor.  
SQLCloseCursor(hstmt);  
```
