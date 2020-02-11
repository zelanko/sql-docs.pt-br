---
title: 'C to SQL: data | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02ee7c1fb396dc1c9c0708cf6c0e7a52ff1c11ec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019414"
---
# <a name="c-to-sql-date"></a>C para SQL: data
O identificador para o tipo de dados de data ODBC C é:  
  
 SQL_C_TYPE_DATE  
  
 A tabela a seguir mostra os tipos de dados ODBC do SQL para os quais os dados C de data podem ser convertidos. Para obter uma explicação das colunas e dos termos na tabela, consulte [convertendo dados de C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento de byte de coluna >= 10<br /><br /> Comprimento de bytes de coluna < 10<br /><br /> O valor dos dados não é uma data válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento de caractere de coluna >= 10<br /><br /> Comprimento de caracteres da coluna < 10<br /><br /> O valor dos dados não é uma data válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|O valor dos dados é uma data válida<br /><br /> O valor dos dados não é uma data válida|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|O valor dos dados é uma data válida [a]<br /><br /> O valor dos dados não é uma data válida|n/d<br /><br /> 22007|  
  
 [a] a parte de tempo do carimbo de data/hora é definida como zero.  
  
 Para obter informações sobre quais valores são válidos em uma estrutura de SQL_C_TYPE_DATE, consulte [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente neste apêndice.  
  
 Quando os dados de data C são convertidos em dados SQL de caractere, os dados de caractere resultantes estão no formato "*aaaa*-*mm*-*DD*".  
  
 O driver ignora o valor de comprimento/indicador ao converter dados do tipo de dados data C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados data C. O valor de comprimento/indicador é passado no argumento *StrLen_or_Ind* em **SQLPutData** e no buffer especificado com o argumento *StrLen_or_IndPtr* em **SQLBindParameter**. O buffer de dados é especificado com o argumento *DataPtr* em **SQLPutData** e o argumento *ParameterValuePtr* em **SQLBindParameter**.
