---
title: Alocar e liberar Buffers | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- buffers [ODBC], allocating and freeing
- allocating buffers [ODBC]
- freeing buffers [ODBC]
ms.assetid: 886bc9ed-39d4-43d2-82ff-aebc35b14d39
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 73689fb95eb9b51e7f5f16b10c43256ef63f8dd2
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="allocating-and-freeing-buffers"></a>Alocar e liberar Buffers
Todos os buffers são alocados e liberados pelo aplicativo. Se um buffer não é adiado, ele precisa existir somente para a duração da chamada para uma função. Por exemplo, **SQLGetInfo** retorna o valor associado com uma opção específica no buffer apontado pelo *InfoValuePtr* argumento. Esse buffer pode ser liberado imediatamente após a chamada a **SQLGetInfo**, conforme mostrado no exemplo de código a seguir:  
  
```  
SQLSMALLINT   InfoValueLen;  
SQLCHAR *     InfoValuePtr = malloc(50);   // Allocate InfoValuePtr.  
  
SQLGetInfo(hdbc, SQL_DBMS_NAME, (SQLPOINTER)InfoValuePtr, 50,  
            &InfoValueLen);  
  
free(InfoValuePtr);                        // OK to free InfoValuePtr.  
```  
  
 Como buffers adiadas são especificados em uma função e usados em outro, é um erro de programação de aplicativo para liberar um buffer adiado, enquanto o driver ainda espera que ele exista. Por exemplo, o endereço do \* *ValuePtr* buffer é passado para **SQLBindCol** para uso posterior pelo **SQLFetch**. Esse buffer não pode ser liberado até que a coluna é desassociada, por exemplo, com uma chamada para **SQLBindCol** ou **SQLFreeStmt** conforme mostrado no exemplo de código a seguir:  
  
```  
SQLRETURN    rc;  
SQLINTEGER   ValueLenOrInd;  
SQLHSTMT     hstmt;  
  
// Allocate ValuePtr  
SQLCHAR * ValuePtr = malloc(50);  
  
// Bind ValuePtr to column 1. It is an error to free ValuePtr here.  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, 50, &ValueLenOrInd);  
  
// Fetch each row of data and place the value for column 1 in *ValuePtr.  
// Code to check if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO   
// not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {  
   // It is an error to free ValuePtr here.  
}  
  
// Unbind ValuePtr from column 1.  It is now OK to free ValuePtr.  
SQLFreeStmt(hstmt, SQL_UNBIND);  
free(ValuePtr);  
```  
  
 Esse erro é feito facilmente declarando o buffer localmente em uma função; o buffer é liberado quando o aplicativo deixa a função. Por exemplo, o código a seguir faz com que o comportamento indefinido e provavelmente fatal no driver:  
  
```  
SQLRETURN   rc;  
SQLHSTMT    hstmt;  
  
BindAColumn(hstmt);  
  
// Fetch each row of data and try to place the value for column 1 in  
// *ValuePtr. Because ValuePtr has been freed, the behavior is undefined  
// and probably fatal. Code to check if rc equals SQL_ERROR or   
// SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmt)) != SQL_NO_DATA) {}  
  
   .  
   .  
   .  
  
void BindAColumn(SQLHSTMT hstmt)  // WARNING! This function won't work!  
{  
   // Declare ValuePtr locally.  
   SQLCHAR      ValuePtr[50];  
   SQLINTEGER   ValueLenOrInd;  
  
   // Bind rgbValue to column.  
   SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr),  
               &ValueLenOrInd);  
  
   // ValuePtr is freed when BindAColumn exits.  
}  
```

