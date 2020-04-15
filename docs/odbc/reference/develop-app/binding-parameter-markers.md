---
title: Marcadores de parâmetro de ligação | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be99bc884a8baa66f3d632ee4731985f0cc85732
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306387"
---
# <a name="binding-parameter-markers"></a>Marcadores de parâmetro de associação
O aplicativo vincula parâmetros chamando **SQLBindParameter**. **SQLBindParameter** liga um parâmetro de cada vez. Com ele, o aplicativo especifica o seguinte:  
  
-   O número do parâmetro. Os parâmetros são numerados na ordem de parâmetros crescente na declaração SQL, começando pelo número 1. Embora seja legal especificar um número de parâmetro que seja maior do que o número de parâmetros na declaração SQL, o valor do parâmetro será ignorado quando a declaração for executada.  
  
-   O tipo de parâmetro (entrada, entrada/saída ou saída). Exceto para parâmetros nas chamadas de procedimento, todos os parâmetros são parâmetros de entrada. Para obter mais informações, consulte [Parâmetros de procedimento,](../../../odbc/reference/develop-app/procedure-parameters.md)mais tarde nesta seção.  
  
-   O tipo de dados C, endereço e comprimento de byte da variável vinculado ao parâmetro. O driver deve ser capaz de converter os dados do tipo de dados C para o tipo de dados SQL ou um erro é retornado. Para obter uma lista de conversões suportadas, consulte [Convertendo Dados de C para Tipos de Dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) no apêndice D: Tipos de dados.  
  
-   O tipo de dados SQL, precisão e escala do parâmetro em si.  
  
-   O endereço de um buffer de comprimento/indicador. Ele fornece o comprimento do byte de dados binários ou de caracteres, especifica que os dados são NULAS ou especifica que os dados serão enviados com **SQLPutData**. Para obter mais informações, consulte [Usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Por exemplo, o código a seguir liga *SalesPerson* e *CustID* a parâmetros para as colunas SalesPerson e CustID. Como *o SalesPerson* contém dados de caracteres, que é o comprimento variável, o código especifica o comprimento do byte do *SalesPerson* (11) e vincula *salesPersonOrInd* para conter o comprimento de byte dos dados no *SalesPerson*. Essas informações não são necessárias para *custID* porque contém dados inteiros, que são de comprimento fixo.  
  
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
  
 Quando **o SQLBindParameter** é chamado, o driver armazena essas informações na estrutura para a declaração. Quando a declaração é executada, ela usa as informações para recuperar os dados do parâmetro e enviá-los para a fonte de dados.  
  
> [!NOTE]  
>  No ODBC 1.0, os parâmetros foram vinculados com **SQLSetParam**. O Driver Manager mapeia chamadas entre **SQLSetParam** e **SQLBindParameter**, dependendo das versões do ODBC usadas pelo aplicativo e pelo driver.
