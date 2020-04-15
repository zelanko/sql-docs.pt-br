---
title: 'SQL a C: Numeric | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from SQL to C types [ODBC], numeric
- numeric data type [ODBC], converting
- converting data from SQL to C types [ODBC], numeric
ms.assetid: 76f8b5d5-4bd0-4dcb-a90a-698340e0d36e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 36b24da4023a96b686742416b83bb5790e129278
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296406"
---
# <a name="sql-to-c-numeric"></a>SQL para C: numérico

Os identificadores para os tipos de dados Numéricos ODBC SQL são os seguintes:

- SQL_DECIMAL  
- SQL_BIGINT  
- SQL_NUMERIC  
- SQL_REAL  
- SQL_TINYINT  
- SQL_FLOAT  
- SQL_SMALLINT  
- SQL_DOUBLE SQL_INTEGER  

A tabela a seguir mostra os tipos de dados ODBC C para os quais os dados SQL numéricos podem ser convertidos. Para obter uma explicação das colunas e termos da tabela, consulte [Convertendo Dados de SQL para C Tipos de Dados](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  

|Identificador de tipo C|Teste|**TargetValuePtr*|**Strlen_or_indptr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|Comprimento do byte do caractere < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) >= *BufferLength*|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_WCHAR|Comprimento do caractere < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) < *BufferLength*<br /><br /> Número de dígitos inteiros (em oposição ao fracionado) >= *BufferLength*|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Comprimento dos dados em caracteres<br /><br /> Comprimento dos dados em caracteres<br /><br /> Indefinido|n/d<br /><br /> 01004<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_NUMERIC|Dados convertidos sem truncação[a]<br /><br /> Dados convertidos com truncação de dígitos fracionados[a]<br /><br /> A conversão de dados resultaria em perda de dígitos inteiros (em oposição ao fracionado)[a]|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE|Os dados estão dentro do intervalo do tipo de dados para o qual o número está sendo convertido[a]<br /><br /> Os dados estão fora do intervalo do tipo de dados para o qual o número está sendo convertido[a]|Dados<br /><br /> Indefinido|Tamanho do tipo de dados C<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_BIT|Os dados são 0 ou 1[a]<br /><br /> Os dados são maiores que 0, menos de 2, e não são iguais a 1[a]<br /><br /> Os dados são inferiores ou superiores ou iguais a 2[a]|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|1[b]<br /><br /> 1[b]<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22003|  
|SQL_C_BINARY|Comprimento de byte de dados <= *BufferLength*<br /><br /> Comprimento de byte de dados > *BufferLength*|Dados<br /><br /> Indefinido|Duração dos dados<br /><br /> Indefinido|n/d<br /><br /> 22003|  
|SQL_C_INTERVAL_MONTH[c] SQL_C_INTERVAL_YEAR[c] SQL_C_INTERVAL_DAY[c] SQL_C_INTERVAL_HOUR[c] SQL_C_INTERVAL_MINUTE[c] SQL_C_INTERVAL_SECOND[c]|Dados não truncados<br /><br /> Porção de segundos fracionados truncada<br /><br /> Parte inteira do número truncado|Dados<br /><br /> Dados truncados<br /><br /> Indefinido|Comprimento dos dados em bytes<br /><br /> Comprimento dos dados em bytes<br /><br /> Indefinido|n/d<br /><br /> 01S07<br /><br /> 22015|  
|SQL_C_INTERVAL_YEAR_TO_MONTH SQL_C_INTERVAL_DAY_TO_HOUR SQL_C_INTERVAL_DAY_TO_MINUTE SQL_C_INTERVAL_DAY_TO_SECOND SQL_C_INTERVAL_HOUR_TO_MINUTE SQL_C_INTERVAL_HOUR_TO_SECOND|Parte inteira do número truncado|Indefinido|Indefinido|22015|  
  
 [a] O valor do *BufferLength* é ignorado para esta conversão. O driver assume que o tamanho de **TargetValuePtr* é do tamanho do tipo de dados C.  
  
 [b] Este é o tamanho do tipo de dados C correspondente.  
  
 [c] Esta conversão é suportada apenas para os tipos exatos de dados numéricos (SQL_DECIMAL, SQL_NUMERIC, SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER e SQL_BIGINT). Não é suportado para os tipos de dados numéricos aproximados (SQL_REAL, SQL_FLOAT ou SQL_DOUBLE).  

## <a name="sql_c_numeric-and-sqlsetdescfield"></a>SQL_C_NUMERIC e SQLSetDescField

 A [função SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) é necessária para executar a vinculação manual com valores SQL_C_NUMERIC. (Observe que o SQLSetDescField foi adicionado no ODBC 3.0.) Para executar a vinculação manual, primeiro você deve obter a alça do descritor.  

```cpp
if (fCType == SQL_C_NUMERIC) {   
   // special processing required for NUMERIC to get right scale & precision  
   // Modify the fields in the implicit application parameter descriptor  
   SQLHDESC hdesc=NULL;  
  
   // Use SQL_ATTR_APP_ROW_DESC for calls to SQLBindCol()  
   // Use SQL_ATTR_APP_PARAM_DESC for calls to SQLBindParameter()  
   //  
   // retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_ROW_DESC, &hdesc, 0, NULL);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);  
   if (!ODBC_CALL_SUCCESS(retcode)) {  
      printf ("\nSQLGetStmtAttr failed");  
      i = 1;  
      sqlstate[7] = '\0';  
      while (SQLGetDiagRec(SQL_HANDLE_STMT, hstmt, i, sqlstate, &NativeError, wrkbuf, sizeof(wrkbuf), &len) != SQL_NO_DATA) {  
         printf("\niTestCase = %d Failed...Precision = %d, Scale = %d\nNativeError=%d, State=%s, \n  Message=%s",   
            iTestCase, Precision, Scale, NativeError, sqlstate, wrkbuf);  
         i++;  
      }  
      continue;  
   }  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_PRECISION, (SQLPOINTER)num.precision, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_SCALE, (SQLPOINTER)num.scale, 0);  
   if (!ODBC_CALL_SUCCESS(retcode))  
      goto error;  
   retcode = SQLSetDescField(hdesc, iCol, SQL_DESC_DATA_PTR, (SQLPOINTER) &(num), sizeof(num));  
```
