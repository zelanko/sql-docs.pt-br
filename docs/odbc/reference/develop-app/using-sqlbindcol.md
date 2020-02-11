---
title: Usando SQLBindCol | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
- SQLBindCol function [ODBC], using
ms.assetid: 17277ab3-33ad-44d3-a81c-a26b5e338512
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0f466d98d5d1edec2efa824ac644ad6bb49e990a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022158"
---
# <a name="using-sqlbindcol"></a>Usar SQLBindCol
O aplicativo associa colunas chamando **SQLBindCol**. Essa função associa uma coluna por vez. Com ele, o aplicativo especifica o seguinte:  
  
-   O número da coluna. A coluna 0 é a coluna de indicadores; Esta coluna não está incluída em alguns conjuntos de resultados. Todas as outras colunas são numeradas a partir do número 1. É um erro associar uma coluna de maior número do que as colunas no conjunto de resultados; Esse erro não pode ser detectado até que o conjunto de resultados tenha sido criado, portanto, ele é retornado por **SQLFetch**, não **SQLBindCol**.  
  
-   O tipo de dados C, o endereço e o comprimento de bytes da variável associada à coluna. É um erro especificar um tipo de dados C para o qual o tipo de dados SQL da coluna não pode ser convertido; Esse erro pode não ser detectado até que o conjunto de resultados tenha sido criado, portanto, ele é retornado por **SQLFetch**, não **SQLBindCol**. Para obter uma lista de conversões com suporte, consulte [convertendo dados de SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) no Apêndice D: tipos de dados. Para obter informações sobre o comprimento do byte, consulte [comprimento do buffer de dados](../../../odbc/reference/develop-app/data-buffer-length.md).  
  
-   O endereço de um buffer de comprimento/indicador. O buffer de comprimento/indicador é opcional. Ele é usado para retornar o comprimento de bytes de dados binários ou de caracteres ou retornar SQL_NULL_DATA se os dados forem nulos. Para obter mais informações, consulte [usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Quando **SQLBindCol** é chamado, o driver associa essas informações com a instrução. Quando cada linha de dados é buscada, ela usa as informações para inserir os dados para cada coluna nas variáveis de aplicativo associadas.  
  
 Por exemplo, o código a seguir associa variáveis às colunas vendedor e CustID. Os dados das colunas serão retornados em *vendedor* e *CustID*. Como o *vendedor* é um buffer de caracteres, o aplicativo especifica seu comprimento de byte (11) para que o driver possa determinar se os dados devem ser truncados. O comprimento de bytes do título retornado ou se ele for nulo, será retornado em *SalesPersonLenOrInd*.  
  
 Como *CustID* é uma variável de inteiro e tem comprimento fixo, não é necessário especificar seu comprimento de byte; o driver pressupõe que é **sizeof (** SQLUINTEGER **)**. O comprimento de bytes dos dados de ID de cliente retornados, ou se ele for nulo, será retornado em *CustIDInd*. Observe que o aplicativo está interessado apenas em se o salário é nulo, pois o comprimento do byte é sempre **sizeof (** SQLUINTEGER **)**.  
  
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
  
 O código a seguir executa uma instrução **Select** inserida pelo usuário e imprime cada linha de dados no conjunto de resultados. Como o aplicativo não pode prever a forma do conjunto de resultados criado pela instrução **Select** , ele não pode associar variáveis embutidas em código ao conjunto de resultados como no exemplo anterior. Em vez disso, o aplicativo aloca um buffer que contém os dados e um buffer de comprimento/indicador para cada coluna nessa linha. Para cada coluna, ele calcula o deslocamento para o início da memória da coluna e ajusta esse deslocamento para que os buffers de dados e de comprimento/indicador da coluna comecem nos limites de alinhamento. Em seguida, ele associa a memória começando no deslocamento para a coluna. Do ponto de vista do driver, o endereço dessa memória é indistinguíveis do endereço de uma variável associada no exemplo anterior. Para obter mais informações sobre alinhamento, consulte [Alignment](../../../odbc/reference/develop-app/alignment.md).  
  
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
