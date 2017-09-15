---
title: "Marcadores de parâmetro de associação | Microsoft Docs"
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
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cd8c39160ee6cafbbc9f041565a57ea29680bef7
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="binding-parameter-markers"></a>Marcadores de parâmetro de associação
O aplicativo associa parâmetros chamando **SQLBindParameter**. **SQLBindParameter** associa um parâmetro de cada vez. Com ele, o aplicativo especifica o seguinte:  
  
-   O número do parâmetro. Parâmetros são numerados em ordem crescente de parâmetro na instrução SQL, iniciando com o número 1. Enquanto estiver legal para especificar um número de parâmetro que é maior do que o número de parâmetros na instrução SQL, o valor do parâmetro será ignorado quando a instrução é executada.  
  
-   O tipo de parâmetro (entrada, entrada/saída ou de saída). Exceto para os parâmetros em chamadas de procedimento, todos os parâmetros são parâmetros de entrada. Para obter mais informações, consulte [parâmetros de procedimento](../../../odbc/reference/develop-app/procedure-parameters.md), mais adiante nesta seção.  
  
-   O comprimento C de bytes, o endereço e o tipo de dados da variável de associado ao parâmetro. O driver deve ser capaz de converter os dados do tipo de dados C para o tipo de dados SQL ou um erro será retornado. Para obter uma lista de conversões com suporte, consulte [converter dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) no Apêndice d: os tipos de dados.  
  
-   O tipo de dados SQL, precisão e escala do parâmetro em si.  
  
-   O endereço de um buffer de comprimento/indicador. Ele fornece o comprimento de bytes de dados binários ou de caractere, especifica que os dados são NULL ou especifica que os dados serão enviados com **SQLPutData**. Para obter mais informações, consulte [usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Por exemplo, o código a seguir associa *vendedor* e *CustID* aos parâmetros para as colunas de vendedor e CustID. Porque *vendedor* contém dados de caractere, que é de comprimento variável, o código especifica o comprimento em bytes de *vendedor* (11) e associa *SalesPersonLenOrInd* para contém o comprimento de bytes dos dados em *vendedor*. Essas informações não são necessárias para *CustID* porque ela contém dados de número inteiro, que é de comprimento fixo.  
  
```  
SQLCHAR       SalesPerson[11];  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLUINTEGER   CustID;  
  
// Bind SalesPerson to the parameter for the SalesPerson column and  
// CustID to the parameter for the CustID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 10, 0,  
                  SalesPerson, sizeof(SalesPerson), &SalesPersonLenOrInd);  
SQLBindParameter(hstmt1, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &CustID, 0, &CustIDInd);  
  
// Set values of salesperson and customer ID and length/indicators.  
strcpy_s((char*)SalesPerson, _countof(SalesPerson), "Garcia");  
SalesPersonLenOrInd = SQL_NTS;  
CustID = 1331;  
CustIDInd = 0;  
  
// Execute a statement to get data for all orders made to the specified  
// customer by the specified salesperson.  
SQLExecDirect(hstmt1,"SELECT * FROM Orders WHERE SalesPerson=? AND CustID=?",SQL_NTS);  
```  
  
 Quando **SQLBindParameter** é chamado, o driver armazena essas informações na estrutura da instrução. Quando a instrução é executada, ele usa as informações para recuperar os dados de parâmetro e enviá-lo à fonte de dados.  
  
> [!NOTE]  
>  No ODBC 1.0, os parâmetros foram associados com **SQLSetParam**. O Gerenciador de Driver mapeia chamadas entre **SQLSetParam** e **SQLBindParameter**, de acordo com as versões do ODBC usada pelo aplicativo e pelo driver.
