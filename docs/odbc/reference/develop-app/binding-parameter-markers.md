---
title: Vinculando marcadores de parâmetro | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e625e01b9bf4771f18dd8e9807ab09100ca580c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107655"
---
# <a name="binding-parameter-markers"></a>Marcadores de parâmetro de associação
O aplicativo associa parâmetros chamando **SQLBindParameter**. **SQLBindParameter** associa um parâmetro por vez. Com ele, o aplicativo especifica o seguinte:  
  
-   O número do parâmetro. Os parâmetros são numerados no aumento da ordem dos parâmetros na instrução SQL, começando com o número 1. Embora seja legal especificar um número de parâmetro que seja maior que o número de parâmetros na instrução SQL, o valor do parâmetro será ignorado quando a instrução for executada.  
  
-   O tipo de parâmetro (entrada, entrada/saída ou saída). Exceto pelos parâmetros em chamadas de procedimento, todos os parâmetros são parâmetros de entrada. Para obter mais informações, consulte [parâmetros de procedimento](../../../odbc/reference/develop-app/procedure-parameters.md), mais adiante nesta seção.  
  
-   O tipo de dados C, o endereço e o comprimento de bytes da variável associada ao parâmetro. O driver deve ser capaz de converter os dados do tipo de dados C para o tipo de dados SQL ou um erro é retornado. Para obter uma lista de conversões com suporte, consulte [convertendo dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) no Apêndice D: tipos de dados.  
  
-   O tipo de dados SQL, a precisão e a escala do próprio parâmetro.  
  
-   O endereço de um buffer de comprimento/indicador. Ele fornece o comprimento em bytes de dados binários ou de caracteres, especifica que os dados são nulos ou especifica que os dados serão enviados com **SQLPutData**. Para obter mais informações, consulte [usando valores de comprimento/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Por exemplo, o código a seguir associa *vendedor* e *CustID* aos parâmetros para as colunas vendedor e CustID. Como o *vendedor* contém dados de caractere, que é o comprimento variável, o código especifica o comprimento de bytes de *vendedor* (11) e associa *SalesPersonLenOrInd* para conter o comprimento de bytes dos dados no *vendedor*. Essas informações não são necessárias para *CustID* porque contêm dados inteiros, cujo comprimento é fixo.  
  
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
  
 Quando **SQLBindParameter** é chamado, o driver armazena essas informações na estrutura da instrução. Quando a instrução é executada, ela usa as informações para recuperar os dados do parâmetro e enviá-los para a fonte de dados.  
  
> [!NOTE]  
>  No ODBC 1,0, os parâmetros foram associados a **SQLSetParam**. O Gerenciador de driver mapeia chamadas entre **SQLSetParam** e **SQLBindParameter**, dependendo das versões do ODBC usadas pelo aplicativo e driver.
