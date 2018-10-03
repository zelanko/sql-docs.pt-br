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
manager: craigg
ms.openlocfilehash: 8edb075be1bf64dad8f4ef18924a6396b7c64e80
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47796124"
---
# <a name="c-to-sql-date"></a>C para SQL: data
O identificador para o tipo de dados ODBC C data é:  
  
 SQL_C_TYPE_DATE  
  
 A tabela a seguir mostra o ODBC do SQL para o qual data C dados pode ser convertida de tipos de dados. Para obter uma explicação das colunas e os termos na tabela, consulte [conversão de dados do C para tipos de dados SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Teste|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Comprimento de bytes da coluna > = 10<br /><br /> Coluna de comprimento de byte < 10<br /><br /> Valor de dados não for uma data válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Comprimento de caracteres da coluna > = 10<br /><br /> Coluna de comprimento < 10 caracteres<br /><br /> Valor de dados não for uma data válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|Valor de dados é uma data válida<br /><br /> Valor de dados não for uma data válida|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Valor de dados é uma data válida [a]<br /><br /> Valor de dados não for uma data válida|n/d<br /><br /> 22007|  
  
 [a] a parte de hora do carimbo de hora é definida como zero.  
  
 Para obter informações sobre quais valores são válidos em uma estrutura SQL_C_TYPE_DATE, consulte [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente neste apêndice.  
  
 Quando dados de data C são convertidos em dados de SQL de caractere, os dados de caracteres resultante estão no "*aaaa*-*mm*-*dd*" formato.  
  
 O driver ignora o valor de comprimento/indicador ao converter dados de tipo de dados date C e pressupõe que o tamanho do buffer de dados é o tamanho do tipo de dados data C. O valor de comprimento/indicador é passado a *StrLen_or_Ind* argumento na **SQLPutData** e no buffer especificado com o *StrLen_or_IndPtr* argumento **SQLBindParameter**. O buffer de dados é especificado com o *DataPtr* argumento **SQLPutData** e o *ParameterValuePtr* argumento em **SQLBindParameter**.
